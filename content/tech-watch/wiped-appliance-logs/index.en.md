---
title: "Two attacks, one shared habit: wipe the logs"
description: "In the attacks on Ivanti Connect Secure and BeyondTrust Remote Support, disclosed in October 2026, attackers deleted or altered the logs on the compromised appliances."
date: 2026-10-20
draft: false
summary: "Ivanti Connect Secure and BeyondTrust Remote Support: two flaws, two attackers, and in both cases logs wiped or altered on the compromised device. Logs that stay on the box prove nothing anymore."
tags: ["Tech Watch", "Logging", "Monitoring", "VPN"]
---

**Two flaws, two different attackers, one shared habit: wipe the logs on the device they just broke into.**

## What happened

**Ivanti Connect Secure.** On 13 October 2026, Volexity disclosed a chain of three unknown flaws in this VPN appliance. The targeted device was fully patched at the time. The attacker gained the highest privileges (root), collected credentials and BitLocker recovery keys, then **altered the logs** to remove traces of their activity. Ivanti's own integrity checking tool doesn't detect this attack, because the code is only changed in memory.

**BeyondTrust Remote Support.** On 15 October 2026, Mandiant described the exploitation of a flaw in this remote support tool since late August. The attacker deployed a web shell, harvested stored credentials, and **deleted the appliance's logs throughout the intrusion**.

## Why it matters

These devices face the internet and sit in a privileged position in the network. Once an attacker is inside with the highest privileges, everything stored on the device is within reach, logs included.

So Mandiant recommends **streaming the appliance's logs to an external collection system** (a SIEM), and also keeping logs from the devices around it: firewall, proxy. It also notes that **a gap in forwarded logs** is in itself a strong sign of tampering.

## What to take away

- **Logs stored only on the compromised device prove nothing.** They need to leave it, continuously, before the attacker shows up.
- **Silence is a signal.** A source that suddenly stops sending logs deserves an alert, not a shrug.
- **"Up to date" doesn't mean "safe".** The Ivanti appliance was patched: only traces kept elsewhere can tell what really happened.
- **Cross-check your sources.** Logs from the firewall or proxy in front of the device keep a record the attacker can't change from the device itself.

## Sources

- [Ivanti Connect Secure zero-day actively exploited — CyberScoop (13/10/2026)](https://cyberscoop.com/ivanti-connect-secure-zero-day-actively-exploited/)
- [Attackers chained three Ivanti zero-days to gain root on fully patched VPN appliances — Help Net Security (14/10/2026)](https://www.helpnetsecurity.com/2026/10/14/ivanti-zero-days-gain-root-patched-vpn-appliances/)
- [ARMORY CASTLE exploits BeyondTrust — Mandiant / Google Threat Intelligence (15/10/2026)](https://cloud.google.com/blog/topics/threat-intelligence/armory-castle-exploits-beyondtrust)
