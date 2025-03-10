---
layout: post
title:  "My Home Server Setup"
date:   2025-03-10
categories: [self-hosting]
tags: [self-hosting]
---

I run a homelab on my small HP EliteDesk 800 G3 Mini, just because I like the learning experience and I always wanted to tinker with computers. 

The setup is quite basic:
- **OS**
    - Ubuntu Desktop 22.04 (I installed the desktop version because since it was my first time running Linux i wanted the safety net of a GUI in case all went to shit and I wanted to interact with the server with something other than the Command Line)

- **Docker and Docker Compose**
    - this is the bedrock of everything else. I run all my web services in Docker containers because they are so easy to run once you get the hang of it, and there is a huge community of people self hosting services this way.

I run just a couple services:

- **Portainer**
    - this is a popular container management application that allows to, you guessed it, spin up containers using a GUI in the browser.

- **Paperless-ngx**
    - this app is a digital archive to keep documents and reduce paper (the name is kind of telling anyway...)

- **Home Assistant**
    - I just recently discovered home automation and decided to give it a try. I think it's cool but still need to figure out use cases that actually make it useful and not just a gimmick. 