---
title: "WordPress: the update itself left a door open"
description: "WordPress 7.1.4 fixes a race condition in the core update process, exploitable without an account. CISA added it to its Known Exploited Vulnerabilities catalog on 3 November."
date: 2026-11-04
draft: false
summary: "For a few seconds during every update, a copy of WordPress sat at a predictable address. Attackers were watching for that moment. The flaw is fixed in WordPress 7.1.4 and CISA lists it as exploited."
tags: ["Tech Watch", "Web development", "WordPress", "Updates"]
---

**For a few seconds during every update, a full copy of WordPress sat at a guessable address.**

## What happened

On 28 October 2026, WordPress released version **7.1.4**, a security update that fixes 22 vulnerabilities. The most serious sits in the **core update process itself**: a race condition that can lead to remote code execution during the update window. It was reported by researcher Umut Bayram.

The mechanism is easy to grasp. During a full update, WordPress unpacks the new files into a temporary folder, `wp-content/upgrade/`. Before 7.1.4, that folder had a **predictable name** and was reachable from the web. It also contained WordPress's installer scripts. An unauthenticated attacker who "wins the race" against the end of the extraction can reach those files and run code on the server.

The window is very short: according to Wordfence, in lab conditions the vulnerable folder stayed reachable for only a few seconds. That did not stop attacks: Wordfence saw automated probing as soon as the fix was released, with some sources polling small groups of sites for roughly 14.5 hours to catch the right moment.

The flaw affects WordPress from version 4.7 through 7.1.3. It was assigned **CVE-2026-119977** (CVSS 8.1, high attack complexity). On 3 November, **CISA** added it to its Known Exploited Vulnerabilities (KEV) catalog.

## Why it matters

- **No account needed.** The attacker doesn't have to log in to WordPress.
- **The window comes back with every update.** Including automatic updates that nobody watches.
- **Exploitation is confirmed.** The KEV listing isn't based on a hypothesis.
- **Older branches are covered, but not all.** Fixes were backported to 4.7; versions 4.6 and earlier no longer receive security updates.

## What to take from it

- **Update to WordPress 7.1.4 (or the fixed version of your branch), then check the version number:** an automatic update doesn't always go through.
- **Block web access to `wp-content/upgrade/`** in the server configuration. It's an extra layer, useful even when everything is up to date.
- **Check the logs:** requests to PHP files under `wp-content/upgrade/`, or unfamiliar files, are a signal worth investigating.
- **An update is a sensitive operation, not just a fix.** While the protection is being installed, the system is briefly more exposed.

## Sources

- [WordPress 7.1.4 — official announcement (28/10/2026)](https://wordpress.org/news/2026/10/wordpress-7-1-4/)
- [Version 7.1.4 — WordPress.org documentation](https://wordpress.org/support/wordpress-version/version-7-1-4/)
- [CISA — adds a vulnerability to the KEV catalog (03/11/2026)](https://www.cisa.gov/news-events/alerts/2026/11/03/cisa-adds-one-known-exploited-vulnerability-catalog)
- [The Hacker News — WordPress flaw exploited after the patch](https://thehackernews.com/2026/10/wordpress-rce-flaw-draws-nearly-63000.html)
- [SecurityWeek — fresh WordPress vulnerability in attackers' crosshairs](https://securityweek.com/fresh-wordpress-vulnerability-in-attackers-crosshairs)
- [WebHostingToday — WordPress 7.1.4 (Patchstack analysis)](https://webhosting.today/2026/10/29/wordpress-7-1-4-fixes-22-flaws-one-in-the-core-update-process/)
