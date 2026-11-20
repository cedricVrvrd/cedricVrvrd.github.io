---
title: "The day Facebook vanished from the internet"
description: "On 4 October 2021, a maintenance command took Facebook, Instagram and WhatsApp offline for about six hours, and the tools to fix it went down too."
date: 2026-11-20
draft: false
summary: "A command meant to check network capacity disconnected all of Meta's data centers. The DNS servers then withdrew their own BGP routes, and engineers had to go on site to fix it."
tags: ["Friday Fun Fact", "Networking", "DevOps", "History"]
---

**On 4 October 2021, Facebook vanished from the internet. Not because of an attacker, but because of a maintenance command.**

## A routine command

At 15:39 UTC, Facebook, Instagram, WhatsApp, Messenger and Oculus became unreachable worldwide. Meta later explained what happened: during maintenance, a command meant to check the capacity of its backbone network (the network linking its data centers) disconnected every connection in that backbone.

An audit tool should have blocked the command. A bug got in the way.

## When DNS withdraws its own routes

Facebook's DNS servers lost contact with the data centers. They then told BGP, the protocol that announces Facebook's IP addresses to the rest of the internet, to withdraw those announcements.

The result: the DNS servers were still running, but nobody could find them anymore. No DNS answer meant no facebook.com, no instagram.com, no whatsapp.com.

## Locked out

The hardest part was still to come. Internal tools were unreachable and, according to Meta, even the emergency access went down with everything else. Engineers had to go to the data centers to work on the machines, which took time because of the physical security in place.

According to the New York Times, some access badges stopped working, and employees talked to each other over LinkedIn and Discord. Services came back that evening, after about six hours.

## What to take from it

- **Emergency access must be independent.** An out-of-band access that depends on the main network is useless the day that network fails.
- **A safeguard can have its own bugs.** No single command should be able to have consequences this large.
- **An outage is not always an attack.** Here, it was an internal mistake.

## Sources

- Meta Engineering, [« More details about the October 4 outage »](https://engineering.fb.com/2021/10/05/networking-traffic/outage-details/) (05/10/2021)
- CACM, [« What Caused the Facebook Outage »](https://cacm.acm.org/news/what-caused-the-facebook-outage)
- The Register, [« Facebook back online »](https://www.theregister.com/2021/10/04/facebook_back_online/) (04/10/2021)
- Silicon Republic, [« What brought down Facebook, WhatsApp and Instagram for six hours? »](https://siliconrepublic.com/?p=947340) (05/10/2021)
- AppleInsider, [« Facebook shows signs of life after hours-long outage »](https://appleinsider.com/articles/21/10/04/facebook-shows-signs-of-life-after-hours-long-outage) (04/10/2021)
