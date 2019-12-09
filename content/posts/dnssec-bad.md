---
author: Haquor
title: "BUG FIX: DNSSEC validation failed: no-signature manjaroo"
date: 2019-12-09T01:12:14-05:00
draft: false
type: post
url: /2019/12/09/dnssec-bad/
image: "dnsssec.webp"
---

#### After switching ISPs I started to encounter a weird problem. A lot of random websites simply didn't load.

No explanation. Just "unable to be reached"

Upon pinging around, I noticed that domain names weren't resolved to IP addresses. I could ping, and even reach an unreachable websites IP, but not it's domain name.

[Manjaro](https://en.wikipedia.org/wiki/Manjaro) uses [systemd-resolved](https://wiki.archlinux.org/index.php/Systemd-resolved) by default, a systemd service that provides network name resolutions to local applications.

To check the DNS actually used by systemd-resolved, I ran
resolvectl status

At the time I was using Google DNS servers, no trouble there. All DNS servers were correct a reachable. So what was the problem?

I decided to delve into resolved's process by running

    resolvectl query unreachable-site.com
The command promptly returned

    DNSSEC validation failed: no-signature manjaroo

It turns out, [DNSSEC](https://blog.cloudflare.com/dnssec-an-introduction/) was the culprit.

<!--more-->

### DNSSEC validation

When DNS was built, no attention was paid to security. Sure, you could create DNS records identifying the IP of a site...but there was no real authentication.

If a false DNS record slipped by, there was no cryptographic proof it came from the right place.

DNSSEC added cryptographic signatures to existing DNS records, allowing  you to verify that the record you've requested is **really** coming from a legitimate authoritative name server, and not a rogue one. 

For some reason, my DNSSEC service wasn't pulling valid signatures.
But why?

### Not all ISPs support DNSSEC

The reality is, DNSSEC isn't being adopted by everyone.
In fact, many major ISPs don't actually support DNSSEC yet for all customers.

A quick Google search revealed, mine didn't.

Now, normally this isn't a problem. You don't HAVE to use the DNS servers your ISP sets for you. If you router allows, you can change the DNS servers your router uses to fetch domains.

Problem, my ISP did not allow you to change it's DNS servers.
You can change your DNS server locally all you want, but if your ISP directs all requests through its servers, and they don't support DNS, you're screwed.

### The Solution

Resolved is a great utility that gives you a few options. In Arch Linux and its variants, you can edit your resolved.conf file at:

    /etc/systemd/resolved.conf
    #DNS=
    #Domains=
    #LLMNR=yes
    #MulticastDNS=yes
    DNSSEC=false
    #DNSOverTLS=no

You can specify different DNS options for resolved to use.
By default, DNSSEC is set to allow-downgrade. This normally covers situations where a server does not support DNSSEC properly. If it doesn't DNSSEC mode is automatically disabled.

Unfortuanately, it didn't cover issues where the ISP's DNS servers block validation. So I had to set my DNSSEC to true, temporarily while I looked for other solutions.

I'll be reaching out to my ISP to diagnose other solutions, but until then, this is the bug as it stands.

Related threads:

https://bbs.archlinux.org/viewtopic.php?id=240427

https://github.com/systemd/systemd/issues/9771