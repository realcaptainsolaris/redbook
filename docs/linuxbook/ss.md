---
title: ss – Socket Statistics
date: 20251005
author: realcaptainsolaris
---

# ss – Netzwerkverbindungen und Sockets anzeigen

**`ss`** („socket statistics“) ist das moderne Werkzeug zur Analyse von Netzwerkverbindungen und ersetzt `netstat`.  
Es zeigt TCP-, UDP-, UNIX- und RAW-Sockets sowie deren Zustände, Ports, Prozesse und Statistiken.

---

## Alle offenen TCP-Verbindungen anzeigen

    ss -t

### Beispielausgabe:

```

State      Recv-Q Send-Q Local Address:Port   Peer Address:Port  Process
ESTAB      0      0      192.168.0.42:53732   142.250.185.36:https
ESTAB      0      0      192.168.0.42:41234   93.184.216.34:http

```

**Felder:**

| Feld              | Bedeutung                                    |
|-------------------|----------------------------------------------|
| State            | Verbindungsstatus (z.B. `ESTAB` = established) |
| Recv-Q / Send-Q   | Empfangs- / Sendewarteschlange (Bytes)       |
| Local Address:Port | lokale IP und Port                         |
| Peer Address:Port  | entfernte IP und Port                      |
| Process           | zugehöriger Prozess (optional, siehe unten) |

---

## Prozesse zu Verbindungen anzeigen

    sudo ss -t -p

```

State  Recv-Q Send-Q Local Address:Port  Peer Address:Port  Process
ESTAB  0      0      192.168.0.42:53732  142.250.185.36:https users:(("firefox",pid=2345,fd=72))

```

Jetzt siehst du, **welcher Prozess** eine Verbindung nutzt.

---

## Alle offenen UDP-Sockets anzeigen

    ss -u

Beispiel:

```

State   Recv-Q Send-Q Local Address:Port  Peer Address:Port
UNCONN  0      0      0.0.0.0:68          0.0.0.0:*

```

UDP ist verbindungslos (`UNCONN`), wird häufig für DNS oder DHCP verwendet.

---

## Alle offenen Sockets (TCP, UDP, UNIX)

    ss -a

- `-a` = all – zeigt auch `LISTEN` und `UNCONN`
- Ohne Filter → alle Protokolle

---

## Nur lausche Sockets (Serverports) anzeigen

    ss -tln

- `-t` = TCP  
- `-l` = listen  
- `-n` = numerische Ausgabe (keine DNS-Auflösung)

### Beispielausgabe:

```

State  Recv-Q Send-Q Local Address:Port  Peer Address:Port
LISTEN 0      128    0.0.0.0:22          0.0.0.0:*
LISTEN 0      100    127.0.0.1:631       0.0.0.0:*

```

Hier lauscht z. B. der **SSH-Dienst auf Port 22**.

---

## Verbindung nach Zustand filtern

    ss -t state established

Nur aktive TCP-Verbindungen:

```

State  Recv-Q Send-Q Local Address:Port   Peer Address:Port
ESTAB  0      0      192.168.0.42:53732   142.250.185.36:https

```

Weitere wichtige Zustände:
- `LISTEN` – Server wartet auf Verbindung  
- `SYN-SENT` – Verbindungsaufbau ausgehend  
- `SYN-RECV` – Verbindungsaufbau eingehend  
- `ESTAB` – Verbindung steht  
- `TIME-WAIT` / `CLOSE-WAIT` – Abbauphase  

---

## Netzwerkstatistiken anzeigen

    ss -s

### Beispielausgabe:

```

Total: 180 (kernel 190)
TCP:   25 (estab 4, closed 15, orphaned 0, synrecv 0, timewait 13)

Transport Total     IP        IPv6

* ```
      190       -         -
  ```

RAW       0         0         0
UDP       5         5         0
TCP       25        25        0

```

Zeigt einen Überblick über alle Socket-Typen und Zustände.

---

## Typische Analyse-Workflows

| Ziel                                        | Befehl                                    |
|--------------------------------------------|-------------------------------------------|
| Aktive TCP-Verbindungen                     | `ss -t`                                   |
| Verbindungen mit Prozessen                 | `sudo ss -t -p`                           |
| Lausche Ports (Server) anzeigen            | `ss -tln`                                 |
| UDP-Sockets                                | `ss -u`                                   |
| Nur `ESTABLISHED` TCP-Verbindungen         | `ss -t state established`                 |
| Socket-Statistik                           | `ss -s`                                   |

---

## Vergleich: `ss` vs. `netstat`

| Tool       | Status         | Vorteile                                                   |
|------------|----------------|------------------------------------------------------------|
| `netstat`  | veraltet       | Kompatibilität                                             |
| `ss`       | empfohlen      | Schneller, moderner, mehr Filteroptionen, IPv6-Unterstützung |

---

## Hinweis

- Für Prozessinformationen ist meist **Root-Recht** nötig (`sudo`).
- In Skripten oder Monitoring-Tools ist `ss` schneller und zuverlässiger als `netstat`.

