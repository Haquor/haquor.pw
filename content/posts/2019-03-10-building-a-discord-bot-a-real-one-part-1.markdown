---
author: Haquor
date: 2019-03-10 05:49:20+00:00
draft: false
title: Building a Conversational AI Discord Bot
type: post
url: /2019/03/10/building-a-discord-bot-a-real-one-part-1/
---

"Bot" is a word we throw around a lot these days.

Aimbots, spam bots and the occasionally nets of bots. I think it's time we wake up. Bots shouldn't be dumb. To fight back against those who think our bots just do what we tell them, we're going to code one with sentience. (Just kidding). (Sorta)

We're going to create one that learns.
<!--more-->

A quite popular open source software library for machine learning, TensorFlow, has become industry standard for rolling out simple ML scripts.

So we're gonna use the TensorFlow library, and Python 3.6 to code a quick little Discord bot. Some thngs to remember before I begin:

I don't know Python, I'm unfamiliar with TensorFlow, and I know the bare minimum about machine learning. But fuck it. Let's build something.


### Platform


I'm using Windows 10 64-bit with WSL (Windows 4 Linux SubSystem) and Python 3.6. Visual Studio Code is the IDE. Code will be pushed to my Github repo.


### The Discord Part


So [DevDungeon](https://www.devdungeon.com/content/make-discord-bot-python) has a nice little tutorial on this. We're going to create a Discord server to test our bot on and an "app. If you wanna make use of the Discord API, you start by [enabling Developer Mode](https://discordia.me/developer-mode) on your Desktop client.

It's kinda cool that Discord has built in support for bots isn't it? So many sites spend 100s of hours and write 100s of lines of ineffective code to ban bots, and Discord gives control of the botting scene to the users.

So here's a breakdown on their bots. Server bots have dedicated bot and can only be invited by a server manager. Selfbots are bots that you run by using the Discord API but NOT the applications page (and are illegal) . And Userbots are bots that run through a regular account.

The general idea is if you're gonna use a bot, go legit, and register it through discord. (Lmao)

    
    python3 -m pip install discord.py==0.16.12


Now let's download that sample code and get things functional. Create an app, import your token, and run that song of a gun.

Logged in as
レイン, ｌａｉｎ れいん
541843909974687756

Great. But is still can't do anything. Let's set the discord part aside until we get TensorFlow recognizing images. Then we'll build that in.


### The TensorFlow Part


So the idea is that Tensor Flow uses things called tensors. Tensors are basically multidimensional data arrays. Go back to physics and remember a vector as a _scalar maginitude_ that also has _direction_.

A tensor, is the mathematical representation of that physical idea that is characterized by _magnitude_ and **multiple** _directions_

    python3 -m pip install tensorflow

Next post we're going to get into a little bit of a top down overview of how TensorFlow works, what we'll use those multidimensional arrays for and how we can approach the idea of "training" our robot's neural network gainst different models.


