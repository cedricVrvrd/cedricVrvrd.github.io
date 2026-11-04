---
title: "Interview with $6.3 Billion"
description: "The biggest crypto theft in history started with a fake job interview. A look at the report Binance published on November 3, 2026."
date: 2026-11-04
draft: false
summary: "A fake recruiter, a fake CEO, a \"coding assignment\" and a token found on a work computer: how $6.3 billion left Binance, according to its own report."
tags: ["Friday Fun Fact", "Social engineering", "Supply chain", "News"]
---

**A series that needs no screenwriter. On October 29, 2026, about $6.3 billion left Binance's wallets. It all started with a job interview.**

On November 3, Binance published its incident report. The FBI blames North Korea, which denies it. Here is the season, episode by episode.

## The episodes

- **June, *The Homebrew*.** An engineer installs a fake version of Homebrew, the software installer for Mac. Binance detects it, replaces his computer and rotates his credentials, but the report says the wallet team was already exposed.
- **September, *The Interview*.** Another engineer is approached about a job by a fake "project director" on a job platform (LinkedIn, according to Fortune). The first interview is on video with a fake HR rep, who shows a social media account full of photos to build trust. The second is with a fake CEO, who has him download a "coding assignment". He runs it on his work computer: it is malware, and the endpoint security tools don't catch it right away.
- **October 20, *The Assistant*.** From that computer and an internal AI tool, the attackers reach the machines of two wallet-team engineers.
- **October 29, *The Token*.** One of those machines holds a token, a kind of digital badge, that allows deploying containers (small runtime environments) on Binance's infrastructure. The attackers use it to trigger the theft. The first withdrawals start around 9:05 pm Paris time, and most of the funds leave in about twenty minutes.

## What we don't know yet

Binance mentions an "advanced transaction-authorization method" without detailing it. On Ethereum the attackers used EIP-7702, a feature that lets a wallet hand its operations over to a program. But on other networks the funds left through ordinary signatures: analysts think Binance's signing system was compromised. The investigation continues. Binance also says it blocked 57 similar North Korea-linked attempts since January 2026.

## The takeaway

The weak point wasn't the vault but a developer's laptop and overly broad internal access.

- Code from a recruiter belongs in a disposable virtual machine, never on your work computer.
- A token should carry only the rights it needs.
- An internal tool shouldn't be a gateway to other machines.

**Sources**: The Register, BleepingComputer, Fortune, Axios, CoinDesk (November 3, 2026); TRM Labs.
