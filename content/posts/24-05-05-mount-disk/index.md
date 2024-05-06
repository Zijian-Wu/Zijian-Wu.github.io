---
title: "Mount Disk(>2T)"
date: 2024-05-05
# weight: 1
# aliases: ["/first"]
tags: ["first"]
author: "Me"
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
description: "Post Description."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true
disableShare: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/Zijian-Wu/Zijian-Wu.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## Check disk name:

try these commands in shell:

`df -h`

`lsblk`

`sudo fdisk -l`

find the disk device name like: `/dev/sdc: 3.64 TiB` for 4T Disk

## Partition the Hard Drive

for disk capacity > 2T: we use `parted` to create partitions on the new hard drive 

```bash
sudo parted /dev/sdX
(parted) mklabel gpt  # Choose the partition table type (e.g., GPT)
(parted) mkpart primary 0% -1  # Create a primary partition using all available space
(parted) quit
```

Replace `/dev/sdX` with your new hard drive's name(e.g., `/dev/sdc`)

## Format the Partition

```bash
sudo mkfs --type ext4 /dev/sdXY
```

Replace `/dev/sdXY`with the identifier of your partition(e.g., `/dev/sdc1`)

## Mount the Partition

```bash
sudo mkdir /mnt/mydrive
sudo mount /dev/sdXY /mnt/mydrive
```

or find `Disks` app in your PC, and mount the partition with GUI in `Disks`
