---
title: "Kanap — an e-commerce site in JavaScript"
description: "The dynamic part of a sofa shop website in JavaScript: catalogue, product page, cart and checkout."
date: 2022-09-30
draft: false
weight: 30
summary: "Making an e-commerce site dynamic in plain JavaScript: catalogue loaded from an API, cart, form validation and checkout."
tags: ["Projects", "OpenClassrooms", "JavaScript"]
---

**A sofa shop website, made dynamic in plain JavaScript, no framework.**

## The brief

Kanap sells sofas online. The HTML and CSS pages were provided, along with an Express API. My job: **write all the JavaScript** connecting the two.

## What I built

- the catalogue, loaded from the API with **fetch** and inserted into the page;
- a product page generated from the ID in the URL, with colour and quantity selection;
- a **cart stored in localStorage**: identical items merged, quantities updated, items removed, total calculated;
- checkout **form validation** with regular expressions;
- sending the order to the API, then a confirmation page showing the order number.

## About the live demo

Originally, the site called the Express API running locally. To publish it on GitHub Pages, which only hosts static files, I adapted a **demo version**: the catalogue is read from a JSON file and checkout is simulated (the order number is generated in the browser; nothing is sent). The original code, back end included, is unchanged in the repository.

## Tech stack

JavaScript · DOM · Fetch API · localStorage · regular expressions · HTML · CSS

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/P5-Dev-Web-Kanap/" target="_blank" rel="noopener" >}}
Live demo
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/P5-Dev-Web-Kanap" target="_blank" rel="noopener" >}}
Code on GitHub
{{< /button >}}
</div>
