---
author: admin
date: 2019-08-26 07:43:55+00:00
draft: false
title: With Seamless Cross Platform Integration
type: post
url: /2019/08/26/minimalism-through-secure-cloud-sync/
---




It's hard to put into words my distaste for bloatware.







Every installation of Windows comes with a certain set of extra software. Depending on where you get your computer, you'll find a preinstalled set of games, applications and sometimes even [adware](https://www.cnet.com/news/superfish-torments-lenovo-owners-with-more-than-adware/). Retail locations from brick and mortar stores like Best Buy to online vendors such as [Lenovo](https://www.pcworld.com/article/2889905/if-you-hate-pc-bloatware-here-are-the-vendors-to-avoid.html) package their products with such annoying bloatware.







Working in a bloated environment is unacceptable. It's 2019, and we live in a world where we can get _whatever_ we want,_ whenever _we want. This reality **should** enable us to cultivate purposeful, efficient work spaces. These days, even the variety of projects I find myself engrossed in often create a bloated environment. New projects and challenges force me to adapt with new software solutions, which just seem to stack up on my hard drive.







When the time comes to move to a new device, or worse yet, work on someone else's, I'm gripped by a very real and very visceral fear. What software do I take? How do I recreate my environment? 







I find myself scrambling for the proper media. More often than not, that means a trip to the store for a new USB drive. Sure, shelling out the money for an external HDD is well worth it's weight. But what happens when you've modified nearly 100 files while working remotely and then have to manually overwrite them BACK onto the HDD for backup purposes?







It's no way to live. I propose a better solution.







There's a few requirements I'm looking for:





  1. EASE OF USE --- Things can't get too complicated. It needs to be secure, yet simple and elegant   2. SECURITY --- If I'm going to use a cloud solution, I need both end-to-end and client-side encryption   3. MOBILITY --- I want to be able to provision **any** OS at any time with the applications, files and settings I've come to know and love.





Now, the obvious answer to this problem is to use cloud backups. But the 'Cloud isn't really enough.







## CLOUD STORAGE SERVICE ([TRESORIT](https://tresorit.com/))







Before, I explain my choice, I need to explain where security comes in. You don't want the encryption key for your files stored on your cloud provider. It completely defeats the purpose. It creates a single point of failure. Who cares if your files are encrypted, if your Cloud provider holds the key. This isn't real security. I needed a solution that stored encryption keys on the client side.







[Tresorit ](https://tresorit.com/)does just that. Using AES256,  Tresorit encrypts each file and directory you choose to send to the cloud. It never transmits the keys, and never sends files unencrypted. Using public key cryptography,  Tresorit allows you to share files quickly, and simply within your contact network. Not only that, but the PKI certificate you use has _no personal information _connected to it, making it completely anonymous.







Tresorit itself is a Switzerland based provider of offshore cloud services. They have data centers in Ireland and the Netherlands, running an ISO compliant Microsoft Azure infrastructure. Their service provides high security and high reliability.







Lastly, Tresorit, unlike many providers, is cross platform. This means I can have the same setup, with all my files mirrored across multiple operating systems. 







Although the cost is high compared to more mainstream cloud providers, it's hard to put a price on peace of mind.







Once we install Tresorit, we can back up all our important files to the  cloud. For me, currently operating primarily from Windows, this means:  Documents, Music, Pictures and Downloads.







You'll notice already that this setup forces you to prioritize which  parts of your OS storage are important. For a more lightweight setup, I  remove the Downloads folder and ensure I copy relevant downloads to my  Documents folder. This frees up a whole folder during cleanup time.  







## PASSWORD MANAGEMENT ([DASHLANE](https://www.dashlane.com/))







So you've got your files. But what about your online life? All your profiles are managed through passwords. To keep things simple, but secure, you need a lightweight password storage solution.







It should: allow you to auto fill credentials, store things other than passwords, and discourage the re-use of common passwords.







For this, I chose [Dashlane](https://www.dashlane.com/). Lastpass provides similar features, but I just preferred the Dashline interface. It has all the above features and gives you a nifty password strength audit. With Dashlane premium, you can even tap into credit/identity monitoring services to make sure your credentials haven't been leaked in a recent breach.







The downside to most password storage options is centralization. Most password managers store your password cache on their servers. Encrypted or not, this provides a single point of failure, controlled by a provider. I prefer a password manager that stores the database on the **client-side.** Dashlane does this. A quick call to my Tresors and I can pull down my password database on any OS.  








## SYNC SOFTWARE & SETTINGS







This last part is the hardest. Without backing up every single application folder, and all its dependencies, I needed a simple, automated way to create "load-outs". Load-outs will allow me to instantly provision any machine with an array of settings and software needed for the task at hand.







Since each OS works a little different, we'll have to create multiple solutions. Currently I only use Windows and Linux, so I'll offer solutions for both. Mac user's? You're on your own.







### Windows Solution







For Windows I take advantage of [Chocolately](https://chocolatey.org/), the best windows package manager. Chocolately works through Powershell modules to automate software installation and keep things up to date. To create the actual loud-outs, I'll leverage [Boxstarter](https://boxstarter.org/). 







To put it simply, Boxstarter creates "Repeatable, **reboot resilient** windows environment installations made easy using [Chocolatey](https://chocolatey.org) packages."







When you create a load-out (or package according to Boxstarter), it generates two things. The first is a .nuspec file. This file servers as a manifest, storing information about your load-out. The second is a ChocolatelyInstall.ps1 file. This file holds the meat and potatoes of your load-out.







Boxstarter provides for not only software installation, but configuring Windows settings through Powershell commands. Simply throw some commands into ChocolatelyInstall.ps1 to unpack certain files or settings you want to provision with your software installs. 







As I develop my Boxstarter packages, you'll be able to find them at this Github repository











### Linux Solution







Don't worry. This is even easier. Whatever Linux distribution you use, you'll have to take the time out to create some scripts to install your load-out apps through your native package manager. Whether it's **apt **or **pacman**, the process is simple and straightforward. Settings also follow suit.







The scripts for my Linux load-outs will live at the same repository.  








## ROUTINE CLEANUP







Now that we've got a simple, secure and portable setup for our files we can get minimal with it. My advice? Reset your OS. Go ahead. Many times there's no substitute for a hard reset. If you trust your load-out files, you'll be able to get back exactly what you need.







And the rest? You probably didn't need it. Working with this setup, I realized how many settings or applications I configure once, and then forget about for months on end. Those days are over.







Once your workspace is fresh and clean with your brand-new software/settings load-out: KEEP IT THAT WAY. Configure [CCleaner ](https://www.ccleaner.com/)or another reliable maintenance app. Have it clean out unused folders and free up space with no fear of losing anything important.





  * System Maintenance - CCleaner, IOBit, Iolo System Mechanic, BleachBit & Cruft  * Hardware Tests - CPU-Z, CrystalDiskInfo, WinDirStat, Windows Memory Diagnostic, Memtest86+, smartmontools





Go ahead, relax in the confidence and simplicity of your new setup .







  




