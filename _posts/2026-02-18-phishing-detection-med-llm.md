---
layout: post
title: "Phishing detection med LLM"
categories: [blogpost]
tags: [Phishing, LLM, Detection, Security, n8n, Ollama]
render_with_liquid: false
image: assets/img/phish_cam_1-768x768.jpeg
image_fit: contain
---

<!--more-->

{% raw %}
## Introduktion
I den här posten visar jag hur jag byggde ett automatiserat phishing-filter i n8n.
Flödet kombinerar:
- hårda nyckelordsregler (snabb blockering)
- AI-klassificering med Ollama (bättre bedömning)
- automatisk Gmail-label för `PHISHING` eller `SAFE`

Målet var att få en enkel men praktisk lösning som går att köra lokalt utan API-kostnad.

## Tutorial
### Flöde i n8n
Min pipeline:
1) `Gmail Trigger` - läser inkommande mail
2) `Get a message` - hämtar full mailtext
3) `Code` - extraherar textfält (`text`, `html`, `textAsHtml`)
4) `If` (bloggfilter) - tar bara mail från bloggformuläret
5) `If` (hard rule) - fångar tydliga phishing-signaler
6) `HTTP Request` mot Ollama - AI-klassificering
7) `Edit Fields` - parse av AI-svar till `label`, `confidence`, `reason`
8) `If` - om `label=phishing` sätt phishing-label, annars safe-label

### 1. Hard rule med nyckelord
För snabb första kontroll körde jag regex i en `If`-nod:

```text
/(spärras inom|verifiera direkt|ange din mfa|klicka här för att behålla åtkomst|bit\.ly|tinyurl|\.ru\/)/i
```

Om den matchar går mailet direkt till phishing-label.

### 2. AI-klassificering med Ollama
I `HTTP Request` skickade jag hela mailet till:

```text
http://host.docker.internal:11434/api/generate
```

Body:
```json
{
  "model": "llama3.1:8b",
  "prompt": "Klassificera ENDAST som phishing om tydliga bedrägerisignaler finns. Vanliga frågor = safe. Svara ENDAST JSON {\"label\":\"phishing|safe\",\"confidence\":0-100,\"reason\":\"kort\"}. MAIL: {{$json.text || $json.fullText || $json.textAsHtml || ''}}",
  "stream": false,
  "format": "json"
}
```

### 3. Labeling i Gmail
Efter AI-svar:
- `label = phishing` -> `PHISHING-DETECT`
- annars -> `SAFE-AUTO`

Det gör inboxen mycket snabbare att triagera.

### 4. Vanliga fel jag stötte på
- `JSON parameter needs to be valid JSON`: trasig body i HTTP Request.
- `The resource you are requesting could not be found`: fel model-namn, kontrollera med `ollama list`.
- `If` går alltid false: jämförde fel fält (`subject`) i stället för full text.
- Dubbelkopplad label-node: samma mail märktes från två grenar.

### 5. Testmail jag använde
Phishing-test:
```text
Ditt konto spärras inom 30 minuter. Klicka här för att behålla åtkomst:
http://bit.ly/secure-check-now
Ange din MFA-kod för verifiering.
```

Normal-test:
```text
Tack för ett bra inlägg. Kan du förklara skillnaden mellan filrättigheter
och ägarskap i Linux med ett enkelt exempel?
```

## Sammanfattning
Det här upplägget gav bra balans mellan:
- snabb regex-detektering
- AI-bedömning på mail som inte är självklara
- enkel hantering via labels i Gmail

Nyckeln var att hålla logiken enkel: hard rule först, AI efter, och tydliga labels.

## Referenser
```text
https://n8n.io/
https://docs.n8n.io/
https://ollama.com/
https://github.com/ollama/ollama/blob/main/docs/api.md
```
{% endraw %}
