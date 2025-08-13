---
title:  Wichtige Netzwerk-Befehle
date: 20200820
author: Captain Solaris
---


# Netzwerk-Untersuchung – Komplette Übersicht

## 1. IP- & Interface-Informationen

### Was ist das?

Zeigt, welche **IP-Adressen**, **Subnetze** und **Statusinformationen** deine Netzwerk-Schnittstellen aktuell haben.

### Wofür nutzen?

* Prüfen, ob du eine gültige IP-Adresse hast.
* Erkennen, ob IPv4 oder IPv6 verwendet wird.
* Status (UP/DOWN, RX/TX-Statistiken) abfragen.

### Befehle

```bash
ip addr show
ip -4 addr show dev wlp0s20f3
ip -s link show dev wlp0s20f3
```

### Typische Fehler

* Falsche IP oder kein Eintrag → kein DHCP oder statische IP falsch gesetzt.
* Interface DOWN → Kabel/WLAN getrennt oder deaktiviert.
* Hohe RX/TX-Drops → Überlast oder Hardwareproblem.

---

## 2. Routing & Gateway

### Was ist das?

Routing ist der Prozess, wie dein System entscheidet, **wohin** Datenpakete geschickt werden.
Das Gateway ist der „Ausgang“ aus deinem lokalen Netz ins nächste Netz (oft ins Internet).

### Wofür nutzen?

* Prüfen, ob der richtige Standard-Gateway eingetragen ist.
* Routen für interne Netze kontrollieren.
* Fehler beim Zugriff auf fremde Netze finden.

### Befehle

```bash
ip route show
ip route get 1.1.1.1
```

### Typische Fehler

* Falscher Gateway → kein Internetzugang.
* Mehrere Default-Routen mit ähnlicher Metrik → unvorhersehbares Verhalten.
* Fehlende Route zu einem Subnetz → bestimmte Geräte nicht erreichbar.

---

## 3. ARP & Nachbarn im LAN

### Was ist das?

ARP (Address Resolution Protocol) wandelt IP-Adressen in MAC-Adressen um, damit Geräte im gleichen Subnetz direkt kommunizieren können.

### Wofür nutzen?

* Prüfen, ob ein Gerät im LAN aktiv ist.
* MAC-Adresse sehen → Hersteller/Typ ermitteln.
* ARP-Probleme (z. B. „Gratuitous ARP“-Spam) entdecken.

### Befehle

```bash
ip neigh show
arp -a
```

### Typische Fehler

* Alte/fehlerhafte ARP-Einträge → falsche MAC-Zuordnung, keine Verbindung.
* ARP-Cache voll oder blockiert → starke Netzwerkausfälle.

---

## 4. Netzwerk-Scan & Hostnamen

### Was ist das?

Scans prüfen, welche Geräte im gleichen Netz erreichbar sind und ob sie Hostnamen haben.

### Wofür nutzen?

* Geräte im LAN identifizieren.
* Hostnamen ermitteln (DNS, mDNS, NetBIOS).
* Sicherheit prüfen (unerwartete Geräte finden).

### Befehle

```bash
sudo nmap -sn 192.168.178.0/24 --system-dns
avahi-browse -a
nbtscan 192.168.178.0/24
```

### Typische Fehler

* Aggressive Scans → Sicherheitssoftware oder Geräte blockieren dich.
* Hostname nicht auflösbar → kein DNS/mDNS/NetBIOS aktiv.

---

## 5. Ports & Dienste

### Was ist das?

Ports sind die „Türnummern“ für Anwendungen im Netzwerk. Offene Ports zeigen, welche Dienste erreichbar sind.

### Wofür nutzen?

* Prüfen, ob ein Dienst läuft und erreichbar ist.
* Sicherheitstest auf offenen Ports.
* Fehlersuche bei blockierten Anwendungen.

### Befehle

```bash
sudo nmap -Pn 192.168.178.20
sudo ss -tulpen
```

### Typische Fehler

* Unerwartete offene Ports → Sicherheitsrisiko.
* Notwendige Ports blockiert → Dienst nicht erreichbar.

---

## 6. Performance & Fehleranalyse

### Was ist das?

Misst, ob Pakete ankommen, wie schnell sie ankommen, und ob unterwegs Verluste passieren.

### Wofür nutzen?

* Verbindungslatenz messen.
* Paketverluste lokalisieren.
* Routing-Engpässe erkennen.

### Befehle

```bash
ping -c 4 192.168.178.1
mtr 1.1.1.1
```

### Typische Fehler

* Hohe Latenz im lokalen Netz → WLAN-Störungen oder Kabelproblem.
* Paketverlust nur außerhalb → Problem beim Provider oder Routing.

---

## 7. WLAN-spezifisch

### Was ist das?

Zeigt Details zu deiner Funkverbindung: Signalstärke, Bitrate, Retries, verlorene Frames.

### Wofür nutzen?

* WLAN-Qualität prüfen.
* Kanal-Interferenzen erkennen.
* Gründe für niedrige Geschwindigkeit finden.

### Befehle

```bash
iw dev wlp0s20f3 link
iw dev wlp0s20f3 station dump
```

### Typische Fehler

* Signal zu schwach → Standort ändern oder Repeater einsetzen.
* Hohe Retries → Kanalstörungen, Wechsel des WLAN-Kanals nötig.

