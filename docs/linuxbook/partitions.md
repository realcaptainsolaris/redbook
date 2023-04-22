---
title: Partitions
date: 20230126
author: realcaptainsolaris 
---

# Filesystems 

- ext2
- ext3: journaling function (save metadata im journaling system)
- ext4: RAM Cash
- xfs: Journaling and high speed
- vfat: Windows Filesystem
- exFat: Flash Memory
- btrfs: big memory, copy on write, Railsystem, btrfs-convert tool


## fdisk 
Program to do partitioning

List partitions:

    fdisk -l 

## mkfs
Create file system

    sudo mkfs.ext4 -j /dev/sdb1

## mkswap
Create swap file system

    sudo mkswap /dev/sdb1

add Swap-Partition to filesystem

    sudo swapon /dev/sdb1

## gdisk
Alternative to fdisk

    sudo gdisk /dev/sdc

## parted

    sudo parteled -l



