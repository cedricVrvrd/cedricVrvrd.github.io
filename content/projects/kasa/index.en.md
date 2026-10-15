---
title: "Kasa — a React app"
description: "A peer-to-peer home rental app built with React and React Router."
date: 2022-11-26
draft: false
weight: 20
summary: "The last project of my web developer training: a home rental app in React, built from reusable components."
categories: ["Web development"]
tags: ["OpenClassrooms", "React"]
showTaxonomies: true
---

*Project from the OpenClassrooms Web Developer path, 2022.*

**A home rental app, broken down into reusable components.**

## The brief

Kasa is a peer-to-peer home rental platform. It was the last project of the training: build the front end in **React** from a mock-up, with one page per listing generated from the data.

## What I built

- a home page listing the properties from a JSON data file;
- a **page for each property**, built from its ID in the URL, with a redirect to the 404 page if it doesn't exist;
- reusable components: photo **carousel**, **collapsible sections** for the description and amenities, **star rating**, tags;
- an "About" page and a 404 error page;
- navigation between pages with **React Router**.

## Tech stack

React 18 · React Router 6 · JSX · CSS · Create React App

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/kasa/" target="_blank" rel="noopener" >}}
Live demo
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/kasa" target="_blank" rel="noopener" >}}
Code on GitHub
{{< /button >}}
</div>
