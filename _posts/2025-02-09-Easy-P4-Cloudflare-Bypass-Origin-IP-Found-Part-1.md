---
layout: post
title:  Easy P4 Cloudflare Bypass, Origin IP Found Part 1
author:  sudosuraj
date:  2025-02-09
categories:  [bugbounty]
tags:  [bugbounty]
image:
  path: /assets/img/headers/cloudflare.jpg
  alt: web pentesting
---

Easy P4: Cloudflare Bypass, Origin IP Found (Part 1)
====================================================

Introduction
============

Hi, myself Suraj Sharma, in this short write-up, I’ll show you various methods to find the origin IP of a website hidden behind a Cloudflare Web Application Firewall (WAF).

Step-by-Step Guide
==================

1. Initial Check with Extensions
=================================

*   **Wappalyzer Extension**: Identify the technologies used by the target website. Example: Amazon CloudFront CDN.
*   [**Shodan Extension**](https://chromewebstore.google.com/detail/shodan/jjalcfnidlmpjhdfepjhjbhnhkbgleap): Obtain the website’s IP and check for direct access. If it returns a CloudFront error, the direct IP isn’t accessible.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*escGpUzWNo4DctdTuBZ-Tg.png)

2. Using Command-Line Tools
============================

*   **Ping Command**: Check the IP associated with the domain.
*   **DNS Recon**: Perform reverse DNS lookups to find potential origin IPs.

3. Shodan Dorks
================

*   Use Shodan to find domain-related information. Access these IPs to check if they bypass the WAF.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*81CTN7dIe36Zt2XByBonRw.png)

> **Contd. in part 2:**
> That’s all for this one, I’ll show you more advanced techniques in part 2. Stay tuned, Happy Hacking!

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*IbjoN74XdXMzT1asy-9kjQ.png)![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*9EPGHoCi-r-V7Iv6w5EMMw.png)
