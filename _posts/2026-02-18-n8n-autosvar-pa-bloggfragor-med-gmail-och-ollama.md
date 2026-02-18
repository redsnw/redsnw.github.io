---
layout: post
title: "n8n autosvar på bloggfrågor med Gmail och Ollama"
categories: [blogpost]
tags: [n8n, Gmail, Ollama, Automation]
render_with_liquid: false
image: assets/img/mindmap-redsnw-github-io.jpg
---

<!--more-->

{% raw %}
## Introduktion
I denna genomgång visar jag hur jag byggde ett automatiskt e-postsvar för frågor från bloggen.
Flödet tar emot mail, filtrerar rätt meddelanden, genererar svar med lokal AI (Ollama) och skickar tillbaka svaret via Gmail i n8n.

Målet var:
- inga API-kostnader för AI
- autosvar på svenska
- enkel felsökning om något går fel

## Tutorial

### Arkitektur
Flödet i n8n:
1) `Gmail Trigger`
2) `If` (filtrering av bloggmail)
3) `HTTP Request` mot Ollama
4) `Send a message` (Gmail)

### 1. Starta n8n lokalt i Docker
```powershell
docker volume create n8n_data
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

Öppna:
```text
http://localhost:5678
```

### 2. Koppla Gmail i n8n
Jag använde OAuth2 med Google Cloud:
- API: Gmail API
- OAuth client type: Web application
- Redirect URI:

```text
http://localhost:5678/rest/oauth2-credential/callback
```

När credentials var sparade kunde `Gmail Trigger` läsa inkommande mail.

### 3. IF-filter för att fånga formulärmail
Eftersom subject varierar filtrerade jag på innehåll i `snippet`.

Condition 1:
```text
{{$json.snippet}} contains E-post:
```

Condition 2:
```text
{{$json.snippet}} contains Fråga:
```

Logik:
```text
AND
```

### 4. Installera och köra Ollama lokalt
Installera Ollama för Windows och kör:

```powershell
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" pull llama3.1:8b
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" serve
```

Tips: håll `serve` igång i ett eget terminalfönster.

### 5. HTTP Request från n8n till Ollama
I n8n körde jag `POST` till:

```text
http://host.docker.internal:11434/api/generate
```

Body (JSON):
```json
{
  "model": "llama3.1:8b",
  "prompt": "Svara kort och professionellt pa svenska pa detta mail:\n\n{{$json.snippet}}\n\nMax 5 meningar. Avsluta med: Detta ar ett automatiskt svar.",
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
Svar på din fråga
```

Message (Expression):
```text
{{ $node["HTTP Request"].json.response }}
```

### 7. Vanliga problem jag stötte på
- `The recipients address is empty` i EmailJS: fel i template-fältet `To Email`.
- `Insufficient quota detected` i OpenAI: API-billing var inte aktiverad.
- `service refused the connection` i n8n HTTP: fel host (`localhost` i container). Löstes med `host.docker.internal`.
- `Reference node doesn't exist`: fel nodnamn i expression (`IF` vs `If`).

## Sammanfattning
Lösningen fungerar nu helt lokalt:
- formulär på bloggen skickar mail
- n8n fångar rätt mail
- Ollama genererar autosvar
- Gmail skickar svaret tillbaka automatiskt

Nästa steg är att lägga till:
- max 1 autosvar per avsändare per 24h
- blockering av no-reply-adresser
- bättre loggning av skickade autosvar

## Referenser
```text
https://n8n.io/
https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/
https://ollama.com/
https://github.com/ollama/ollama/blob/main/docs/api.md
https://console.cloud.google.com/
```
{% endraw %}

