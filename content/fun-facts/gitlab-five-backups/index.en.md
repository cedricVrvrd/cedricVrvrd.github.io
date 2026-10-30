---
title: "GitLab, 2017: five backups, none of them worked"
description: "The night a GitLab.com engineer wiped the wrong database, and the team found out its backups didn't work."
date: 2026-10-30
draft: false
summary: "A command run on the wrong server, 300 GB gone, and five backup methods, none of which worked. GitLab was saved by a copy taken by hand, six hours earlier, for something else entirely."
tags: ["Friday Fun Fact", "DevOps", "Backups", "History"]
---

**On 31 January 2017, GitLab.com lost six hours of data. Not because of a hacker: because of a command run on the wrong server.**

## A long evening

That evening, the GitLab.com team was already struggling with an overloaded database, probably caused by spam. Replication between the primary server, `db1`, and its standby, `db2`, had fallen behind. To restart it, an engineer decided to wipe `db2`'s data directory.

Around 23:30 UTC, the command ran. But the session was open on `db1`, the production server.

The engineer noticed a second or two later and stopped it. Too late: around **300 GB of data** were already gone.

## Five safety nets, all with holes

The team turned to the backups. That's when the evening took a turn. GitLab summed it up in a public message: *"out of 5 backup/replication techniques deployed none are working reliably or set up in the first place"*.

- **Daily backups** to S3 storage used a version of the `pg_dump` tool (9.2) that didn't match the database (PostgreSQL 9.6). They had been failing for a while, and the S3 bucket was empty.
- **Alert emails** reporting those failures were rejected by the mail server, because DMARC wasn't set up for them. Nobody ever received them.
- **Disk snapshots** on Azure were enabled for other servers, but not for the databases.
- **Replication** was precisely what had broken, and the standby had just been wiped too.

## Saved by a copy made for something else

One chance remained: a disk snapshot taken **by hand six hours earlier** by an engineer, to feed the staging environment. It was never meant as a backup, yet it's what made the restore possible.

Copying it back to production took around 18 hours, on slow disks. The toll: six hours of lost data, at least 5,000 projects, 5,000 comments and 700 new user accounts. The Git repositories themselves, stored elsewhere, were untouched.

A rare detail: GitLab did all of this in public. A shared document tracked progress minute by minute, and the restore was **streamed live on YouTube**, with up to 5,000 viewers.

## What every sysadmin will recognise

A backup you've never restored is just a hypothesis. And an alert nobody receives doesn't exist. In the list of fixes GitLab published afterwards, one line says it all: **automate testing of backup recovery**.

## Sources

- [Postmortem of database outage of January 31 — GitLab (10/02/2017)](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)
- [GitLab.com melts down after wrong directory deleted, backups fail — The Register (01/02/2017)](https://www.theregister.com/2017/02/01/gitlab_data_loss/)
