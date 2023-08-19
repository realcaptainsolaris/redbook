---
title: Permissions
date: 20230126
author: realcaptainsolaris 
---

# Permissions 

## Show permissions

    ls -l

    -rw-rw-r--  1 bob solaris    30 Feb 25 17:42 pyproject.toml

1. d => if directory

## Permissions
- Owner
- Group
- all others

### User bob
- r => Read SET
- w => Write SET
- x => Execute NOT SET

user bob can open and write pyproject.toml

    id
    uid=1000(bob) gid=1000(solaris) Gruppen=1000(solaris),4(adm),24(cdrom),27(sudo)

### Group solaris 
- r => Read SET
- w => Write SET
- x => Execute

User alice, which is member of group solaris, can open and write pyproject.toml


## chmod Change File Permissions


    -rw-rw-r--  1 bob solaris    30 Feb 25 17:42 pyproject.toml

- r = 4
- w = 2
- x = 1

Bits jeder Gruppe (User, Gruppe, world)immer zusammenzählen

- 1. Gruppe (User): 4 + 2 = 6
- 2. Gruppe (Group): 4 + 2 = 6
- 3. Gruppe (world): 4 + 0 + 0 = 0

Neue Gruppe, nur schreibbar für User

- 1. Gruppe: 4 + 2 = 6
- 2. Gruppe: 4 + 0 = 4
- 3. Gruppe: 4 + 0 = 4

    chmod 644 pyproject.toml 

oder in der folgenden Schreibweise:

    chmod u=rwx,g=r,o=r pyproject.toml

## Sticky Bit

Das "Sticky Bit" ist ein spezielles Berechtigungsattribut in Unix-basierten
Betriebssystemen wie Linux. Es wird normalerweise auf Verzeichnissen angewendet
und hat eine besondere Bedeutung in Bezug auf die Dateizugriffsrechte.

Wenn das Sticky Bit auf einem Verzeichnis gesetzt ist, bedeutet dies, dass nur
der Eigentümer einer Datei (oder das Root-Konto) Dateien in diesem Verzeichnis
löschen kann, selbst wenn andere Benutzer Schreibrechte in diesem Verzeichnis
haben. Mit anderen Worten, das Sticky Bit verhindert, dass Benutzer Dateien
löschen, die sie nicht selbst erstellt haben, selbst wenn sie Schreibzugriff
auf das Verzeichnis haben.

    ls -l / | grep tmp

    drwxrwxrwt  25 root root      12288 Aug 13 17:05 tmp

t = Sticky Bit

### Sticky Bit setzen

    chmod +t verzeichnisname

### Sticky Bit deaktivieren

    chmod -t verzeichnisname

## SETUI (Set user id)
setuid (Set User ID) is a special permission in Unix-like operating systems
that allows a user to execute a program with the permissions of the owner of
the program, rather than with their own permissions. This can be extremely
powerful and useful in certain scenarios, but it also introduces security
concerns if not used carefully.

When the setuid permission is set on an executable file, the program that is executed gains the same privileges as the owner of the file, even if the person executing the program does not have those privileges. This is particularly relevant for programs that require elevated privileges to perform certain tasks, such as system maintenance or administration.

    chmod +s filename

And to remove the setuid permission:

    chmod -s filename

## SETGID

Set Group ID, which is another special permission in Unix-like operating
systems, similar to setuid but for groups.

When the setgid permission is set on an executable file or a directory, any
process or program executed within that context will inherit the group
ownership of the parent directory, rather than the group ownership of the user
who launched the process. This can be useful in scenarios where multiple users
need to collaborate on files within a common group.

For example, consider a directory called shared_files that is owned by a group called project_team. If the setgid permission is set on shared_files, any new files or directories created within shared_files will inherit the project_team group ownership, regardless of who created them. This ensures that all members of the project_team group have access to the files.


## CHOWN
Eigentümer oder Gruppe ändern. Muss immer mit sudo-Rechten ausgeführt werden.

### change owner

    sudo chown user:gruppe test.py

### change only owner

    sudo chown user: test.py

### change only group

    sudo chown :neuegruppe test.py

### Change directory

    sudo chown -R user:gruppe directory

## chgrp Gruppe ändern

Als Alternative zu chown kann man auch die Gruppe ändern mit chgrp.

    sudo chgrp -R groupname directory

## umask
umask is a Unix command that stands for "user file creation mask." It is used
to control the default permissions that are assigned to newly created files and
directories in a Unix-like operating system.

When a new file or directory is created, it is assigned permissions based on
the umask value. The umask value specifies which permission bits should be
turned off from the maximum permission settings. In other words, it sets the
permission bits that are not allowed when creating new files and directories.

The umask value consists of three octal digits (0-7), each representing the permissions that are turned off for the owner, group, and others. Each digit corresponds to read (4), write (2), and execute (1) permissions. Subtracting the umask value from the maximum permission settings (usually 666 for files and 777 for directories) gives you the default permission settings for newly created files and directories.

If the umask is set to 022, it means the write permission is turned off for
group and others. New files would be created with permissions 644 (666 - 022)
- read and write for the owner, and read-only for group and others.  

If the umask is set to 027, it means the write permission is turned off for group, and
both write and execute permissions are turned off for others. New files would
be created with permissions 640 (666 - 027) - read and write for the owner, and
read-only for group and others.

### get current value of umask

    umask 

### set umask

    umask 022

Unter Debian findet sich die Standard-Einstellung hier:

    cat /etc/login.defs | less
