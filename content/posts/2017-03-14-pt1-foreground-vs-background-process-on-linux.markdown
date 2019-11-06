---
author: No Content Found
date: 2017-03-14 01:35:38+00:00
draft: false
title: 'PT1: Foreground vs Background process on Linux'
type: post
url: /2017/03/14/pt1-foreground-vs-background-process-on-linux/
---

<blockquote>_Most commands issued from an interactive shell run in foreground. That basically means that you must wait for the executed command (or processus ) to stop before doing something else. For long/complex programs or scripts, the alternative is to run them in the background. This means that you can continue to work while the long program executes._

_The ampersand & at the end of a command does this. You can also use ctrl-Z to suspend a foreground command and throw it in the background with the bg command. You can thereafter manage these backgrounds tasks (jobs command), kill them, etc._

_Please note that the background command is not detached from your tty : there may be some cases when a background command waits for user input (see fg command to bring back a job to foreground). If you logout, background jobs may be also killed (see nohup for more details)._

What is background and Foreground processes in Jobs, Uriel, Dec 24 '14 at 20:34</blockquote>
