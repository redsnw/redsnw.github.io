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
`pwd` = visar aktuell katalog  
```bash
pwd
```

2) Lista filer (inkl dolda)  
`ls` = listar filer, `-l` = detaljer, `-a` = dolda  
```bash
ls -la
```

3) Gå till hemkatalogen  
`cd` = byt katalog  
```bash
cd ~
```

4) Skapa mapp och gå in  
`mkdir` = skapa mapp  
```bash
mkdir linux-labb
cd linux-labb
```

5) Skapa fil  
`touch` = skapa tom fil  
```bash
touch anteckningar.txt
```

6) Visa filinnehåll  
`cat` = visar fil direkt  
```bash
cat anteckningar.txt
```

7) Öppna fil med scroll  
`less` = läs fil med scroll  
```bash
less anteckningar.txt
```

8) Gå upp och ta bort  
`rm` = ta bort fil, `rmdir` = ta bort tom mapp  
```bash
cd ..
rm linux-labb/anteckningar.txt
rmdir linux-labb
```

## Navigering och sök
Här lär du dig hitta filer och söka i text från terminalen:

**find** – sök efter filer i en katalogstruktur:
```bash
find /home -name fil.txt
```

**grep** – sök efter text i filer (vanligt i loggar):
```bash
grep "error" loggfil.txt
```

**Tab-komplettering** – tryck Tab för att auto-komplettera filer, mappar och kommandon.

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

## Sammanfattning
I labben har du fått grunderna i terminalnavigering, filhantering och rättigheter. Detta är en stabil bas för vidare arbete inom Linux, IT-support och systemadministration.

## Referenser
{% endraw %}

