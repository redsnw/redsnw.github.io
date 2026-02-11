---
layout: post
title: "Introduktion till Linux terminal och filsystem i Ubuntu"
categories: [blogpost]
tags: [Linux, Ubuntu, Terminal]
render_with_liquid: false
image: https://images-bonnier.imgix.net/files/kom/production/2024/04/03100724/Ubuntu-WEB.png?auto=compress,format
---

<!--more-->

{% raw %}
## Introduktion
I denna labb får du en snabb introduktion till Ubuntu-terminalen och Linux-filsystemet. Du lär dig grunderna i navigering, filhantering och viktiga kommandon som du behöver för vidare Linux-arbete.

## Uppgift

### Skapa och hantera en liten projektmapp

1) Visa var du är  
<a class="glossary-term" href="/termlista/#term-pwd" data-tip="Visar nuvarande katalog (var du &auml;r).">pwd</a> = visar aktuell katalog  
```bash
pwd
```

2) Lista filer (inkl dolda)  
<a class="glossary-term" href="/termlista/#term-ls" data-tip="Listar filer och mappar i en katalog.">ls</a> = listar filer, `-l` = detaljer, `-a` = dolda  
```bash
ls -la
```

3) Gå till hemkatalogen  
<a class="glossary-term" href="/termlista/#term-cd" data-tip="Byter katalog (navigerar i filsystemet).">cd</a> = byt katalog  
```bash
cd ~
```

4) Skapa mapp och gå in  
<a class="glossary-term" href="/termlista/#term-mkdir" data-tip="Skapar en ny mapp.">mkdir</a> = skapa mapp  
```bash
mkdir linux-labb
cd linux-labb
```

5) Skapa fil  
<a class="glossary-term" href="/termlista/#term-touch" data-tip="Skapar en tom fil eller uppdaterar en fil.">touch</a> = skapa tom fil  
```bash
touch anteckningar.txt
```

6) Visa filinnehåll  
<a class="glossary-term" href="/termlista/#term-cat" data-tip="Visar filinneh&aring;ll direkt i terminalen.">cat</a> = visar fil direkt  
```bash
cat anteckningar.txt
```

7) Öppna fil med scroll  
<a class="glossary-term" href="/termlista/#term-less" data-tip="L&auml;ser filer sida f&ouml;r sida med scroll.">less</a> = läs fil med scroll  
```bash
less anteckningar.txt
```

8) Gå upp och ta bort  
<a class="glossary-term" href="/termlista/#term-rm" data-tip="Tar bort filer (och mappar med flaggor).">rm</a> = ta bort fil, <a class="glossary-term" href="/termlista/#term-rmdir" data-tip="Tar bort en tom mapp.">rmdir</a> = ta bort tom mapp  
```bash
cd ..
rm linux-labb/anteckningar.txt
rmdir linux-labb
```

<figure class="demo-video-card">
  <figcaption class="demo-video-label">Demo-video (projektmapp)</figcaption>
  <a href="https://www.youtube.com/watch?v=h94PqoOC02s" target="_blank" rel="noopener noreferrer">
    <img src="https://img.youtube.com/vi/h94PqoOC02s/0.jpg" alt="Demo video för projektmapp i Ubuntu-terminalen" loading="lazy" />
  </a>
</figure>

## Navigering och sök
Här lär du dig hitta filer och söka i text från terminalen:

<a class="glossary-term" href="/termlista/#term-find" data-tip="S&ouml;ker efter filer och mappar i katalogtr&auml;d."><strong>find</strong></a> – sök efter filer i en katalogstruktur:
```bash
find /home -name fil.txt
```

<a class="glossary-term" href="/termlista/#term-grep" data-tip="S&ouml;ker efter text i filer."><strong>grep</strong></a> – sök efter text i filer (vanligt i loggar):
```bash
grep "error" loggfil.txt
```

**Tab-komplettering** – tryck Tab för att auto-komplettera filer, mappar och kommandon.

