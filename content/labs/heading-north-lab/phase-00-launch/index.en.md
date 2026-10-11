---
title: "Phase 0 — Why this lab"
description: "The scenario, the starting point and the target architecture of Heading North Lab."
date: 2026-10-13
draft: true
summary: "A travel agency hacked in peak season, a partner bound by NIS2, one sysadmin to rebuild everything. Here is the scenario, the starting point and the plan."
tags: ["Heading North Lab", "Phase 0", "Architecture"]
---

**A travel agency hacked in peak season. A key partner ready to walk away. One admin to rebuild everything.**

## Why one long-running project

I'm completing a Bachelor's in DevOps Systems Administration. Rather than stacking isolated exercises, I'm applying everything I learn to **one infrastructure**, on my own Proxmox server, phase after phase. Each new skill has to solve a real need of the same company — and each phase builds on the previous ones.

## The scenario: Norrøn Voyages

**Norrøn Voyages** is a French travel agency founded in 2012. Its 15 employees run small-group adventure trips to Iceland, the Faroe Islands and Norway: hiking, trekking, northern lights. Most of the team works at the head office; the sales staff travel a lot, and Bjarni, the guide and coordinator, works from Reykjavik.

The agency handles sensitive data: travellers' identities, passport copies, medical information for the treks, payments — all subject to GDPR.

**The incident.** Last spring, in the middle of the booking season, the WordPress website was defaced through an outdated plugin. It stayed offline for several days.

**The trigger.** The agency's main Norwegian partner, bound by the NIS2 directive, now requires security guarantees from its suppliers. Without them, the contract won't be renewed.

**My role.** Hélène Marchand, the founder, hires a DevOps systems administrator: me. The mission: rebuild the infrastructure properly, automate it, then be able to defend it.

> Norrøn Voyages is a fictional company, created as the scenario for this lab.

## The starting point

Like many small companies, the agency's IT grew without a plan:

- **a single old server** doing everything;
- **a flat network**: every computer and server can reach every other one;
- **shared passwords** between colleagues;
- **a WordPress site edited directly in production**, with plugins rarely updated.

The defaced website is not bad luck: it's the logical result of this setup. On a flat network, one compromised machine is one step away from all the others.

## The target

![Today's flat network next to the target architecture, segmented into VLANs behind pfSense](architecture-en.png)

The target is a segmented network: each zone is a separate VLAN, and **every flow between zones goes through the pfSense firewall**. Everything is blocked by default; each flow is opened explicitly, for a reason.

- **Administration**: the admin interfaces of Proxmox and pfSense are only reachable from here;
- **Servers / DMZ**: the WordPress site and its database, the only part exposed to the Internet;
- **Users**: the staff's workstations, which reach the website like any visitor;
- **VPN**: Bjarni and the sales team connect through the Internet; their encrypted tunnel ends on pfSense, which only lets them reach the services they actually need;
- **Monitoring / SIEM**: in its own VLAN. Logs from every zone arrive one way only, so that an attacker who compromises a server can't reach the SIEM to erase their tracks;
- **Offensive lab**: an isolated attack machine for the final phase. It may reach the DMZ during the phase 12 tests, never the Administration or Users zones.

This is a **plan, not something already built**. It will change as I build it, and every change will be explained.

## The 13 phases

| # | Phase | Norrøn Voyages' need |
|---|---|---|
| 0 | Launch | Present the project and the scenario |
| 1 | Architecture | Audit the existing setup: the flat network |
| 2 | Proxmox, VMs, network | Rebuild on sound foundations |
| 3 | Hardening | Never again the spring incident |
| 4 | Remote access | Bjarni must work safely from Reykjavik |
| 5 | WordPress | Reinstall the website properly |
| 6 | Git / GitHub | No more direct changes in production |
| 7 | Jenkins | Update the site without downtime |
| 8 | Docker | The same environment from test to production |
| 9 | Kubernetes | Handle the January booking peak |
| 10 | Terraform / Ansible | Disaster recovery: rebuild everything fast |
| 11 | Monitoring | Know about problems before customers do |
| 12 | Blue Team | Prove to the NIS2 partner that attacks are detected |

The final phase closes the loop: I'll attack the infrastructure I built and secured myself, and show what my detection catches.

## How I'll document it

Each phase follows the same structure: **the company's need → what I set up → what went wrong or what I learned → the next step**. Mistakes included: they are part of learning, and often the most useful part.

I share each step on [LinkedIn](https://www.linkedin.com/in/c%C3%A9dric-vervoord-07940915b/) every week, with the detailed version here.
