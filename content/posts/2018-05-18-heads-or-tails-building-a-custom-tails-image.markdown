---
author: No Content Found
date: 2018-05-18 08:19:02+00:00
draft: false
title: 'Heads or Tails: Building a Custom Tails Image'
type: post
url: /2018/05/18/heads-or-tails-building-a-custom-tails-image/
---

You should begin by prepping our build environment and grabbing a copy of the Tails source code, as detailed [here](https://tails.boum.org/contribute/build/).


# Setup the build environment





	  1. To install everything the Tails build system needs, execute the following command:

    
    <code>sudo apt install \
        psmisc \
        git \
        rake \
        libvirt-daemon-system \
        dnsmasq-base \
        ebtables \
        qemu-system-x86 \
        qemu-utils \
        vagrant \
        vagrant-libvirt \
        vmdebootstrap && \
    sudo systemctl restart libvirtd
    </code>



	  2. Ensure your user can run commands as root with `sudo`.
	  3. Ensure your user is in the relevant groups:

    
    <code>for group in kvm libvirt libvirt-qemu ; do
       sudo adduser "$(whoami)" "$group"
    done
    </code>



	  4. Logout and log back in to apply the new group memberships.



# Get the Sawce






	  * To get the Tails sources and checkout the [development branch](https://tails.boum.org/contribute/git/#main-repo), execute the following commands:

    
    <code> git clone https://git-tails.immerda.ch/tails && \
     cd tails && \
     git checkout devel && \
     git submodule update --init
    </code>







# Checking the Manual


It's important to understand how information flows, and how we follow clues through README files and man pages to solve our problems.

The comment at the end of the build command description mentions:

"You may also want to [customize](https://tails.boum.org/contribute/customize/) the content of the ISO image before building it."

This brings us to a page that lets us know a few important facts:



	  1. There are settings specific to tails that are stored in `config/amnesia`
	  2. Tails is based on Debian Live (Stretch)
	  3. Debian Live is almost completely customizable...so if we wanted to make changes, we're headed there.



# Hacking Debian Live


Life isn't easy. If it was, would it really be any fun?

Just to make life a little harder (and more interesting), the [manual](http://live.debian.net/manual/oldstable/html/live-manual.en.html) link in the documentation is broken. Typical for 'stable' operating systems haha

A quick Google Search, and we see that Debian actually hosts packages for its Debian Live manuals.

`sudo apt-get install live-manual-html`

And we've got ourselves a copy. Going through the list of files, we find our manual in

`/usr/share/doc/live-manual/html/live-manual/index.en.html`

I recommend reading through it. It's a helpful and well structured guide-book to messing with Debian Live.

But what we're specifically looking for....

![Screenshot from 2018-05-18 04-13-55](https://haquor.files.wordpress.com/2018/05/screenshot-from-2018-05-18-04-13-55.png)



# Finding the Skeleton Key


After hitting a dead end with the live manual I decided to take a look through the tails source directory. Immediately, a conveniently placed file entitled HACKING.mdwn caught my eye.

https://gist.github.com/Isonyx/5fcb0e35854b97c4f05b2cc10058b6f4


