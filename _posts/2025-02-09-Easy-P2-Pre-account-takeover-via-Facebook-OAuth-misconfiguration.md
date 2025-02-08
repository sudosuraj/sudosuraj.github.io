---
layout: post
title:  Easy P2 — Pre account takeover via Facebook OAuth misconfiguration
author:  sudosuraj
date:  2025-02-09
categories:  [bugbounty]
tags:  [bugbounty]
image:
  path: /assets/img/headers/facebook.jpg
  alt: web pentesting
---

Easy P2 — Pre account takeover via Facebook OAuth misconfiguration
==================================================================

**Login with Facebook** has become a widely-used authentication method, simplifying the sign-in process for users across apps and websites. However, as convenient as it is, there’s a lesser-known vulnerability that could lead to account takeover if not handled properly. Specifically, if email sharing is disabled during the Facebook login process, an attacker can exploit this to gain unauthorized access to a victim’s account.

**Disable Email Sharing On Facebook OAuth:**

1. Log in you Facebook.
2. Click “modify access permissions/edit access”
3. Uncheck the email address checkbox.
4. Click Continue.

**POC**
-------

1.  **Visit the target site** (for example, `https://example.com`) and log in using the "Login with Facebook" option.
2.  **Disable email sharing** by unchecking the email address during the Facebook login process.
3.  **Enter the victim’s email address** when prompted by the target site for an email, as it will require one since the email was not shared via Facebook.
4.  Without email verification, **the system will grant access to the victim’s account**, thus completing the takeover.

![Photo by Etienne Girardet on Unsplash](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*_XV39TVECmqOdYVc)

Follow for more:

*   [LinkedIn](https://linkedin.com/in/sudosuraj)
*   [GitHub](https://github.com/sudosuraj)
*   [Bugcrowd](https://bugcrowd.com/sudosuraj)
*   [X](https://x.com/sudosuraj)
*   [Instagram](https://instagram.com/sudosuraj)
