---
title: iw – Wireless CLI
date: 20251005
author: realcaptainsolaris
---

# iw – WLAN-Informationen und Diagnose

Das Tool **`iw`** ist das moderne Kommandozeilenwerkzeug zur Abfrage und Konfiguration von WLAN-Schnittstellen unter Linux. Es nutzt die `nl80211`-Schnittstelle des Kernels und ersetzt ältere Tools wie `iwconfig`.

## Aktive WLAN-Verbindung anzeigen

Zeigt Informationen zur aktuellen WLAN-Verbindung einer Schnittstelle:

    iw dev wlp0s20f3 link

### Beispielausgabe:

```

Connected to 98:da:c4:12:ab:cd (on wlp0s20f3)
SSID: Heimnetz_5G
freq: 5180
RX:  135847 bytes (1234 packets)
TX:  98572 bytes (876 packets)
signal: -52 dBm
tx bitrate: 866.7 MBit/s VHT-MCS9 80MHz short GI
bss flags:      short-slot-time
dtim period:    2
beacon int:     100

```

**Interpretation:**

| Feld             | Bedeutung                                                                 |
|------------------|---------------------------------------------------------------------------|
| SSID             | Name des verbundenen WLAN-Netzes                                          |
| freq             | Frequenz in MHz – bestimmt das Band (2,4 GHz ~ 2400, 5 GHz ~ 5000)       |
| RX / TX          | Empfangene und gesendete Daten                                           |
| signal           | Empfangsstärke in dBm (näher bei 0 = besser)                             |
| tx bitrate       | Aktuelle Sende­rate                                                      |
| beacon int       | Beacon-Intervall (Zeit zwischen Management-Frames)                       |

---

## Alle verfügbaren Netzwerke scannen

Scannt alle sichtbaren WLANs in Reichweite:

    sudo iw dev wlp0s20f3 scan

(Erfordert Root-Rechte.)

### Beispielausgabe (gekürzt):

```

BSS 98:da:c4:12:ab:cd(on wlp0s20f3)
SSID: Heimnetz_5G
freq: 5180
signal: -52.00 dBm
capabilities: ESS (Short Slot Time)
rates: 6.0 9.0 12.0 18.0 24.0 36.0 48.0 54.0
BSS 3c:84:6a:98:ef:22(on wlp0s20f3)
SSID: Gastnetz
freq: 2412
signal: -68.00 dBm
capabilities: ESS Privacy ShortSlotTime
rates: 1.0 2.0 5.5 11.0 6.0 12.0 24.0 36.0

```

**Wichtige Felder:**

| Feld          | Bedeutung                                                                  |
|---------------|----------------------------------------------------------------------------|
| BSS           | MAC-Adresse des Access Points                                              |
| SSID          | Name des WLANs                                                            |
| freq          | Frequenz / Band                                                           |
| signal        | Empfangsstärke                                                            |
| capabilities  | Eigenschaften (z.B. Verschlüsselung, Short Slot Time)                     |
| rates         | Unterstützte Übertragungsraten                                           |

---

## Weitere nützliche Befehle

### Liste aller WLAN-Interfaces

    iw dev

Beispiel:

```

phy#0
Interface wlp0s20f3
ifindex 3
wdev 0x1
addr 12:34:56:78:9a:bc
type managed
txpower 22.00 dBm

```

### Kanal und Frequenz einer Schnittstelle setzen

    sudo iw dev wlp0s20f3 set channel 36

---

## Typische Analyse-Workflows

1. **Verbindung prüfen:**  
   `iw dev wlp0s20f3 link`

2. **Signalstärke und Bitrate beobachten:**  
   `watch -n 2 iw dev wlp0s20f3 link`

3. **Netzwerke in Reichweite analysieren:**  
   `sudo iw dev wlp0s20f3 scan | grep -E "SSID|signal|freq"`

---

## Hinweise

- `iw` ist rein lesend und steuernd auf Kernel-Ebene. Für Netzwerkkonfigurationen (z. B. Verbindung herstellen) ist `nmcli` oder `wpa_supplicant` zuständig.
- Für eine kontinuierliche Überwachung kann `watch` oder `grep` kombiniert werden.

