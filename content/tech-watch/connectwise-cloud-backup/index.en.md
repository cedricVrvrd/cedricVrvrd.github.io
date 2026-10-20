---
title: "A backup app opened up 162 Microsoft 365 tenants"
description: "Using a credential stolen from ConnectWise, attackers signed in to Microsoft 365 tenants as an application, without going through a single user account."
date: 2026-10-20
draft: false
summary: "The attackers didn't hack a single account: they signed in as ConnectWise's backup app, already trusted by its customers. User MFA never came into play."
tags: ["Tech Watch", "Cloud", "Microsoft 365", "Third parties"]
---

**The attackers didn't steal a single user password. They signed in as a backup app.**

## What happened

**ConnectWise Cloud Backup** (formerly SkyKick) backs up its customers' Microsoft 365 data: mail, OneDrive, SharePoint, Teams. To do that, each customer has authorised the app to access its tenant.

On **15 October 2026**, between 06:13 and 08:34 UTC, attackers used one of the app's credentials, stolen from the vendor, to sign in **as the application** to customer tenants, from a single IP address and in an automated way. As of 16 October, Huntress had confirmed unauthorised sign-ins in **162 tenants**. According to a later update, the address attempted sign-ins to nearly 1,000 tenants and succeeded in over 300.

In about fifty tenants monitored by Huntress, ConnectWise apps assigned themselves admin roles, mostly Exchange Administrator. In at least one case, one of them gave itself **Global Administrator**, then added new secrets to two other apps: a way back in for later.

ConnectWise shut down access to the service on 17 October. The vendor says it has no indication so far that backed-up data was compromised.

## Why it matters

A sign-in "as an application" involves **no user**. So there's no password to type and no MFA prompt to approve. Protections designed for accounts simply don't apply.

And a backup app, by design, can reach almost everything. It concentrates read access to the whole organisation. Microsoft describes it as an active supply chain attack.

## What to take away

- **A third-party app is an identity in its own right**, often with more rights than any employee. Know which apps can access what, and remove the ones you no longer use.
- **MFA protects accounts, not apps.** App sign-ins and role changes deserve the same monitoring as admin accounts.
- **Disable rather than delete.** Huntress recommends disabling the affected app without deleting it, to keep the history, then reviewing every secret added to apps since 13 October.
- **A supplier's security is part of yours.** That's exactly what regulations like NIS2 ask for.

## Sources

- [ConnectWise (SkyKick) Vendor Credentials Abused in M365 Attacks — Huntress (16/10/2026)](https://www.huntress.com/blog/vendor-credential-enables-unauthorized-access)
- [Hackers breach Microsoft 365 tenants via ConnectWise supply chain attack — BleepingComputer (17/10/2026)](https://www.bleepingcomputer.com/news/security/hackers-breach-microsoft-365-tenants-via-connectwise-supply-chain-attack/)
- [ConnectWise Cloud Backup Compromise in Microsoft 365: What Happened and What to Do Now — Security Boulevard](https://securityboulevard.com/2026/10/connectwise-cloud-backup-compromise-in-microsoft-365-what-happened-and-what-to-do-now/)
