---
title: nmap – Netzwerkscanner
date: 20251005
author: realcaptainsolaris
---

# nmap – Netzwerk- und Portscanner

**`nmap`** („Network Mapper“) ist das Standardwerkzeug zur **Erkennung von Hosts, offenen Ports, Diensten und Betriebssystemen** in Netzwerken. Es kombiniert ICMP-, TCP- und UDP-Scans und kann von einfachen Ping-Tests bis zu detaillierten Service-Analysen eingesetzt werden.

---

## Grundlegender Hostscan (Ping)

Testet, ob ein Host erreichbar ist:

    nmap 192.168.0.1

### Beispielausgabe:

```

Starting Nmap 7.94 ( [https://nmap.org](https://nmap.org) ) at 2025-10-05 12:34 CEST
Nmap scan report for 192.168.0.1
Host is up (0.0031s latency).
Not shown: 997 closed tcp ports
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https

```

**Interpretation:**

| Spalte  | Bedeutung                          |
|---------|------------------------------------|
| PORT    | Portnummer / Protokoll            |
| STATE   | Zustand (`open`, `closed`, `filtered`) |
| SERVICE | erkannter Dienstname              |

---

## Netzwerkscan – Alle Hosts im Subnetz finden

Scannt ein ganzes Netz (z. B. `/24` für 256 Hosts):

    nmap -sn 192.168.0.0/24

Nur Host-Erreichbarkeit („Ping-Sweep“):

```

Nmap scan report for 192.168.0.1
Host is up (0.0021s latency).
Nmap scan report for 192.168.0.42
Host is up (0.0009s latency).

```

---

## Detaillierter Service-Scan

Ermittelt offene Ports **und** den Dienst inkl. Version:

    nmap -sV 192.168.0.42

### Beispielausgabe:

```

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.3
80/tcp   open  http    Apache httpd 2.4.52
443/tcp  open  ssl/https OpenSSL 1.1.1f

```

`-sV` aktiviert die **Versionserkennung** der Dienste.

---

## Betriebssystemerkennung

Versucht, das Betriebssystem des Ziels zu identifizieren:

    sudo nmap -O 192.168.0.42

### Beispielausgabe:

```

OS details: Linux 5.15 - 5.17, Ubuntu 22.04 LTS
Network Distance: 1 hop

```

---

## Alle Ports scannen

Standardmäßig prüft `nmap` nur die 1000 wichtigsten Ports. Für **alle 65535 Ports**:

    nmap -p- 192.168.0.42

Oder nur bestimmte Ports:

    nmap -p 22,80,443 192.168.0.42

---

## Scan mehrerer Hosts gleichzeitig

    nmap 192.168.0.1 192.168.0.42 192.168.0.100

Oder mit Wildcards:

    nmap 192.168.0.*

Oder ganze Netze:

    nmap 192.168.0.0/24

---

## UDP-Scan (langsamer, aber wichtig)

    sudo nmap -sU 192.168.0.42

Zeigt offene UDP-Dienste wie DNS (53) oder NTP (123).

---

## Stealth-Scan (SYN-Scan)

Standard-Scan-Typ für schnelle und „leise“ Scans:

    sudo nmap -sS 192.168.0.42

Sendet nur SYN-Pakete, ohne eine vollständige TCP-Verbindung aufzubauen.

---

## Kombinierte Scans (Praxisbeispiel)

Ein sehr informativer Scan, der Ports, Dienste, OS und Skripte kombiniert:

    sudo nmap -A 192.168.0.42

- `-A` = Aggressiver Modus (Versionserkennung, OS-Erkennung, Skripte, Traceroute)

---

## Beispiele für Zustände (`STATE`)

| Zustand      | Bedeutung                                                      |
|--------------|----------------------------------------------------------------|
| open         | Port antwortet aktiv und nimmt Verbindungen an                |
| closed       | Port antwortet, nimmt aber keine Verbindungen an              |
| filtered     | Keine Antwort → evtl. Firewall                                |
| unfiltered   | Antwort erhalten, aber Zustand nicht klar                     |
| open|filtered | Port offen **oder** gefiltert – nicht eindeutig bestimmbar  |

---

## Typische Analyse-Workflows

| Ziel                                   | Befehl                                   |
|----------------------------------------|------------------------------------------|
| Host erreichbar?                       | `nmap -sn 192.168.0.1`                  |
| Offene Ports anzeigen                  | `nmap 192.168.0.1`                      |
| Dienste und Versionen ermitteln       | `nmap -sV 192.168.0.1`                  |
| Betriebssystem erkennen               | `sudo nmap -O 192.168.0.1`              |
| Alle Ports scannen                     | `nmap -p- 192.168.0.1`                  |
| UDP-Dienste prüfen                     | `sudo nmap -sU 192.168.0.1`             |
| Komplettanalyse                        | `sudo nmap -A 192.168.0.1`              |

---

## Sicherheitshinweis

- **Nur Systeme scannen, für die du berechtigt bist.**  
  Unautorisierte Scans können rechtlich problematisch sein.
- Viele Firewalls erkennen oder blockieren Nmap-Scans – Ergebnisse können unvollständig sein.

---

## Vergleich: `ss` vs. `nmap`

| Tool    | Perspektive           | Funktion                                               |
|---------|-----------------------|--------------------------------------------------------|
| `ss`    | lokal                 | Zeigt **lokale** offene Ports und Verbindungen        |
| `nmap`  | remote + lokal        | Scannt **lokal und remote** auf offene Ports und Dienste |

