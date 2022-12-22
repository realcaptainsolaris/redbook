# Systeminformationen beim Booten

## dmesg: Kernelinformationen und Fehler:
    
    dmesg

nach Fehler filtern:

    dmesg | grep -i error

## jourcnalct: systemd Journal anfragen

Kernelinformationen mit -k

    journalctl -k