### Uppgift: Navigering och sök
1) Skapa en mapp med undermappar och filer  
```bash
mkdir -p sok-uppgift/rapport sok-uppgift/loggar
touch sok-uppgift/rapport/anteckningar.txt
touch sok-uppgift/loggar/system.log
```

2) Lägg in några rader text i loggfilen (valfritt)  
```bash
printf "INFO start\nERROR fel hittad\nINFO klar\n" > sok-uppgift/loggar/system.log
```

3) Sök efter ordet **ERROR** i loggfilen med `grep`  
```bash
grep "ERROR" sok-uppgift/loggar/system.log
```

4) Hitta alla `.log`-filer i mappen med `find`  
```bash
find sok-uppgift -name "*.log"
```

5) Hitta filen `anteckningar.txt` från din hemkatalog  
```bash
find ~ -name "anteckningar.txt"
```

6) Använd Tab-komplettering när du skriver fil- och mappnamn  
(t.ex. skriv `sok-` + Tab)

7) Gå in i mappen `rapport` och lista innehåll  
```bash
cd sok-uppgift/rapport
ls -la
```

8) Rensa upp allt  
```bash
cd ~
rm -r sok-uppgift
```

<figure class="demo-video-card">
  <figcaption class="demo-video-label">Demo-video (navigering och sök)</figcaption>
  <a href="https://www.youtube.com/watch?v=ijALfKOxDMc" target="_blank" rel="noopener noreferrer">
    <img src="https://img.youtube.com/vi/ijALfKOxDMc/0.jpg" alt="Demo video för navigering och sök i Linux-terminalen" loading="lazy" />
  </a>
</figure>

## Behörigheter och ägarskap
Linux använder ägare, grupp och övriga med rättigheter `rwx`:

- `r` = read (läsa)
- `w` = write (skriva)
- `x` = execute (köra)

**chmod** – ändra behörigheter:
```bash
chmod 644 fil.txt
```

**chown** – ändra ägare och grupp (kräver sudo):
```bash
sudo chown user:user fil.txt
```

### Skapa och byta till en vanlig användare
1) Skapa användaren  
```bash
sudo adduser testuser
```

2) Byt till användaren  
```bash
su - testuser
```

3) Gå tillbaka till din vanliga användare  
```bash
exit
```

### Uppgift: Behörigheter och ägarskap
1) Skapa en mapp med två filer  
```bash
mkdir behorighet-test
touch behorighet-test/offentlig.txt
touch behorighet-test/privat.txt
```

2) Kontrollera behörigheter  
```bash
ls -l behorighet-test
```

3) Gör `privat.txt` bara läsbar för ägaren  
```bash
chmod 600 behorighet-test/privat.txt
```

4) Gör `offentlig.txt` läsbar för alla  
```bash
chmod 644 behorighet-test/offentlig.txt
```

5) Kontrollera att ändringarna slog igenom  
```bash
ls -l behorighet-test
```

6) Byt till vanlig användare (testuser)  
```bash
su - testuser
```

7) Testa både offentlig och privat fil  
```bash
cat /home/<din-anvandare>/behorighet-test/offentlig.txt
cat /home/<din-anvandare>/behorighet-test/privat.txt
```

8) Rensa upp  
```bash
exit
rm -r behorighet-test
```

<figure class="demo-video-card">
  <figcaption class="demo-video-label">Demo-video (behörigheter och ägarskap)</figcaption>
  <a href="https://www.youtube.com/watch?v=mzE1N96KqlE" target="_blank" rel="noopener noreferrer">
    <img src="https://img.youtube.com/vi/mzE1N96KqlE/0.jpg" alt="Demo video för behörigheter och ägarskap i Linux" loading="lazy" />
  </a>
</figure>

## Sammanfattning
I labben har du fått grunderna i terminalnavigering, filhantering och rättigheter. Detta är en stabil bas för vidare arbete inom Linux, IT-support och systemadministration.

## Referenser
{% endraw %}

