---
title: tmux
date: 20231111
author: realcaptainsolaris
---

# tmux

### **tmux Befehle – Übersicht**

| **Aktion**                       | **Befehl**                                                       | **Tastenkürzel / Hinweise**                  |
| -------------------------------- | ---------------------------------------------------------------- | -------------------------------------------- |
| **Server beenden**               | `tmux kill-server`                                               | Zerstört alle Sessions                       |
| **Neue Session starten**         | `tmux new -s <NAME>`                                             | Erstelle eine neue Session mit Namen         |
| **Session laden / verbinden**    | `tmux attach -t <NAME>`                                          | Verbindung zu einer bestehenden Session      |
|                                  | `tmux attach -t -1`                                              | Letzte Session laden                         |
| **Session umbenennen**           | `tmux rename-session -t -1 <NEUERNAME>`                          | Session einen neuen Namen geben              |
| **Session zerstören**            | `tmux kill-session -t <NAME>`                                    | Spezifische Session beenden                  |
| **Session-Übersicht anzeigen**   | `Ctrl + b` `w`                                                   | Alle Sessions und Fenster anzeigen           |
| **Von Session trennen**          | `Ctrl + b` `d`                                                   | Detach von der aktuellen Session             |
| **Neues Fenster erstellen**      | `Ctrl + b` `c`                                                   | Neues Window erstellen                       |
| **Fenster umbenennen**           | `Ctrl + b` `,`                                                   | Aktuelles Fenster umbenennen                 |
| **Fenster schließen**            | `Ctrl + b` `x`                                                   | Aktuelles Fenster schließen                  |
| **Zu einem Fenster springen**    | `Ctrl + b` `0`                                                   | Zu Fenster Nr. 1 wechseln                    |
| **Verticaler Split erstellen**   | `Ctrl + b` `"`                                                   | Pane vertikal splitten                       |
| **Horizontaler Split erstellen** | `Ctrl + b` `%`                                                   | Pane horizontal splitten                     |
| **Zwischen Panes wechseln**      | `Ctrl + b` + `h`, `l`, `k`, `j`                                  | Zwischen Panes (links, rechts, hoch, runter) |
| **Tmux Resurrect – speichern**   | `Ctrl + b` `Ctrl + s`                                            | Speichert aktuelle Session                   |
| **Tmux Resurrect – laden**       | `Ctrl + b` `Ctrl + r`                                            | Lädt gespeicherte Session                    |
| **Tmux Plugin Manager (TPM)**    | [tmux-plugins/tpm](https://github.com/tmux-plugins/tpm)          | Plugin Manager für tmux                      |
| **Tmux Resurrect Plugin**        | [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) | Session speichern und wiederherstellen       |
