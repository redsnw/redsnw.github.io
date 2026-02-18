---
layout: post
title: "n8n autosvar pa bloggfragor med Gmail och Ollama"
categories: [blogpost]
tags: [n8n, Gmail, Ollama, Automation]
render_with_liquid: false
image: assets/img/n8n-workflow-autosvar.png
image_fit: contain
---

<!--more-->

{% raw %}
## Introduktion
I denna genomgang visar jag hur jag byggde ett automatiskt e-postsvar for fragor fran bloggen.
Flodet tar emot mail, filtrerar ratt meddelanden, genererar svar med lokal AI (Ollama) och skickar tillbaka svaret via Gmail i n8n.

Malet var:
- inga API-kostnader for AI
- autosvar pa svenska
- enkel felsokning om nagot gar fel

## Tutorial
### Arkitektur
Flodet i n8n:
1) `Gmail Trigger`
2) `If` (filtrering av bloggmail)
3) `HTTP Request` mot Ollama
4) `Send a message` (Gmail)

### 1. Starta n8n lokalt i Docker
```powershell
docker volume create n8n_data
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

Oppna:
```text
http://localhost:5678
```

### 2. Koppla Gmail i n8n
Jag anvande OAuth2 med Google Cloud:
- API: Gmail API
- OAuth client type: Web application
- Redirect URI:

```text
http://localhost:5678/rest/oauth2-credential/callback
```

Nar credentials var sparade kunde `Gmail Trigger` lasa inkommande mail.

### 3. IF-filter for att fanga formularmail
Eftersom subject varierar filtrerade jag pa innehall i `snippet`.

Condition 1:
```text
{{$json.snippet}} contains E-post:
```

Condition 2:
```text
{{$json.snippet}} contains Fraga:
```

Logik:
```text
AND
```

### 4. Installera och kora Ollama lokalt
Installera Ollama for Windows och kor:

```powershell
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" pull llama3.1:8b
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" serve
```

Tips: hall `serve` igang i ett eget terminalfonster.

### 5. HTTP Request fran n8n till Ollama
I n8n korde jag `POST` till:

```text
http://host.docker.internal:11434/api/generate
```

Body (JSON):
```json
{
  "model": "llama3.1:8b",
  "prompt": "Svara kort och professionellt pa svenska pa detta mail:\\n\\n{{$json.snippet}}\\n\\nMax 5 meningar. Avsluta med: Detta ar ett automatiskt svar.",
  "stream": false
}
```

### 6. Skicka autosvar med Gmail
I `Send a message`:

To (Expression):
```text
{{ ($node["If"].json.snippet.match(/E-post:\s*([^\s]+)/) || [])[1] }}
```

Subject:
```text
Svar pa din fraga
```

Message (Expression):
```text
{{ $node["HTTP Request"].json.response }}
```

### 7. Vanliga problem jag stotte pa
- `The recipients address is empty` i EmailJS: fel i template-faltet `To Email`.
- `Insufficient quota detected` i OpenAI: API-billing var inte aktiverad.
- `service refused the connection` i n8n HTTP: fel host (`localhost` i container). Lostes med `host.docker.internal`.
- `Reference node doesn't exist`: fel nodnamn i expression (`IF` vs `If`).

## Sammanfattning
Losningen fungerar nu helt lokalt:
- formular pa bloggen skickar mail
- n8n fangar ratt mail
- Ollama genererar autosvar
- Gmail skickar svaret tillbaka automatiskt

Nasta steg ar att lagga till:
- max 1 autosvar per avsandare per 24h
- blockering av no-reply-adresser
- battre loggning av skickade autosvar

## Referenser
```text
https://n8n.io/
https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/
https://ollama.com/
https://github.com/ollama/ollama/blob/main/docs/api.md
https://console.cloud.google.com/
```
{% endraw %}

