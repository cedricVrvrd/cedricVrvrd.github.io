---
title: "The worm that wanted to count"
description: "1988: a student wanted to measure the size of the Internet. His program knocked part of the network offline."
date: 2026-11-06
draft: false
summary: "On 2 November 1988, a Cornell student released a program meant to measure the Internet. A mistake made it uncontrollable. The first large-scale worm, and the first conviction of its kind in the US."
tags: ["Friday Fun Fact", "Cybersecurity", "History", "Malware"]
---

**On 2 November 1988, a student launched a program to count the machines on the Internet. A few hours later, part of the network had stopped responding.**

## An experiment, not an attack

Robert Tappan Morris was a computer science student at Cornell. He launched the program from a computer at MIT, which he accessed remotely from Cornell. According to the FBI, the goal was to measure the size of the Internet, then around 60,000 machines. The program copied itself from machine to machine using known Unix flaws, including `sendmail` and `fingerd`, plus weak passwords.

## The mistake that changed everything

The worm was meant to install itself once per machine. But Morris worried an administrator could fool it by answering "already infected". So he made the worm copy itself again from time to time anyway. The result: machines ended up running many copies, slowed to a crawl, and refused new connections. Administrators sometimes couldn't even log in to intervene.

The worm destroyed and stole no data. The damage came from overload. About 6,000 machines affected, roughly 10% of the network, is the figure often quoted, but it remains a disputed estimate.

## The aftermath

Morris was the first person convicted in the US under the 1986 Computer Fraud and Abuse Act. He later became a professor at MIT. The incident also led to the creation of an incident response team, the future CERT.

## What to take from it

A safeguard added out of caution can become the cause of the problem. And a known but unpatched flaw is still a flaw: weak passwords and out-of-date services did the job more than thirty years ago, just as they do today.

## Sources

- [Morris worm — Wikipedia](https://en.wikipedia.org/wiki/Morris_worm)
- [Morris worm — Tom's Hardware, relaying the FBI retrospective](https://www.tomshardware.com/tech-industry/cyber-security/on-this-day-in-1988-the-morris-worm-slithered-out-and-sparked-a-new-era-in-cybersecurity-10-percent-of-the-internet-was-infected-within-24-hours)
- Eugene Spafford, "The Internet Worm Program: An Analysis" (Purdue, 1988)
