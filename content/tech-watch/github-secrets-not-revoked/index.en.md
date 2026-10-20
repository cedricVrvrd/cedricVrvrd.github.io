---
title: "543,699 GitHub secrets still work. Nobody revoked them."
description: "A study of 224 million public repositories shows that leaked credentials stay valid for years — because nobody revokes them."
date: 2026-10-11
draft: false
summary: "Out of 1.1 million credentials exposed on public GitHub repositories, 543,699 still worked in July 2026. The problem isn't the leak, it's the missing revocation."
tags: ["Tech Watch", "DevSecOps", "Secrets management", "GitHub"]
---

**Deleting a password from GitHub doesn't switch it off. 543,699 credentials prove it.**

## What happened

On 29 September 2026, Truffle Security published research based on The Stack v3, a dataset of public GitHub code collected for AI training: 224 million repositories and 58 billion files, crawled until August 2025.

The researchers found **1,103,438 exposed credentials**. In late July 2026, they tested each one against the service that issued it: **543,699 still worked**.

A few figures stand out:

- the oldest live credential is an **AWS key pushed in 2009**, still valid after 16 years;
- the median credential had been public for **784 days**;
- just under **200,000** live credentials were pushed **after** GitHub made push protection the default, in February 2024.

## Why it matters

The most interesting finding isn't the volume, it's the cause. Survival depends on **revocation**, not detection:

- tokens that their provider revokes automatically (GitHub, npm) are almost all dead — only 260 GitHub tokens and a single npm token were still live;
- database connection strings (MongoDB, Postgres, MySQL), which nobody revokes automatically, are almost all still live.

Push protection roughly halved the rate at which covered secrets reach public code. But, as the researchers put it, it "did not change what happens to a credential once it is there". And about half of live credentials are types that push protection does not block by default.

## What to take away

- **A published secret is compromised**, even if you delete the commit a minute later. Rotate it first, clean the history second.
- **Blocking future leaks doesn't fix past ones.** Scan your repositories' full history, especially anything committed before February 2024.
- **Prefer short-lived credentials.** Most of the leaked secrets would have expired harmlessly if they had a lifetime.
- **Check your providers.** Does the service you use revoke leaked keys automatically? If not, detection alone leaves the key working.

For Norrøn Voyages, the fictional company of my lab, this becomes a rule from day one of phase 6: no secret ever goes into Git, and any secret that does is rotated immediately.

## Sources

- [GitHub Repos Exposed 543,699 Credentials. Nobody Revoked Them. — Truffle Security (29/09/2026)](https://trufflesecurity.com/blog/github-repos-exposed-543699-credentials-nobody-revoked-them)
- [500,000 Active Credentials Left Exposed on GitHub — SecurityWeek (01/10/2026)](https://www.securityweek.com/500000-active-credentials-left-exposed-on-github/)
