---
layout: post
title: "Labb 1: Introduktion till Linux terminal och filsystem i Ubuntu"
categories: [blogpost]
tags: [Linux, Ubuntu, Terminal]
render_with_liquid: false
image: https://images-bonnier.imgix.net/files/kom/production/2024/04/03100724/Ubuntu-WEB.png?auto=compress,format
date: 2026-02-04 12:00:00 +0000
published: true
---
<!--more-->

{% raw %}
# Labb 1: Introduktion till Ubuntu-terminalen och Linux-filsystemet

## Inledning
I denna första labb fokuserar jag på grunderna i Linux genom att arbeta praktiskt i Ubuntu-terminalen.  
Syftet är att förstå vad terminalen är, när den används och hur Linux filsystem är uppbyggt.  
Labben är en del av min lärandeprocess där jag dokumenterar samtidigt som jag lär mig, för att bygga både förståelse och teknisk portfölj inom IT.

---

## Vad är terminalen och när används den?
Terminalen är ett textbaserat gränssnitt där man kommunicerar direkt med operativsystemet genom kommandon.  
I Linux är terminalen ett centralt verktyg och används ofta inom:

- systemadministration
- felsökning
- serverdrift
- arbete i miljöer utan grafiskt gränssnitt

Även om många uppgifter kan göras grafiskt ger terminalen större kontroll och bättre insyn i hur systemet fungerar.

---

## Linux filsystem – en överblick
Linux använder ett hierarkiskt filsystem som börjar i rotkatalogen `/`.  
Till skillnad från Windows finns inga enhetsbokstäver, utan allt är organiserat i en sammanhängande struktur.

Några viktiga kataloger:

- `/` – rotkatalogen, grunden för hela systemet  
- `/home` – användarnas hemkataloger  
- `/etc` – system- och programkonfiguration  
- `/var` – loggfiler och variabel data (t.ex. systemloggar)

Att förstå dessa kataloger gör det lättare att navigera och felsöka i systemet.

---

## Grundläggande terminalkommandon

### Visa aktuell katalog – `pwd`
```bash
pwd
```

### Lista filer och mappar – `ls`
```bash
ls
ls -l
ls -la
```

- `ls` visar innehållet i katalogen
- `-l` visar detaljerad information
- `-a` visar även dolda filer

### Byta katalog – `cd`
```bash
cd /etc
cd ~
cd ..
```

- `cd /etc` går till katalogen `/etc`
- `cd ~` går till hemkatalogen
- `cd ..` går upp en nivå

### Skapa och ta bort mappar – `mkdir` och `rmdir`
```bash
mkdir testmapp
rmdir testmapp
```

`rmdir` fungerar endast om mappen är tom.

### Skapa och ta bort filer – `touch` och `rm`
```bash
touch fil.txt
rm fil.txt
```

- `touch` skapar en tom fil
- `rm` tar bort filer direkt, utan bekräftelse

### Visa filinnehåll – `cat` och `less`
```bash
cat fil.txt
less fil.txt
```

- `cat` visar hela filen direkt
- `less` är bättre för större filer och låter dig scrolla

---

## Navigering och sökning

### Hitta filer – `find`
```bash
find /home -name fil.txt
```

Söker efter filer i en katalogstruktur.

### Söka i text – `grep`
```bash
grep "error" loggfil.txt
```

Används för att söka efter text i filer, ofta i loggar.

### Tab-komplettering
Genom att trycka på Tab kan terminalen automatiskt komplettera:

- filnamn
- katalognamn
- kommandon

Detta minskar risken för stavfel och sparar tid.

---

## Behörigheter och ägarskap
Linux använder ett behörighetssystem baserat på:

- ägare (user)
- grupp (group)
- övriga (others)

Behörigheter visas som `rwx`:

- `r` = read (läsa)
- `w` = write (skriva)
- `x` = execute (köra)

### Ändra behörigheter – `chmod`
```bash
chmod 644 fil.txt
```

Ändrar vem som får läsa och skriva till filen.

### Ändra ägare – `chown`
```bash
sudo chown user:user fil.txt
```

Ändrar ägare och grupp för en fil (kräver sudo).

---

## Laboration demo – enkel övning
Som praktisk övning genomfördes följande:

- Skapa en katalog med `mkdir`
- Skapa en fil med `touch`
- Skriv innehåll i filen
- Visa innehållet med `cat` och `less`
- Kontrollera behörigheter med `ls -l`
- Ta bort filen och katalogen

Denna övning gav en tydlig helhetsbild av hur man arbetar med filer i Linux.

---

## Sammanfattning
I denna labb har jag fått en introduktion till Ubuntu-terminalen och Linux-filsystemet.  
Genom praktiska kommandon har jag lärt mig hur man navigerar, hanterar filer och förstår systemets struktur.

Detta är en viktig grund för vidare arbete inom Linux, IT-support och systemadministration.
{% endraw %}

