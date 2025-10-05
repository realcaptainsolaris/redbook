---
title: ip – Netzwerk-Interfaces, Routing und Nachbarn
date: 20251005
author: realcaptainsolaris
---

# ip – zentrales Netzwerk-Tool unter Linux

**`ip`** ist das moderne Standardwerkzeug zur Verwaltung von **Netzwerkinterfaces, IP-Adressen, Routen, ARP/Nachbarn und Regeln**. Es ersetzt die alten Tools `ifconfig`, `route`, `arp` und `netstat` weitgehend und bietet ein einheitliches Interface.

---

## Interfaces anzeigen

Listet alle Netzwerkinterfaces und ihre IP-Adressen:

    ip addr

Kurzform:

    ip a

### Beispielausgabe:

```

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
inet 192.168.0.42/24 brd 192.168.0.255 scope global dynamic enp0s3
valid_lft 86395sec preferred_lft 86395sec
inet6 fe80::a00:27ff:fe4e:66a1/64 scope link
valid_lft forever preferred_lft forever

```

**Interpretation:**

| Feld | Bedeutung |
|------|-----------|
| `state UP` | Interface aktiv |
| `inet` | IPv4-Adresse / Präfix |
| `inet6` | IPv6-Adresse |
| `mtu` | maximale Paketgröße |
| `qlen` | Queue-Länge |

oder die Kurzverison 

    ip -br a


---

## IP-Adresse hinzufügen oder entfernen

Adresse hinzufügen:

    sudo ip addr add 192.168.0.50/24 dev enp0s3

Adresse entfernen:

    sudo ip addr del 192.168.0.50/24 dev enp0s3

---

## Interfaces aktivieren/deaktivieren

Interface aktivieren:

    sudo ip link set dev enp0s3 up

Interface deaktivieren:

    sudo ip link set dev enp0s3 down

---

## Routingtabelle anzeigen

Zeigt aktuelle IPv4-Routen:

    ip route

Beispiel:

```

default via 192.168.0.1 dev enp0s3 proto dhcp metric 100
192.168.0.0/24 dev enp0s3 proto kernel scope link src 192.168.0.42

```

| Feld | Bedeutung |
|------|-----------|
| `default via` | Standardgateway |
| `dev` | Interface |
| `src` | Quelladresse |

---

## Route hinzufügen oder löschen

Route hinzufügen:

    sudo ip route add 10.0.0.0/24 via 192.168.0.1

Route löschen:

    sudo ip route del 10.0.0.0/24

---

## Nachbartabelle (ARP) anzeigen

    ip neigh

Beispiel:

```

192.168.0.1 dev enp0s3 lladdr 08:00:27:11:22:33 REACHABLE

```

| Feld | Bedeutung |
|------|-----------|
| `lladdr` | MAC-Adresse des Nachbarn |
| `REACHABLE` | ARP-Eintrag ist aktuell gültig |

---

## Nachbarn löschen oder hinzufügen

Eintrag löschen:

    sudo ip neigh del 192.168.0.1 dev enp0s3

Manuell hinzufügen:

    sudo ip neigh add 192.168.0.1 lladdr 08:00:27:11:22:33 dev enp0s3

---

## IP-Routen zu Hosts testen

Mit `ip route get` kann man den Pfad zu einem Ziel analysieren:

    ip route get 8.8.8.8

Beispielausgabe:

```

8.8.8.8 via 192.168.0.1 dev enp0s3 src 192.168.0.42 uid 1000
cache

```

---

## Interfaces kurz anzeigen (ohne IPs)

    ip link

Beispiel:

```

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

```

---

## Typische Praxisbefehle

| Ziel | Befehl |
|------|--------|
| Interfaces mit IPs anzeigen | `ip addr` |
| Interface aktivieren/deaktivieren | `ip link set dev enp0s3 up/down` |
| Neue IP-Adresse setzen | `ip addr add 192.168.0.50/24 dev enp0s3` |
| Routingtabelle anzeigen | `ip route` |
| Neue Route hinzufügen | `ip route add 10.0.0.0/24 via 192.168.0.1` |
| ARP-Tabelle anzeigen | `ip neigh` |
| Pfad zu Host prüfen | `ip route get 8.8.8.8` |

---

## Vergleich: `ifconfig` vs. `ip`

| Tool | Status | Funktion |
|------|--------|----------|
| `ifconfig` | veraltet | Nur Interfaces und IPs verwalten |
| `ip` | modern | Interfaces, Routen, ARP, Regeln – alles in einem Tool |

---

## Tipp

- Die meisten Befehle funktionieren auch **ohne root**, wenn sie nur lesend sind.
- Schreibende Aktionen (`add`, `del`, `set`) erfordern meist `sudo`.

