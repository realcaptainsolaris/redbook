---
title: Postgres Database 
date: 20220902
author: realcaptainsolaris 
---

## Basic psql Commands

### connect to db inside docker container -w to DB postgres

docker exec -it dbname psql -U postgresuser -w postgres

### List all databases

    \l

### Switch to a database

    \c postgres

### List all tables of current database


    \dt

### List all Users

    \du

### List all Schemas

    \dn

### Descripe a table

    \d tablename


### Show History

    \s

### Save Query results to file

    \o home/myhome/filename.txt

now query, what you need. Output will be written to filename.txt

    \o

Output to screen again.




