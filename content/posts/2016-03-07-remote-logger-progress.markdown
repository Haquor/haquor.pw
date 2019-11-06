---
author: No Content Found
date: 2016-03-07 21:13:45+00:00
draft: false
title: introducing weevil
type: post
url: /2016/03/07/remote-logger-progress/
---

Progress is coming along well on the remote logger.

When I began, my first thought was to craft a simple keylogger for personal use. I pretty quickly veered off on a tangent and ended up researching DLL injection.

While doing this, I stumbled upon some other stuff involving byte code and other cool stuff soooo. I ended up conceptualizing this.

Here's the informational so far

Weevil
- the purpose of the weevil software is a simple, minimalist, Windows based easily deployable payload that worms its way out of the network and back to a listening server.

- the weevil then sits on the infected system and continuously sends a live keystroke feed back to any listening party through the means of a remote command shell.

Weevil works very close to the system core and can be loaded as a SYSTEM process.

Coded in C++, based in Windows using a 32-bit program architecture.

Generator offers the option of embedding the byte code within another process.
The generator then creates an infected file.
This file can be delivered to a target system or encrypted with Shikata Ga Nai.

Port used: 666 (testing purposes, configurable)
IP used: virtual machine (testing purposes, configurable)

Functionality
1. File generator program: C#
- Control Server
- Control Port
- Pack with Executable
2. Weevil (C++)
- Run as SYSTEM process or unable to close/service
Does it need to be run as admin?
- Open a channel to control server? If error, log error somewhere in memory
- Once C&C server is open, begin to log by hooking WinAPI
- Check for previous keystroke logging data. Make it avaliable.
- Send keystroke data to remote terminal
- Continue connection until termination
