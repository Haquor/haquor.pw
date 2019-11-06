---
author: No Content Found
date: 2018-11-24 21:04:05+00:00
draft: false
title: Unmasking an IP behind a proxy
type: post
url: /2018/11/24/unmasking-an-ip-behind-a-proxy/
---

With government surveillance and targeted advertising constantly tightening their grip on internet connected devices, more and more users are turning to anonymity software.

Proxies allow a user to hide behind a machine running dedicated anonymity software. With a proxy, a user's machine can appear to be halfway across the globe.

There's also the TOR network, which routes the user through a series of anonymous nodes, creating secure layers and providing access to a new type of Inter network.

This is well and good for people trying to hide their location. But have hackers found a way around this?

There are **three **main ways a hacker can expose you real IP from behind a proxy or anonymity network.


## Unsecured Code Objects




#### (JavaScript, Flash, Java, ActiveX)




<blockquote>Most likely what they do is utilize a Flash or Java applet, or a bit of JavaScript, which would "go directly to the source to learn the true IP".

- [Kromey](https://superuser.com/users/74087/kromey) (SuperUser)</blockquote>


Third party plugins and software have been abused reliably for decades. Most users insist on the benefits of rich multimedia applications and dynamic animations. These multimedia perks are achieved through the use of software frameworks like Adobe Flash, Java, ActiveX, and JavaScript.

The problem with these programs, is that proxy software very frequently runs INSIDE the browser. Meanwhile, code objects access data OUTSIDE the browser.

Sometimes an attacker can use the built-in functionality of Flash or JavaScript technology to access the host machine. Other times, a 0-day exploit launched against these code objects will yield a result.

Below are some interested examples.


### Adobe Flash Sockets




<blockquote>If you write a simple Flash program that opens a socket to a remote logging server, you can embed that on a site and use it to identify certain people running through Tor or any other SOCKS/HTTP proxy.

- [meowface](https://news.ycombinator.com/user?id=meowface) (Hacker News)</blockquote>


To try out this example, rewrite this function connecting to a Telnet server to use your logging server.

    
    public function Telnet(server:String, port:int, output:TextArea) 
    { 
        serverURL = server; 
        portNumber = port; 
        ta = output; 
        socket = new Socket(); 
        socket.addEventListener(Event.CONNECT, connectHandler); 
        socket.addEventListener(Event.CLOSE, closeHandler); 
        socket.addEventListener(ErrorEvent.ERROR, errorHandler); 
        socket.addEventListener(IOErrorEvent.IO_ERROR, ioErrorHandler); 
        socket.addEventListener(ProgressEvent.SOCKET_DATA, dataHandler); 
        Security.loadPolicyFile("http://" + serverURL + "/crossdomain.xml"); 
        try 
        { 
            msg("Trying to connect to " + serverURL + ":" + portNumber + "\n"); 
            socket.connect(serverURL, portNumber); 
        } 
        catch (error:Error) 
        { 
            msg(error.message + "\n"); 
            socket.close(); 
        } 
    }


The vulnerability here is that Adobe Flash does not utilize your browser's built in proxy when creating a connection to your logging server.

The solution is to configure your proxy correctly. You must ensure that code objects route through your proxy.

Keep in mind, not every version of Flash has this issue. Flash is making [efforts ](https://www.adobe.com/devnet/security/articles/flash-player-sandbox-bridge.html)to improve their security.


### Leveraging Exploits




<blockquote>During Operation Torpedo, the FBI deployed an "implant" on Freedom Hosting's servers which was an exploit for CVE-2013-1690, a vulnerability in Firefox.

It wasn't a 0-day, but a lot of people using The Tor Browser had not patched yet. It was just some JavaScript which executed a small bit of Windows shellcode, sending each victim's IP address, MAC address, and a serial number to an FBI-controlled server.

The only way to be safe from this was with an updated Firefox version, and/or running NoScript.</blockquote>


To pull of a specific exploit, an attacker only needs to look for CVEs related to the browser or code plugin they want to target. Any exploit that enables _remote code execution_ is sure to be a winner!

The exploit an attacker looks for can be at **any **level, as long as it breaks out of the boundary the proxy runs within.

A great example of remote code execution is the [Windows Metafile Vulnerability](https://en.wikipedia.org/wiki/Windows_Metafile_vulnerability). The exploit would compromise a browser's image handling by utilizing a hole in the _gdi32.dll _file to execute arbitrary code on NT versions of the Windows OS.

This is a long outdated example, but there are plenty of current examples, just like it.


## Unsecured DNS


This next trick requires access to the DNS server for your logging domain. If you have access, you can see all the requests coming in.

If you create a unique subdomain address for each visitor and embed it somewhere in the HTML, you can check the user's real IP on your DNS server.

82.69.65.76 has requested IP for 70657569FAKE.domain.com

70.65.75.69 has accessed 70657569FAKE.domain.com

The solution is to use a DNS Masquerade server with something like _dnsmasq_. Some proxies or proxy services also route DNS request traffic as well.


## A Smarter Setup


A slicker, smarter setup for running a proxy comes from a leader in anonymity; the [Whonix OS](https://www.whonix.org/wiki/Main_Page).

It requires you to have access to virtualization technology. You can either run Whonix directly on your host, or simulate this environment through a virtualization enabled host.

Virtualization enables a deeper layer of abstraction, keeping your real IP and networking info multiple steps away from your attacker.

You begin by setting up 2 Virtual Machines (VMs):


### **Gateway VM**





	  * 2 NICs [One Public, One Internal to VMs only]
	  * Runs Tor
	  * Exposes only Tor Socks5 port to internal network
	  * Firewalls everything else



### **Workstation VM**





	  * 1 NIC [internal only]
	  * Connects only to Gateway VM on Tor SOCKS5 port
	  * Prevents any app from connecting
	  * Must be isolated from the host



<blockquote>

> 
> #### Whonix Design
> 
> 
Whonix consists of two VMs: the Whonix-Gateway and the Whonix-Workstation. [[2]](https://www.whonix.org/wiki/Main_Page#cite_note-2) The former runs Tor processes and acts as a gateway, while the latter runs user applications on a completely isolated network. The Whonix design affords several benefits:

> 
> 
	  * Only connections through Tor are permitted.
	  * Servers can be run, and applications used, anonymously over the Internet.
	  * DNS leaks are impossible.
	  * Malware with root privileges cannot discover the user's real IP address.
	  * Threats posed by misbehaving applications and user error are minimized.

</blockquote>


![whonix_concept_refined](https://haquor.files.wordpress.com/2018/11/whonix_concept_refined.jpg)

