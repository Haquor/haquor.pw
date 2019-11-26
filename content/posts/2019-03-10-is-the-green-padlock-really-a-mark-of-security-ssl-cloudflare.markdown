---
author: Haquor
date: 2019-03-10 14:10:14+00:00
draft: false
title: Is the Green Padlock Really a Mark of Security?
type: post
url: /2019/03/10/is-the-green-padlock-really-a-mark-of-security-ssl-cloudflare/
image: "/ev-green-bar-example02.png"
---

We all know the trusty little green padlock button on our favorite websites as the guarantor that everything is exactly as it seems, but how accurate is that?

{{< fluid_imgs
  "pure-u-1-1|/ev-green-bar-example02.png|Green Bar Example"
>}}

<!--more-->

The idea behind SSL is based on some pretty simple concepts. The idea of public key cryptography ensures that if a message is encrypted with a user's (or server's) private-key, it can only be decrypted with their public-key.

The actual protocol dealing with these encryption algorithms started out as SSL, back in the mid-late 90s, but was found to be vulnerable to a [host of exploits](https://www.acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/) targeting the strength of block cipher's. TLS has also found to be insecure, but that's a story for another post.

Now adays, the certificate systems that represent these protocols is known collectively as SSL/TLS certificating.

Certificates are supposed to ensure that your data is going to, and received only by, the server with the private decryption key. This prevents a man-in-the-middle (MiTM) from spying on your traffic. But how is SSL actually being used today?

The reality is, that with DDOS protection and load balancing solutions like CloudFlare, SSL certificate creation and implementation is being outsourced.

The risk is, that although Cloudflare might establish a secure connection from the _visitor_'s system to their own, their "free" SSL certificates don't enforce security from their OWN servers to yours.

A user on HackerNews, joepie91 [commented ](https://blog.cloudflare.com/introducing-universal-ssl/)on this issue back in 2016, citing an instance where users of The Pirate Bay experienced network blocking messages from the ISP, Airtel.

![](/cloudflare1.png)


What had  happened, was the Airtel had MiTM'd TPB's CloudFlare protected site.

Even now adays, the only thing a free SSL certificate from CloudFlare proves is that the owner of the website has verified the certificate.

It doesn't protect from any level of snoopery. CloudFlare knows this, and addresses this situation by explaining their [Universal SSL types](https://support.cloudflare.com/hc/en-us/articles/200170416-What-do-the-SSL-options-Off-Flexible-SSL-Full-SSL-Full-SSL-Strict-mean-).

Take a look:

![](https://support.cloudflare.com/hc/en-us/article_attachments/206124658/cfssl_flexible.png)
![](https://support.cloudflare.com/hc/en-us/article_attachments/206167937/cfssl_full.png)


![](https://support.cloudflare.com/hc/en-us/article_attachments/206167947/cfssl_strict.png)


Now which one looks better. More padlocks? Or less.

If your CloudFlare site is using Flexible or Full SSL and someone changes the backend IP address or somehow intercepts the connection from CloudFlare to the origin server, there is no way for a visitor to tell. Further, the attacker could change the SSL certificate to their own malicious one, and the visitor would STILL be greeted with a happy little padlock.

My beef isn't even really with CloudFlare, as a lot of sites use CloudFlare for subdomains of CDNs, which don't really require the same level of security as a fully functional website.

But this huge move to "[#savetheweb](https://blog.cloudflare.com/introducing-universal-ssl/)" and make over 1 million websites that have **no actual** security just helps to mislead those who don't know the inner workings of web applications & platforms.
