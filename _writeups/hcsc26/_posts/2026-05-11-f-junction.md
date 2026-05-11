---
layout: post
title: "F-junction"
date: 2026-05-11 13:00:00 +0000
ctf: "HCSC'26"
category: "Reverse"
---

**Files:** junction, libjunction.so

## Solution

We were given an ELF file (junction) and a library (libjunction.so). The library exports 2048 functions named junk_n and another 2048 named junc_n. According to the challenge description, these are the relevant formulas:

![Challenge formulas](/writeups/hcsc26/images/image7.png)

The junction ELF just calls the junk functions in the order given by formula A. This is meant to serve as a tutorial as stated by the description. I opened up the lib with Binary Ninja and analyzed the file for a bit. All junc functions manipulate a buffer and a cursor as seen in the example here:

![Function analysis](/writeups/hcsc26/images/image8.png)

I created a simple C program that would dynamically load in the lib file and call the junc functions in the order given by formula B:

![C program code](/writeups/hcsc26/images/image9.png)

Running this application, I got a result full of junk characters:

![Initial output](/writeups/hcsc26/images/image10.png)

This meant that something was still wrong. I dug around a bit more in the lib file and found this function:

![Buffer initialization function](/writeups/hcsc26/images/image11.png)

It sets the buffer to some starting value, this meant that me setting it to 0 with memset was ruining the starting state of the buffer. After removing that line and running again I got this output:

![Better output](/writeups/hcsc26/images/image12.png)

This approach looked more promising, but it still wasn't quite right. I stayed stuck here for a while, suspecting my function calling order was incorrect. The breakthrough finally came while debugging with gdb. Initially, I didn't see anything unusual, but I eventually noticed that the output string changed after the debugging session ended. The fact that running the program under a debugger yielded a different result immediately raised my suspicions. 

I began searching for anti-debugging checks within the library and discovered several subfunctions being called at the start of almost every junc call. Such as this one:

![Anti-debugging code](/writeups/hcsc26/images/image13.png)

Analyzing these functions took some time, but the takeaway was clear: the library was packed with diverse anti-debugging mechanisms. The most significant check is shown below:

![Process name check](/writeups/hcsc26/images/image14.png)

This function specifically checks if the process is being executed by Python. While I could have written a Python script to call the functions properly, I tried a workaround first: I simply renamed my compiled executable to python. To my surprise, this was enough to fool the check:

![Solution output](/writeups/hcsc26/images/image15.png)
