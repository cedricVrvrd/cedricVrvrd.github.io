---
title: "An app \"for testing\" opened up Nextcloud servers"
description: "A flaw in Nextcloud's optional Built-in CODE app let anyone run commands on the server without an account. It was exploited from September 2026."
date: 2026-10-20
draft: false
summary: "A Nextcloud app described as meant for testing let anyone run commands on the server without logging in. Attackers planted web shells, and disabling the app wasn't enough."
tags: ["Tech Watch", "DevOps", "Nextcloud", "Patching"]
---

**An optional app, described as meant for testing, was all it took to take over Nextcloud servers.**

## What happened

Nextcloud offers an app called **"Collabora Online - Built-in CODE Server"** (`richdocumentscode`), which downloads and runs an online office suite directly on the Nextcloud server. Its listing describes it as meant for local testing, personal use or small teams.

Up to version 26.4.302, one of the app's scripts placed part of the requested URL inside a system command. The result: **a single request, with no account, could run commands on the server** (CVE-2026-110447). The attack only worked at a specific moment: when the built-in document server was down, for example after a restart, an upgrade or a crash.

The first attacks show up in logs on **10 September 2026**. Attackers planted PHP **web shells** in the app's folder. The fix, version 26.4.303, was released on 11 September.

## Why it matters

Two details make this case worth a closer look:

- **Disabling the app wasn't enough.** Its files stayed on the server and remained reachable. The vendor is clear: update it or remove it.
- **Exploitation started the day before the fix.** A server updated afterwards is no longer vulnerable, but a web shell planted earlier is still there.

## What to take away

- **Every installed extension is part of the attack surface**, even an optional one, even one you rarely use. If you don't need it, remove it.
- **A "for testing" component has no place in production.**
- **Disabled is not removed.** As long as the code is on disk, it can be called.
- **Patching doesn't clean up.** After an exploited flaw, you also have to look for traces: here, `shx*.php` files in the app's folder and suspicious requests in the logs since 10 September.

## Sources

- [Hackers Backdoor Nextcloud Servers Through Critical Flaw in Collabora's Built-in CODE App — The Hacker News (14/10/2026)](https://thehackernews.com/2026/10/hackers-backdoor-nextcloud-servers.html)
- [Security advisory GHSA-g3vx-3m76-fghh — Collabora Online (GitHub)](https://github.com/CollaboraOnline/online/security/advisories/GHSA-g3vx-3m76-fghh)
- [Vulnerability in Nextcloud app allowed attackers to plant web shells — SC Media](https://www.scworld.com/brief/vulnerability-in-nextcloud-app-allowed-attackers-to-plant-web-shells)
