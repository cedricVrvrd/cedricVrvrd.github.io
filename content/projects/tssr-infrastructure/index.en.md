---
title: "TSSR infrastructure — Active Directory, GLPI and VLANs"
description: "Practical exam for the French TSSR diploma: a Windows domain, a GLPI ticketing server authenticated against AD, VLAN segmentation and a GPO, built from scratch."
date: 2026-01-14
draft: false
weight: 80
summary: "The practical exam of my systems and networks diploma: a Windows domain, GLPI authenticated against Active Directory, inter-VLAN routing and a startup GPO."
categories: ["Systems and networks"]
tags: ["TSSR", "Active Directory", "GLPI", "Cisco", "GPO"]
showTaxonomies: true
showTableOfContents: true
---

*Practical exam (ECF) of the Titre Professionnel Technicien Supérieur Systèmes et Réseaux (TSSR, RNCP level 5), 2026.*

**A fictional company, seven missions, and timestamped proof for each step.**

## The brief

The exam describes a fictional design studio, *CreativeFusion Studios*. Its problems are very ordinary ones: every application has its own passwords, support requests get lost between emails and phone calls, and all departments share one flat network. My job was to fix that, then prove every step with timestamped screenshots.

## What I built

**A Windows domain.** Windows Server 2022, Active Directory and DNS, with an OU structure that follows the org chart and keeps users and computers apart in each department. Then one DHCP scope per department.

**A ticketing server.** GLPI 11 on Debian 13 without a graphical interface: Apache, PHP-FPM, MariaDB. I moved the configuration, data and logs out of the web root and hardened the PHP session cookies.

**Single sign-on for support.** GLPI authenticates users against Active Directory through a dedicated service account, so employees log in with their usual domain password.

![GLPI's LDAP test: connection, bind and search all succeed](ldap-test.png)

**Network segmentation.** In Cisco Packet Tracer: six VLANs on a 2960 switch and a router-on-a-stick on a 2901, with DHCP relayed to the server. Every department gets its address automatically and can still reach the others.

![One ping per network from the HR workstation: TTL 127 means one hop through the router](inter-vlan-ping.png)

**Config backups.** Switch and router configurations copied to an FTP server.

**A GPO against static IPs.** A startup script, stored in SYSVOL and filtered on a security group, puts every network card back in DHCP mode.

![gpresult on the test workstation: the GPO is applied](gpresult.png)

## Naming

RFC 1178 recommends naming machines after a theme rather than their role. The domain controller is **MIDGARD**, the GLPI server **YGGDRASIL**, the test workstation **THOR**. For someone heading north, it seemed fitting.

## What I learned

Some of my mistakes are kept in the documentation on purpose. A wrong subnet mask, rejected by IOS. A switch backup that timed out, because a layer-2 switch has no IP address until you give it one. And a typo in the GPO script that I only spotted months later, while preparing this page. The GPO was applied, but one line of the script would have failed. Lesson learned: a script gets tested by hand on one machine before a GPO pushes it to all of them.

Looking back with a security mindset, I would also change several things on a real network: LDAPS instead of plain LDAP, HTTPS for GLPI, SFTP instead of FTP, and GLPI's default accounts changed on day one. The repository has the full list.

## Tech stack

Windows Server 2022 · Active Directory · DNS · DHCP · GPO · PowerShell · Debian 13 · Apache · PHP-FPM · MariaDB · GLPI 11 · LDAP · Cisco IOS · Packet Tracer

On GitHub, each mission has its own page: the need, the commands and configuration files (transcribed from my screenshots), and the proof that it works.

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://github.com/cedricVrvrd/tssr-infra-ad-glpi-vlan" target="_blank" rel="noopener" >}}
Documentation on GitHub
{{< /button >}}
</div>
