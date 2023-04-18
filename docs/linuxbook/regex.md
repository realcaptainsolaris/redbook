---
title: Regexe
date: 20230126
author: realcaptainsolaris 
---

# Reguläre Ausdrücke (Regex)
Zeichenketten durchsuchen.

## Grundlegende Ausdrücke mit grep

Match Winter:

    echo "Winter am See" | grep -in w.*r

Alle Dateien im Verzeichnis, die mit tag anfangen (caseinsensitive)

    ls | grep -i ^tag

Alle Zip-Dateien, die ins Schema tag_Zahl.zip passen

    ls | grep -i "tag_[0-9]\.zip$"

## erweiterte Ausdrücke mit egrep
 
    echo "das Haus am Wald ist leer" | egrep "Haus am Wald ist (leer|gross)"
