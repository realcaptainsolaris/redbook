---
title: tmux 
date: 20231111
author: realcaptainsolaris 
---

# tmux 

## tmux Kill Server
Tmux kill server und alle Sessons zerstören (kann resurrectet werden)

    tmux kill-server 


## neue Session

    tmux new -s <NAME>

## Session laden:

    tmux attach -t -1
    tmux attach -t clox

## Session umbenennen:
    
    tmux rename-sessiong -t -1 <NEUERNAME>

## Session zerstören 
  
    tmux kill-session -t <NAME>

## Session übersicht
    
    ctrl + w w => zeigt alle Sessions und Fenster
    ctrl + w d => detach from session

## Fenster

    ctrl + w c => neues Window
    ctrl + w , => Fenster umbennen
    Ctrl + w + x => Fenster schliessen (kill)

### von Fenster zu Fenster gehen:
    ctrl + w 0 => zu fenster nummer 1 gehen

## RESURRECT
    
    ctrl + w ctrl + R => Resurrect
    ctrl + w ctrl + S => Save

## PANES

    ctrl + w " => vertikaler split
    ctrl + w % => horizontaler split
    ctrl + w lhki => panes wechseln


### tmux Plugin Manager

    https://github.com/tmux-plugins/tpm


## tmux Resurrect

    https://github.com/tmux-plugins/tmux-resurrect
