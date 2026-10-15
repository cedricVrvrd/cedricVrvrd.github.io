---
title: "La Panthère — optimising an existing site"
description: "Auditing and optimising a web agency's website: SEO, performance and accessibility."
date: 2022-08-11
draft: false
weight: 40
summary: "Taking over a web agency's website and fixing it: SEO, page weight, accessibility, and removing abusive SEO tricks."
categories: ["Web development"]
tags: ["OpenClassrooms", "SEO", "Accessibility"]
showTaxonomies: true
---

*Project from the OpenClassrooms Web Developer path, 2022.*

**No new site here: take an existing one, find what's wrong, and fix it.**

## The brief

La Panthère is a web design agency in Lyon whose website ranked poorly, loaded slowly and wasn't very accessible. The job: **audit the site, then optimise it** for SEO, performance and accessibility.

## What I fixed

- **SEO**: rewrote the `title` tag and meta description, put the heading structure back in order, declared the page language, and removed lists of links to web directories, an abusive "black hat" SEO technique;
- **Performance**: lighter, resized images, minified CSS and JavaScript, scripts loaded at the end of the page, more efficient font loading, libraries hosted with the site instead of a CDN;
- **Accessibility**: rewrote image alt text, added ARIA labels to social media links, fixed contrast issues (including white text on a white background), used semantic tags;
- validated the HTML and CSS with the W3C tools.

## Tech stack

HTML · CSS · Bootstrap · SEO · web performance · accessibility (WCAG)

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/panthere_optimis-/" target="_blank" rel="noopener" >}}
Live demo
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/panthere_optimis-" target="_blank" rel="noopener" >}}
Code on GitHub
{{< /button >}}
</div>
