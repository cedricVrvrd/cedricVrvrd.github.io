---
title: "The scenario: Norrøn Voyages"
description: "The fictional company behind Heading North Lab: its business, its incident and why it needs to rebuild everything."
date: 2026-10-11
draft: false
weight: 10
summary: "A travel agency hacked in peak season, a partner bound by NIS2, one sysadmin to rebuild everything. Meet the fictional company behind the lab."
tags: ["Heading North Lab", "Scenario"]
---

**A travel agency hacked in peak season. A key partner ready to walk away. One admin to rebuild everything.**

> Norrøn Voyages is a fictional company, created as the scenario for this lab.

## The company

**Norrøn Voyages** is a French travel agency founded in 2012. Its 15 employees run small-group adventure trips to Iceland, the Faroe Islands and Norway: hiking, trekking, northern lights.

- **Hélène Marchand**, the founder, is a former hiking guide. Pragmatic and not technical, she wants concrete results and to understand what's at stake.
- **Bjarni**, the guide and coordinator, works from Reykjavik and needs remote access to the internal tools.
- **The sales team** travels a lot and uses the website and booking tools on the move.

The agency handles sensitive data: travellers' identities, passport copies, medical information for the treks, payments — all subject to GDPR.

## The starting point

Like many small companies, the agency's IT grew without a plan:

- **a single old server** doing everything;
- **a flat network**: every computer and server can reach every other one;
- **shared passwords** between colleagues;
- **a WordPress site edited directly in production**, with plugins rarely updated.

## The incident

Last spring, in the middle of the booking season, the WordPress website was **defaced through an outdated plugin**. It stayed offline for several days.

It wasn't bad luck: it was the logical result of the setup above. On a flat network with no updates and shared passwords, one weakness is enough.

## The trigger

The agency's main Norwegian partner, bound by the **NIS2 directive**, now requires security guarantees from its suppliers. Without them, the contract won't be renewed.

## My role

Hélène hires a DevOps systems administrator: me. The only technician, reporting directly to her. The mission: **rebuild the infrastructure properly, automate it, then be able to defend it**.

Next article: the plan.
