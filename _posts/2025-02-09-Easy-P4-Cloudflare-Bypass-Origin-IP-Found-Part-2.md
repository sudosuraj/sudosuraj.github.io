---
layout: post
title:  Easy P4 Cloudflare Bypass, Origin IP Found Part 2
author:  sudosuraj
date:  2025-02-09
categories:  [bugbounty]
tags:  [bugbounty]
image:
  path: /assets/img/headers/cloudflare.jpg
  alt: web pentesting
---

Easy P4: Cloudflare Bypass, Origin IP Found (Part 2)
====================================================
Introduction
============

Hi, myself Suraj Sharma aka **sudosuraj**. This is a short part 2 of Cloudflare WAF bypass, Find Origin IP techniques. Before you go ahead, I’d suggest you to read part-1 from [here](https://medium.com/easy-p4-cloudflare-bypass-origin-ip-found-part-1-685d27e73dd0). Without any boring intro, lets dive in.

Contd…
======

4. Using favicon hash
----------------------

Collecting origin IP using favicon.ico is quite easy. Let’s suppose your target is target.com, follow below steps:

**Steps 1 Get hash from favicon.ico:** Visit [https://favicon-hash.kmsec.uk/](https://favicon-hash.kmsec.uk/) and paste your target, it will give you hash.

**Step 2 search hash across censys and shodan:** If you observer your results from step1, the tool [https://favicon-hash.kmsec.uk/](https://favicon-hash.kmsec.uk/) also gives quick search link for virustotal, shodan and censys, click on them and it will redirect you on search page with respective dorks.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*j_dQduZT-qKZUWKVSci19A.png)

**5. Using Virus Total and URLScan:**
--------------------------------------

Virus Total and URLScan API are easy and effective method to get origin IP address of a Cloudflare protected web site. Replace your target domain in the followings and check all IP address in response:

**VirusTotal VTAP:** You’ll need an API key, but that’s not big deal, you can get a free API key by signing-up on _virustotal.com._

**Use your API and Visit: _https://www.virustotal.com/vtapi/v2/domain/report?apikey=<APIKEY>&domain=target.com_**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*9ewvZIZdiP7Km4kjd-Jvow.png)

**URLScan:** URLScan is easy one, you don’t need any API key, simply replace your target here: [**_https://urlscan.io/api/v1/search/?size=10000&q=domain:target.com_**](https://urlscan.io/api/v1/search/?size=10000&q=domain%3Atarget.com)

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*PmUxN4iSLrLZzcmpWIixDA.png)

**6. The final secret method:**
--------------------------------

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*9INcBzOY4dD_5aCCrGIR_g.jpeg)

Don’t be sad if all above methods don’t work, I have something speacial for you, yeah I mean it, you waited whole week for part-2, you deserve this.

Before we begin, let me tell you one thing, using this method I have secured $$$ bounty till now.

This is your last hope to find origin IP of your target. If this fails, don’t hunt for Origin IP for particular domain, move on to the next target!

**HTTP.title method:**

As the name suggests, you just need your target’s http title. Copy the http title of the target, and use below Censys and Shodan dorks:

**Censys:** services.http.response.html_title:”Title”

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*b2KfWG99UyEh7uBY0FJozw.png)

**Shodan:** http.title: “Title”

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*HKyE66oBnLGPJrqUiCKyRw.png)

Yeah, that’s it, its not a rocket science!

With this, lets conclude here, I will write part-3 if I get any new method for this easy P4. Let me know your thoughts below!

Lets Connect:
-------------

**LinkedIn:** [https://www.linkedin.com/in/sudosuraj](https://www.linkedin.com/in/sudosuraj)

Sharing is caring ❤

Peace.
