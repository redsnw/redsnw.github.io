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
I denna genomgÃ¥ng visar jag hur jag byggde ett automatiskt e-postsvar fÃ¶r frÃ¥gor frÃ¥n bloggen.
FlÃ¶det tar emot mail, filtrerar rÃ¤tt meddelanden, genererar svar med lokal AI (Ollama) och skickar tillbaka svaret via Gmail i n8n.

MÃ¥let var:
- inga API-kostnader fÃ¶r AI
- autosvar pÃ¥ svenska
- enkel felsÃ¶kning om nÃ¥got gÃ¥r fel

## Tutorial

### Arkitektur
FlÃ¶det i n8n:
1) `Gmail Trigger`
2) `If` (filtrering av bloggmail)
3) `HTTP Request` mot Ollama
4) `Send a message` (Gmail)

### 1. Starta n8n lokalt i Docker
```powershell
docker volume create n8n_data
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

Ã–ppna:
```text
http://localhost:5678
```

### 2. Koppla Gmail i n8n
Jag anvÃ¤nde OAuth2 med Google Cloud:
- API: Gmail API
- OAuth client type: Web application
- Redirect URI:

```text
http://localhost:5678/rest/oauth2-credential/callback
```

NÃ¤r credentials var sparade kunde `Gmail Trigger` lÃ¤sa inkommande mail.

### 3. IF-filter fÃ¶r att fÃ¥nga formulÃ¤rmail
Eftersom subject varierar filtrerade jag pÃ¥ innehÃ¥ll i `snippet`.

Condition 1:
```text
{{$json.snippet}} contains E-post:
```

Condition 2:
```text
{{$json.snippet}} contains FrÃ¥ga:
```

Logik:
```text
AND
```

### 4. Installera och kÃ¶ra Ollama lokalt
Installera Ollama fÃ¶r Windows och kÃ¶r:

```powershell
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" pull llama3.1:8b
& "$env:LOCALAPPDATA\Programs\Ollama\ollama.exe" serve
```

Tips: hÃ¥ll `serve` igÃ¥ng i ett eget terminalfÃ¶nster.

### 5. HTTP Request frÃ¥n n8n till Ollama
I n8n kÃ¶rde jag `POST` till:

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
Svar pÃ¥ din frÃ¥ga
```

Message (Expression):
```text
{{ $node["HTTP Request"].json.response }}
```

### 7. Vanliga problem jag stÃ¶tte pÃ¥
- `The recipients address is empty` i EmailJS: fel i template-fÃ¤ltet `To Email`.
- `Insufficient quota detected` i OpenAI: API-billing var inte aktiverad.
- `service refused the connection` i n8n HTTP: fel host (`localhost` i container). LÃ¶stes med `host.docker.internal`.
- `Reference node doesn't exist`: fel nodnamn i expression (`IF` vs `If`).

## Sammanfattning
LÃ¶sningen fungerar nu helt lokalt:
- formulÃ¤r pÃ¥ bloggen skickar mail
- n8n fÃ¥ngar rÃ¤tt mail
- Ollama genererar autosvar
- Gmail skickar svaret tillbaka automatiskt

NÃ¤sta steg Ã¤r att lÃ¤gga till:
- max 1 autosvar per avsÃ¤ndare per 24h
- blockering av no-reply-adresser
- bÃ¤ttre loggning av skickade autosvar

## Referenser
```text
https://n8n.io/
https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/
https://ollama.com/
https://github.com/ollama/ollama/blob/main/docs/api.md
https://console.cloud.google.com/
```
{% endraw %}


