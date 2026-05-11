---
layout: post
title: "Minecraft"
date: 2026-05-11 14:00:00 +0000
ctf: "HCSC'26"
category: "Other"
---

# Minecraft

## Solution

In this challenge we are given a plugin for a Minecraft server. Starting the server we can type in `/start` to start the challenge. We are then teleported to a random coordinate and a pattern is shown on the floor:

![Minecraft pattern](/writeups/hcsc26/images/image19.png)

We then need to use the `/tpguess <x> <y>` to guess the correct coordinate. We only have 5 minutes from the start and can only guess once. I first opened the given jar file in Jadx. While variable names were obfuscated it was not hard to reverse engineer. This was the most important class:

![Decompiled class code](/writeups/hcsc26/images/image20.png)

This class uses Mersenne Twister for PRNG. The state of this is then shown on the floor encoded in white and black blocks. To solve this challenge I needed to read the next state to get the correct coordinates. There are many ways to do this, but I used a mod called JS Macros. This allowed me to write a simple script in JS that read the states needed and calculated the correct coordinates to solve the challenge:

![JS Macros script](/writeups/hcsc26/images/image21.png)

![Solution command](/writeups/hcsc26/images/image22.png)

*(Fake flag is shown the VM is no longer available so the server is ran locally)*
