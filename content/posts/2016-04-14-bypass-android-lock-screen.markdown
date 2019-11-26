---
author: Haquor
date: 2016-04-14 04:22:40+00:00
draft: false
title: Bypass Android Lock Screen
type: post
url: /2016/04/14/bypass-android-lock-screen/
---

This process revolves around deleting the .key files that enable the android lock screen.

Download ADB through [Cygwin ](http://x.cygwin.com/docs/ug/setup-cygwin-x-installing.html)on Windows, or with the following command on Linux:

	sudo apt-get install android-tools-adb

Connect the phone to your computer via USB

Open a terminal window (linux) or cygwin (windows)

	adb devices
	adb shell
	cd data/system
	su
	rm *.key
<!--more-->
	  4. Reboot the device

If this code, for whatever reason, does not work, there is another method that works for **ALL ANDROID DEVICES**.
_adb shell_

_cd_

_/data/data/com.android.providers.settings/databases_

_sqlite3 settings.db_

_update system set value=0 where_

_name='lock_pattern_autolock';_

_update system set value=0 where_

_name='lockscreen.lockedoutpermanently';_

_.quit_

Then reboot the device


