---
title: File system
date: 20230126
author: realcaptainsolaris 
---

# Dateisystem überwachen 

## du (Disk usage)

Summarize and humanize:

    sudo du -hs /    
    sudo du -hs ~   

maximale Tiefe angeben und sortieren

    sudo du -h --max-depth=2 ~ | sort -h

## df (disk free)
Festplattenspeicher (belegt, frei) anzeigen

    df -h 

Inodes (Dateisystemeinträge mit Metadaten) anzeigen.

    df -i

## fsck 
Filesystemcheck (nur mit ausgehängter Partition)

    sudo umount /dev/sdc1
    sudo fsck /dev/sdc1


## mke2fs
Erstellt ext-Dateisysteme. Mkfs hartlinked auf mke2fs

## tunefs
Einstellungen am Dateisystem vornehmen.

Alle Informationen zur Partition anzeigen:
    sudo tune2fs -l /dev/sda1

## xfs_repair

Dateisystem reparieren, Partition vorher aushängen

## xfs_db
Dateisystem untersuchen (debuggen), Partition vorher aushängen

