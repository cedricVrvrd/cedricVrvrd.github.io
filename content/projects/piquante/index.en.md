---
title: "Piquante — a secure API"
description: "A Node.js / Express / MongoDB REST API for a hot sauce review app, with authentication and OWASP-inspired security measures."
date: 2022-11-26
draft: false
weight: 10
summary: "The only back-end project of my web developer training, and the closest to what I do today: a Node.js API where most of the work is about security."
categories: ["Web development"]
tags: ["OpenClassrooms", "Node.js", "Security"]
showTaxonomies: true
---

*Project from the OpenClassrooms Web Developer path, 2022.*

**An API where most of the work is invisible: authentication, access control and data protection.**

## The brief

Piquante is an app where users post hot sauces and rate them with likes or dislikes. OpenClassrooms provided the Angular front end. My job: **build the API behind it**, with a strong focus on security.

## What I built

- a complete REST API: create, read, update and delete sauces, plus likes and dislikes;
- user sign-up and login, with a **JWT** for every authenticated request;
- **ownership checks**: only the author of a sauce can edit or delete it, and the user ID is taken from the token, never from the client's request;
- image uploads with multer.

## Security

- passwords **hashed with bcrypt**, with an enforced password policy (length, upper case, digits, symbols);
- email addresses **pseudonymised with an HMAC** before storage: the database never holds them in clear text;
- HTTP headers hardened with **helmet**, input sanitised against **XSS**, **rate limiting** per IP address;
- every secret (database, signing keys) kept in **environment variables**, never in the code.

## Tech stack

Node.js · Express · MongoDB · Mongoose · JWT · bcrypt · crypto-js · helmet · express-rate-limit · multer · dotenv

## Why it matters today

Of all my web developer projects, this is the closest to where I'm heading now, DevSecOps: think first about what an attacker could do, then make it hard.

No live demo: an API needs a server and a database, which GitHub Pages doesn't provide.

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://github.com/cedricVrvrd/PIQUANTE" target="_blank" rel="noopener" >}}
Code on GitHub
{{< /button >}}
</div>
