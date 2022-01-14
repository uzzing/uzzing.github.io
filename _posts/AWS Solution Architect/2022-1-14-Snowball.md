---
title:  "[AWS Solution Architect] Snowball / Snowball Edge / Snowmobile"
date: 2022-1-14 12:36PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-14 12:36PM
---

## Snowball

- `Petabyte-scale data transfer service`
- Move data onto AWS via physical briefcase computer
- very quickly
- very inexpensively

### speed
- when you try and transfer 100 terabytes over a high speed internet to AWS, it could take over 100 days - but with a snowball, it will take `less than a week.`

### cost
- snowball is going to `reduce` that cost by 1/5th


### Features and limitations

- come with the kind of digitial shipping label
- temper and weather proof
- The data is encrypted end to end using tivity.
- has Trusted Platform Module (TPM) (chip)
    - a specialized chip on an endpoint device that stores RSA encryption keys specific to the host system for hardware authentication.
- For security purposes, `data transfers` must be completed within `90days` of the Snowball being prepared.
- Snowball can import and export from S3

### Size
- in two sizes
- 50 terabytes (42 TB of usable space)
- 80 terabytes (72 TB of usable space)
- you don't need to utilize the space on there

- petabyte scale migration 
    - you can use multiple snowballs to get to petabytes
        - A petabyte is a multiple of a byte
---

## Snowball Edge

- snowball + more storage and onsite compute capacity capabilties.

- difference 
    - orange bars
        - that's the way to distinguish snowball from snoball edge.
    - more storage and with local processing

###  features
- LCD display 
    - shipping information and other functionality
    - instead of having E-ink display
- ⭐️ can undertake `local processing` and `edge-computing workloads`
- can use in a cluster in groups of 5 to 10 devices
    - you can get a bunch of these noble edges
    - have them work on a single job that is kind of like having your own little mini data center up to five to 10 devices.
- three options for device configurations
    - you can optimize what you need
    - and the CPU amounts are goint to change in this device based on what you need.
    - storage optimized (24 vCPUs)
    - compute optimized (54 vCPUs)
    - GPU optimized (54 vCPUs)

### Size
- 100 TB (83 TB of uable space)
- 100 TB Clustered (45TB per node)

---

### Snowmobile

- a 45-foot long ruggedized shipping container
- size : 100 PB (perabytes)


--- 
### Summary

<img width="1440" alt="Screen Shot 2022-01-14 at 12 32 11 PM" src="https://user-images.githubusercontent.com/83699657/149447297-027caf84-c3ff-4f75-92cd-9c95994889b5.png">

---

The copyright of all material here is on the video <https://www.youtube.com/watch?v=Ia-UEYYR44s>
This post is just for studying AWS SAA.