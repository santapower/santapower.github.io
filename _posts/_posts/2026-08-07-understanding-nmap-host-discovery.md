---
layout: default
title: "Understanding Nmap Host Discovery"
date: 2026-08-07
categories: [penetration-testing]
tags: [nmap, reconnaissance, networking, cybersecurity]
---

# Understanding Nmap Host Discovery

Before scanning ports or identifying services, one of the first steps in network reconnaissance is determining which systems are actually online.

Nmap provides several host discovery techniques that can help identify active devices on a network. In this post, I'll explain the basic host discovery process, useful commands, and some of the concepts I learned while practicing with Nmap.

> Only perform network scanning against systems and networks you own or have explicit authorization to test.

---

## What Is Host Discovery?

Host discovery is the process of determining which IP addresses correspond to active systems.


For example, suppose we are given the network:

```text
192.168.1.0/24
