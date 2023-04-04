---
title: TMUX nohup 
date: 20230126
author: realcaptainsolaris 
---

# Sleep
Bash 20 Sekunden schlafen legen:

    sleep 20 

STRG + Z bringt Prozess in den Hintergrund.
    [1]+  Angehalten              sleep 20

entspricht:

    sudo kill -SIGSTOP 1234

STRG + C sendt immer einen SIGINT:

    sudo kill -SIGINT 1234

## Job
prüfen, ob Prgramme im Hintergrund laufen

    jobs
    [1]+  Angehalten              sleep 20

## FG
Programm wieder in den Vordergrund holen

    fg 1

## NOHUP
nohup - run a command immune to hangups, with output to a non-tty
Wenn man längere Zeit eingeloggt ist, und ein Prozess lange dauert, 
können wir nohup verwenden, um eine Datenübertragung nicht zu unterbrechen.

nohup ist ein Befehl, um ein Programm auszuführen, wobei dieses dann das HUP-Signal unterdrückt. Dadurch kann man ein Programm starten und weiter laufen lassen, auch wenn man sich vom System abgemeldet hat.

    gedit &

Wenn man das Programm startet, aber das TErminal schließt, sendet
Terminal beim Schliessen ein SIGHUP und gedit wird geschlossen.

    nohup gedit &

Gedit bleibt auch nach schließen des terminals offen.


## SCREEN
Screen hat die gleiche Aufgabe wie nohup. Beim Einloggen via SSH auf 
einem remote Server, starte ein Programm und logge mich wieder aus: mit scren
wird das Programm nicht beendet.


