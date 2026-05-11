---
layout: post
title: "Demoscene"
date: 2026-05-11 12:00:00 +0000
ctf: "HCSC'26"
category: "Reverse"
---

# Demoscene

**Files:** Demoscene.exe

## Solution

The Demoscene.exe is a 64 bit windows executable. Upon running it the task for this challenge becomes clear. The flag is visible in the background, but it is hidden by the text in front of it.

I tried searching for the flag string, but that did not work. I ran the executable using x64dbg. To get started I searched for the "HCSC 2026" string which I was able to find.

![Initial state with hidden flag](../images/image1.png)

I tried searching for the flag string, but that did not work. I ran the executable using x64 dbg. To get started I searched for the "HCSC 2026" string which I was able to find.

Simply patching that part of the memory to be an empty string yields this result:

![After patching text](../images/image3.png)

With a bit of trial and error I was able to find where the boxes position was being set.

![Finding box position code](../images/image5.png)

After patching those values, I got this result:

![After patching box position](../images/image7.png)

Now I just needed to resize the window. To do this I found the window creation call at the start of the main function and patched it. With this version I was able to see the full flag:

![Full flag revealed](../images/image8.png)
