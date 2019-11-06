---
author: No Content Found
date: 2016-03-07 21:42:46+00:00
draft: false
title: moving forward
type: post
url: /2016/03/07/moving-forward/
---

so the next step moving forward is as follows

create c++ code to utilize the digital mars lightweight compiler found [here](http://www.digitalmars.com/ctg/ctgCompilingCode.html)



	  * Generator will then write C++ code to a file, including certain keywords such as listener IP & port.
	  * From there it will compile that file with dmc

Then it will advance into the binding step.

there are 2 options.

	  1. merge the byte code together through memory allocation
	  2. <del>read the byte code from the original executable, generate another c++ file that runs the byte code of the target program first, and then our malware. c++ file must be compiled</del>

i'll be going the manual way
