---
author: No Content Found
date: 2019-03-08 10:24:20+00:00
draft: false
title: (Workaround) Multiple shell shortcuts in Hyper terminal
type: post
url: /2019/03/08/hacking-multiple-shell-shortcuts-in-hyper-terminal/
---

As of March 8, 2019 Hyper doesn't have native support for multiple shells.

Their configuration system (.hyper) allows you to specify which shell Hyper uses by default, but doesn't allow you to conveniently switch between multiple shells without re-editing the file.

A user on the issues page for Hyper's Github provided a workaround solution involving changing Hyper's shellargs command to run a batch file on startup, that then allowed the user to select from a menu the shell to load.

To further simplify and automate the process, I have set up a more preferable workaround. It also involves Hyper shortcuts Running as Administrator by Default while bypassing UAC confirmation.

This solution is Windows native and has only been tested on Windows 10 Pro x64.

Here's how its done


### Create tasks for each of your shells in Task Scheduler


I found that by running with the highest elevation from **Task Scheduler** on Windows, I could bypass the pesky UAC prompt that hit me every time I tried to open my Hyper shortcut.Using Task Scheduler also works well in this case, because this workaround uses an _environment variable _that needs to be set for the current user right before EVERY new Hyper shortcut is actually launched.Task Scheduler lets us launch our environment var setting script (start-args.bat), which will set the environment variable %HYPERTERM% to the command name of the shell (either bash or cmd in my case).The process is very simple. Open up Task Scheduler and Create a New Task for each of your shells. The tasks name should be simple, and reflect the shell. I used HyperCMD and HyperBash. Each task should have the following configurations

General Tab :=> Make sure "Run with the highest privileges" is _checked_ and set "Configure for" to your current OS.

Actions Tab :=> Create New entires to Start 2 programs. The first will be your _start-args.bat_ file with the argument of your shell and the next, the location of _Hyper.exe_.

![1](https://haquor.files.wordpress.com/2019/03/1-e1552034652672.png)


Conditions Tab :=> If you are on a laptop, you'll need to make sure "Start the task only if the computer is on AC power" is _unchecked_. This will prevent your tasks from failing if your laptop is plugged in.

Settings Tab :=> _Check_ "Allow task to be run on demand" and "If the task is already running, then the following rule applies:" should be set to _Run a new instance in parallel_

Now repeat for the remaining shells.


### Create a start-args,bat & start.bat files


https://gist.github.com/Haquor/dc5f65a5135e31902b8d0934800ef325This code is pretty self explanatory, the start-args.bat takes an argument (passed from Task Scheduler) and sets our ENV variable %HYPERTERM% to the currently selected shell we about to run. The start file just starts it, and is called through changing the shellArgs variable in Hyper's config file.


### Change hyper.config file shellArgs var


Open up Hyper and go to Edit -> Preferences to open up your .hyper file. Scroll down until you find shellArgs and change it to the following:`shellArgs: ["/C", "\\Users\\YOURUSER\\AppData\\Local\\hyper\\start.bat"],`


### Create custom shortcuts to your tasks


Lastly, since we have custom tasks that will run when we call them....we can create special shortcuts. One for each of our shells.Create some new shortcuts on your desktop, with the _Target _field set in this manner for each shell.`C:\Windows\System32\schtasks.exe /run /tn "[NAME OF TASK]"`So, mine were C:\Windows\System32\schtasks.exe /run /tn "HyperBash" & C:\Windows\System32\schtasks.exe /run /tn "HyperCMD"

And you're done! Download your favorite custom icons and enjoy!

![CMD and Bash running on Windows](https://haquor.files.wordpress.com/2019/03/multishells-14.gif)



