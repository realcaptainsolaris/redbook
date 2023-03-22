---
title: Prozesse
date: 20230126
author: realcaptainsolaris 
---

# Prozesse 

## PS
processes zeigt die laufenden Prozesse des Systems an

UID = User
PID = Prozess ID
PPID = Parent Prozess ID
C = 


### -ef
Alle Prozesse anzeigen (e), in vollem Format (f)

    ps -ef

Prozess der Bash:

    ps -ef | grep bash

##  pstree
pstree zeigt Prozesse in Baumansicht. (p) für Baum mit Prozess-ID.

    pstree | grep bash
    pstree -p | grep node

## top
Zeigt Prozesse an

    top

- PID = Prozess ID
- USER 
- PR = Priorität
- NI = Nice Wert
- VIRT = virtueller Speicher inkl. shared libs und Swapped
- RES = Reserved Memory, physikalischer Arbeitsspeicher
- SHR = shared 
- S = STATUS (R = Running, Z = Zombie, S = Sleep)
- %CPU = CPU Last
- %MEM = Teil des physikalischen Speichers

Root Prozesse ansehen:

    top -u root

Prozesse mit ID 11222 - 12345

    top -p 11222,12345

## Uptime
Zeigt an, wie lange das SYstem läuft, wieviele User angemeldet sind
und mit load average die mittlere Systemauslastung an. 

    uptime
    23:48:04 up  3:56,  1 user,  load average: 0,97, 0,90, 0,83

Load Avagere in letzter Minute, letzten 5 Minuten, letzten 15 Minuten
Generell sollte der Wert nicht höher werden als die Anzahl der
Prozessorkerne, da sonst Prozesse in der Warteschlange liegen.

## Free
Zeigt die Speicherauslastung an, (h) für human readable

    free -h
