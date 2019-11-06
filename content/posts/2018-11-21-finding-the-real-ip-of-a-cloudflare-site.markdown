---
author: No Content Found
date: 2018-11-21 20:50:19+00:00
draft: false
title: Finding the real IP of a Cloudflare site
type: post
url: /2018/11/21/finding-the-real-ip-of-a-cloudflare-site/
---

<blockquote>[Cloudflare](https://www.cloudflare.com) and other reverse proxy services can make websites faster and safer. One of the benefits of these services is that they add a layer of anonymity to mask a website's hosting provider and other details.</blockquote>


Sometimes, in our line of work, it's useful to know the real IP address associated with a Cloudflare hosted domain.

Without hacking Cloudflare, there's no good way around their proxy. However, with the proper information, we can figure out what IP the original site used.

When websites change, DNS information changes.

This DNS information is publicly indexed by a variety of free/paid services. [SecurityTrails](https://securitytrails.com/dns-trails) provides an elegant solution, with paid access to more advanced information.

Since I'm a strong believer of ballin' on a budget, we're going to use [ViewDNS.info](https://viewdns.info/iphistory/) as an example.

**TARGET**: https://wordoffaithfellowship.org/

**DOMAIN**: wordoffaithfellowship.org

By running a quick ping request, we can grab their Cloudflare IP

`Pinging wordoffaithfellowship.org [104.25.201.105] with 32 bytes of data:`

**CLOUDFLARE IP: **104.25.201.105

Plugging in our data to [ViewDNS.info](https://viewdns.info/iphistory/), we see that the last seen IP before Cloudflare was 192.185.35.89.
<table width="1000" align="center" id="null" bgcolor="#FFFFFF" >
<tbody >
<tr >

<td >IP history results for wordoffaithfellowship.org.
==============


<table border="1" >
<tbody >
<tr >

<td width="150" >IP Address
</td>

<td >Location
</td>

<td >IP Address Owner
</td>

<td align="center" >Last seen on this IP
</td>
</tr>
<tr >

<td >104.25.202.105
</td>

<td >United States
</td>

<td >Cloudflare, Inc.
</td>

<td align="center" >2018-11-17
</td>
</tr>
<tr >

<td >104.25.201.105
</td>

<td >United States
</td>

<td >Cloudflare, Inc.
</td>

<td align="center" >2018-11-17
</td>
</tr>
<tr >

<td >192.185.35.89
</td>

<td >Houston - United States
</td>

<td >WEBSITEWELCOME.COM
</td>

<td align="center" >2017-02-25
</td>
</tr>
<tr >

<td >192.254.233.20
</td>

<td >Houston - United States
</td>

<td >WEBSITEWELCOME.COM
</td>

<td align="center" >2016-10-22
</td>
</tr>
<tr >

<td >174.132.148.226
</td>

<td >Dallas - United States
</td>

<td >SoftLayer Technologies Inc.
</td>

<td align="center" >2013-07-05
</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>
**REAL IP: **192.185.35.89
