---
title: "Bubble Game — a small JavaScript game"
description: "A small JavaScript game: bubbles appear, you click to pop them, a counter keeps the score."
date: 2023-01-09
draft: false
weight: 70
summary: "A short JavaScript exercise: creating elements on the fly, handling clicks and animating bubbles with CSS."
tags: ["Projects", "Exercise", "JavaScript"]
---

**A tiny game in about thirty lines of JavaScript: pop the bubbles before they disappear.**

## The exercise

Bubbles of random size and direction float up the screen. Each click pops a bubble and adds to the score.

## What I practised

- **creating elements on the fly** in the DOM, at regular intervals;
- **events**: a click pops the bubble and updates the counter;
- clean-up: each bubble is removed from the page after a few seconds;
- a **CSS animation** whose direction is set from JavaScript through a CSS variable.

## Tech stack

JavaScript · DOM · events · CSS animations · CSS variables

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/bubbleGame/" target="_blank" rel="noopener" >}}
Live demo
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/bubbleGame" target="_blank" rel="noopener" >}}
Code on GitHub
{{< /button >}}
</div>
