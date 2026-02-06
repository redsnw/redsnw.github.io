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
Skriv en kort introduktion till labben och vad man kommer lara sig.

## Terminalen i Ubuntu
Beskriv kort vad terminalen ar och nar den ar anvandbar.

## Filsystem i Linux
Forklara mappstruktur (/, /home, /etc, /var) och var filer normalt ligger.

## Viktiga kommandon
### 1. pwd (var ar jag?)
Beskriv vad kommandot gor och ge ett exempel.

### 2. ls (lista filer)
Beskriv vanliga flaggor som -l och -a.

### 3. cd (byt katalog)
Beskriv absoluta och relativa vagar.

### 4. mkdir / rmdir
Skapa och ta bort mappar.

### 5. touch / rm
Skapa och ta bort filer.

### 6. cat / less
Lasa filer i terminalen.

## Navigering och sok
Beskriv find, grep och tab-komplettering.

## Behorigheter och agarskap
Forklara chmod, chown och rattigheter (rwx).

## Laboration demo
## Uppgift: Skapa och hantera en liten projektmapp

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

## Referenser
Lista eventuella kallor eller laenk-tips.
{% endraw %}
