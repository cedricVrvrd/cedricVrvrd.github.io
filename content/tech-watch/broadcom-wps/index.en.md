---
title: "Routers and ISP boxes: a Wi-Fi flaw some models will never fix"
description: "Broadcom's old WPS module, found in routers and ISP boxes from many brands, can be exploited within radio range without the Wi-Fi password. Broadcom did not assign a CVE."
date: 2026-10-20
draft: false
summary: "A flaw in Broadcom's old WPS module affects routers and ISP boxes from many brands. It can be exploited within radio range, without the Wi-Fi password. No CVE, and no fix for some older models."
tags: ["Tech Watch", "Networking", "Wi-Fi", "End of life"]
---

**No Wi-Fi password needed. Being within radio range is enough.**

## What happened

On 16 October 2026, at the Hexacon conference, researcher Quentin Kaiser presented a flaw in **WPS Monitor**, Broadcom's old component that handles WPS — the button that lets you connect a device to Wi-Fi without typing the password.

This component doesn't properly check the size of the WPS messages it receives and reassembles. An attacker **within Wi-Fi range**, **without knowing the password** and without going through WPS pairing, can trigger memory corruption. The researcher demonstrated controlled memory disclosure and **code execution** on the device. The exact consequences depend on the model and its firmware.

The list of affected products, which isn't exhaustive, includes devices from many brands: ARRIS, Arcadyan, Askey, Cisco, Comtrend, Huawei, Netgear, Nokia, TP-Link, ZTE, Zyxel… For some models the vulnerability is confirmed; for others, it still needs checking against the firmware.

## Why it matters

- **Broadcom did not assign a CVE.** The company says it replaced this component in 2018 and considers the affected products obsolete or outside its support window.
- **Turning WPS off isn't always enough.** According to the researcher, the settings toggle may leave the vulnerable component running.
- **Some devices will never get a fix.** The oldest products, based on the eCos system, sometimes have no update path at all.

## What to take away

- **A setting is not a fix.** Unticking an option doesn't guarantee the vulnerable code is gone.
- **Network hardware has an expiry date.** A device that no longer gets updates stays vulnerable for life: replace it.
- **The ISP box is part of your network.** The ISP or manufacturer has to ship the update, but it's up to you to ask for it.
- **Radio range is attack surface.** Wi-Fi goes through walls: a flaw that needs no password can be attacked from the pavement.

## Sources

- [Broadcom WPS — Quentin Kaiser, Hexacon 2026 talk (16/10/2026)](https://qkaiser.github.io/broadcom-wps)
- [Weekly Security Intelligence Briefing, week of 2026-10-19 — Tech Jacks Solutions](https://techjacksolutions.com/security/briefing/weekly-security-intelligence-briefing-week-of-2026-10-19/)
