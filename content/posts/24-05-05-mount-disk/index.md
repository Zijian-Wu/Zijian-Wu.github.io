---
title: "Mount New Hard Drive(>2T)"
description: "Some often used Command Lines' Record."
date: 2024-05-05
tags: ["tools"]
author: "Me"
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
disableHLJS: true
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "2.jpg"
    caption: "mizore"
---

## 1. Check disk name:

try these commands in shell:

`df -h`

`lsblk`

`sudo fdisk -l`

find the disk device name like: `/dev/sdc: 3.64 TiB` for 4T Disk

## 2. Partition the Hard Drive

for disk capacity > 2T: we use `parted` to create partitions on the new hard drive 

```bash
sudo parted /dev/sdX
(parted) mklabel gpt  # Choose the partition table type (e.g., GPT)
(parted) mkpart primary 0% -1  # Create a primary partition using all available space
(parted) quit
```

Replace `/dev/sdX` with your new hard drive's name(e.g., `/dev/sdc`)

## 3. Format the Partition

```bash
sudo mkfs --type ext4 /dev/sdXY
```

Replace `/dev/sdXY`with the identifier of your partition(e.g., `/dev/sdc1`)

## 4. Mount the Partition

```bash
sudo mkdir /mnt/mydrive
sudo mount /dev/sdXY /mnt/mydrive
```

or find `Disks` app in your PC, and mount the partition with GUI in `Disks`

## 5. Umount the Partition

```bash
sudo umount /dev/sdXY
```

### End
