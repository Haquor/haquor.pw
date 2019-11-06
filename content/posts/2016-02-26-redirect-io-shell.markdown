---
author: No Content Found
date: 2016-02-26 04:49:52+00:00
draft: false
title: redirect i/o shell
type: post
url: /2016/02/26/redirect-io-shell/
---

building a shell that redirects output to listening system

also, need to be able to send commands through the shell.

    
    #include <string> 
    #include <iostream>
    #include <cstdio>
    #include <memory>
    
    std::string exec(const char* cmd) {
        std::shared_ptr pipe(popen(cmd, "r"), pclose);
        if (!pipe) return "ERROR";
        char buffer[128];
        std::string result = "";
        while (!feof(pipe.get())) {
            if (fgets(buffer, 128, pipe.get()) != NULL)
                result += buffer;
        }
        return result;
    }
    


[Source](http://stackoverflow.com/questions/478898/how-to-execute-a-command-and-get-output-of-command-within-c)

First, design basic shell functionality in a C++ project Gate

That code up there is obsolete. Uploaded the production files to github

https://github.com/Isonyx/Shell/blob/master/Shell/Shell.cpp

There were issues with process creation which were sorted,

also some problems debugging. The code should only be tested as an .exe otherwise argv will trigger issues.

ALMOSST where it needs to be.

I just can't work out piping input correctly to the process.

will read over a great resource tomorrow - https://msdn.microsoft.com/en-us/library/windows/desktop/ms682499(v=vs.85).aspx


