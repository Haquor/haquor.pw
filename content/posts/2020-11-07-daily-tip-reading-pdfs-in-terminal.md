---
title: "2020 11 07 Daily Tip Reading Pdfs in Terminal"
date: 2020-11-07T18:51:20-05:00
draft: true
---

To read PDFs in terminal, we will utilize the less command.
Less is a file pager, which is a fancy way of saying it lets you view files in terminal.
Unfortuanately though, less alone can't parse PDF files into anything less than a jumble of binary garbage.

We will use an "input filter", or add-on if you will to run less data through the "pdftotext" package.
PDFTOTEXT on its own can be run against the file, but less integration is far more convenient.

1. Download and install pdftotext
Fetch and install the *pdftotext* package through your respective package manager.
	brew install pdftotext (MacOSX)
	apt-get install pdftotext (Ubuntu)

2. Add LESSOPEN to .zshrc.
Keep in mind, if you don't use ZSH, you'll need to create a variable in the config file for whatever shell you prefer.
	export LESSOPEN="|/usr/local/bin/lesspipe.sh %s" LESS_ADVANCED_PREPROCESSOR=1

3. Ensure lesspipe.sh is executable
	chmod +x /usr/local/bin/lesspipe.sh

For good measure, reinitialize your terminal, and you'll be free to test it out on a PDF
	less NuclearLaunchCodes.pdf
