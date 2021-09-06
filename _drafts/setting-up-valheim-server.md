---
layout: post
title:  "Setting up a Valheim server on Linux"
date:   2021-03-12 19:25:00 -0600
author: Leo
categories: gaming linux
---

Recently started playing Valheim with some friends and it really sucks to host the game locally, especially when the number of people playing on the same server starts to grow and you don't want to have your PC running all day long.

I have an Amazon LightSail instance that I use for random projects and it turned out to be a perfect place to host the game. Follow this short guide to see how to do it.



## Requirements
- Linux server: I am using Debian for this guide
- Copy of Valheim on Steam
- Some background Linux knowledge



## Getting Valheim Server
Normally you could just download Valheim Dedicated Server directly off Steam and start the server but that requires the Steam client and a display to click on things. 

Since we're trying to do this on a headless server that won't do. Luckily for us, it doesn't look like Valheim server requires the steam client to run so we can just download it on any Linux computer with Steam and then copy the files over to the server.



## Copy files to VPS

On Debian, Steam installs games by default under `/home/username/.local/steam/common/steamapps/` so we can `tar` and `scp` the whole Vlaheim directory to our headless server.

```bash
tar -czf /home/username/.local/steam/common/steamapps/valheim valheim.tar.gz
scp ./valheim.tar.gz user@hostname:/home/user/
```

Then at the server we can unpack and move it to `/opt/valheim`.

```bash
tar -zxf valheim.targ.gz
mv -P ./valheim /opt/valheim
cd /opt/valheim
```



## Configure server





## Open up ports

