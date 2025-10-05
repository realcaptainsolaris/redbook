---
title: nmcli – NetworkManager CLI
date: 20251005
author: realcaptainsolaris
---

# nmcli – WLAN-Verwaltung und Diagnose

**`nmcli`** ist das Kommandozeilenwerkzeug für den **NetworkManager**. Es ermöglicht das **Auflisten, Verbinden, Trennen und Diagnostizieren** von Netzwerken – ohne grafische Oberfläche.

---

## Aktive Verbindung prüfen

Zeigt den aktuellen Verbindungsstatus und alle aktiven Schnittstellen:

    nmcli device status

### Beispielausgabe:

```

DEVICE          TYPE      STATE         CONNECTION
wlp0s20f3       wifi      connected     Heimnetz_5G
enp0s31f6       ethernet  disconnected  --
lo              loopback  unmanaged     --

```

**Interpretation:**

| Spalte  | Bedeutung                                           |
|---------|-----------------------------------------------------|
| DEVICE  | Name der Netzwerkschnittstelle                      |
| TYPE    | Typ (wifi, ethernet, loopback, …)                  |
| STATE   | Verbindungsstatus                                  |
| CONNECTION | Name der aktiven Verbindung oder `--` wenn keine |

---

## Detaillierte Verbindung anzeigen

Zeigt Details zur aktuellen WLAN-Verbindung, inkl. Signal, Band, Frequenz, TX/RX usw.:

    nmcli device wifi show-ifname wlp0s20f3

oder klassisch:

    nmcli -f all device show wlp0s20f3

### Beispielausgabe:

```

GENERAL.DEVICE:                         wlp0s20f3
GENERAL.TYPE:                           wifi
GENERAL.STATE:                          100 (connected)
GENERAL.CONNECTION:                     Heimnetz_5G
IP4.ADDRESS[1]:                         192.168.0.42/24
IP4.GATEWAY:                            192.168.0.1
IP4.DNS[1]:                             192.168.0.1
WI-FI.PHY:                              wlan0
WI-FI.SSID:                             Heimnetz_5G
WI-FI.BSSID:                            98:da:c4:12:ab:cd
WI-FI.MODE:                             infrastructure
WI-FI.FREQUENCY:                        5180 MHz
WI-FI.RATE:                             866.7 MBit/s
WI-FI.SIGNAL:                           70
WI-FI.SECURITY:                         WPA2

```

**Wichtige Felder:**

| Feld             | Bedeutung                                               |
|------------------|---------------------------------------------------------|
| SSID             | WLAN-Name                                              |
| BSSID            | MAC-Adresse des AP                                     |
| FREQUENCY        | Frequenz → bestimmt Band (2.4 GHz / 5 GHz)             |
| RATE             | aktuelle Bitrate                                       |
| SIGNAL           | Signalqualität (0–100 %)                               |
| SECURITY         | Verschlüsselungsstandard                               |

---

## WLAN-Netze scannen

Scannt und zeigt alle verfügbaren WLANs:

    nmcli device wifi list

### Beispielausgabe:

```

IN-USE  SSID          MODE   CHAN  RATE        SIGNAL  BARS  SECURITY

* ```
    Heimnetz_5G   Infra  36    866 Mbit/s  70      ▂▄▆_  WPA2
    Gastnetz      Infra  1     54 Mbit/s   42      ▂▄__  WPA2
    WLAN-Cafe     Infra  11    72 Mbit/s   55      ▂▄▆_  WPA2
  ```

```

**Spalten erklärt:**

| Spalte    | Bedeutung                                         |
|-----------|---------------------------------------------------|
| IN-USE    | `*` wenn aktuell verbunden                        |
| SSID      | Netzwerkname                                     |
| CHAN      | Kanalnummer                                      |
| RATE      | maximale Bitrate                                 |
| SIGNAL    | Signalqualität (0–100)                           |
| SECURITY  | Verschlüsselungsstandard                         |

---

## WLAN verbinden

Mit einem Netzwerk verbinden (interaktiv nach Passwort fragen lassen):

    nmcli device wifi connect "Heimnetz_5G"

Oder Passwort direkt mitgeben:

    nmcli device wifi connect "Heimnetz_5G" password "meinpasswort"

---

## Verbindung trennen

    nmcli device disconnect wlp0s20f3

---

## Nützliche Kommandos im Alltag

| Ziel                                | Befehl                                                           |
|------------------------------------|------------------------------------------------------------------|
| Alle Geräte auflisten              | `nmcli device`                                                  |
| WLAN-Netze scannen                 | `nmcli device wifi list`                                        |
| Verbindung herstellen              | `nmcli device wifi connect "SSID"`                              |
| Aktive Verbindung anzeigen         | `nmcli device status`                                           |
| Detaillierte Infos zur Verbindung  | `nmcli device show wlp0s20f3`                                   |
| Schnittstelle neu verbinden        | `nmcli device reapply wlp0s20f3`                                |

---

## Vergleich: `iw` vs. `nmcli`

| Tool     | Aufgabe                                     | Zugriffsebene             |
|----------|--------------------------------------------|---------------------------|
| `iw`     | Kernel-nahe Diagnose und Statusinfos       | Low-Level (`nl80211`)    |
| `nmcli`  | Netzwerkverwaltung + Status + Verbindung   | High-Level (NetworkManager) |

Beide Tools ergänzen sich:  
`iw` für detaillierte physikalische Infos, `nmcli` für Verwaltung und Verbindungssteuerung.
