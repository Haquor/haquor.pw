---
author: Haquor
date: 2019-11-28T18:37:12-05:00
draft: false
title: "How to Set Up a Free, Anonymous VoIP phone"
type: post
url: /2019/11/28/anonymous-burner/
image: "voip-client.png"
---

I found this service while searching for a free VoIP provider and debated whether I should share. The reason? I didn't want it to catch on. I'd like to keep this SIP provider & method relatively obscure so it isn't abused by bad threat actors. So please, only use this for legal purposes. Don't get it shut down.

I'm sharing this in the hopes it'll be useful to other security researchers or even just IT enthusiasts who want a quick, anonymous VoIP number.

Shout out to Kerberos for helping me troubleshoot the VPN aspect & JMP for the free services.
<!--more-->

## Basic OPSEC

Even the best laid plans fall apart with bad OPSEC. This isn't the blog for learning [basic OPSEC](https://medium.com/@JMartinMcFly/basic-opsec-for-the-uninitiated-77d0839f7bce). Randomize handles, browse securely, and pay attention to services/softwae that creates unique fingerprints that might identify you later.

## Secure Browsing

For this to really be anonymous you should do this from a secure browser, and a secure tunnel. Chain VPN or TOR together however you see fit. Otherwise you're sorta wasting your time.

## Register for Jabber/XMP/JMP 

Register for a Jabber/XMP account
https://xmpp.is/account/register/

You should choose an XMPP client that JMP chat recommends. Good options are Psi, Gajim or Movim. Movim worked best for me.

Make sure you're logged in to the XMP client before you complete this next step.

Go to JMP chat and register for a phone with desired area code
https://jmp.chat/sp1a/register1/

Put in your XMP information.

## Your Free SIP Account

Paste verification code into JMP site.
You should then get your SIP server info
If you don't, download: Psi, Gajim or Movim and add cheogram.com as a contact
Then right click cheogram -> Execute Command -> Reset SIP Account
This will give you your SIP info in the following format:

server: jmp.servers
user ID: your_user
Password: your_pass

## Download a VoIP Client
Download linphone or similar VOIP SIP client
Put in your VOIP info

You get 30 minutes of calling & 300 texts/picture for 30 days.
After 30 days or after you run out make a new account

JMP may also accept BTC payments (not sure yet)
You need to message "ossguy" in the JMP/Soprani.ca chatroom at discuss@conference.soprani.ca
or text them - +1 416 993 8000 (Canada) or +1 312 796 8000 (US)

## VoIP Client through 
To use VoIP (such as linphone or Jami) with VPN, make sure your VoIP client is configured to use the local IP of your VPN interface when it sends the "register" command to the SIP server. Had a lot of issues with clients using other IP. You can specify this in .linphonerc or in Jami's advanced settings. May take a few restarts to take affect

You should see something like this:
{{< fluid_imgs
  "pure-u-1-1|/voip-client.png|VoIP"
>}}