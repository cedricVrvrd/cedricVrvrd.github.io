---
title: "11 lines of code that broke the web"
description: "March 2016: a developer pulled his packages from npm, and thousands of projects stopped building."
date: 2026-11-13
draft: false
summary: "In 2016, the removal of more than 250 npm modules, including left-pad, an 11-line function that pads text with spaces, made installs fail for thousands of projects."
tags: ["Friday Fun Fact", "DevOps", "Supply chain", "Development"]
---

**On 22 March 2016, an 11-line function vanished from the internet. A few hours later, thousands of projects couldn't install.**

## A tiny module

`left-pad` does one thing: add characters, usually spaces or zeros, to the left of a string to reach a given length. Eleven lines of JavaScript, published on npm, the public JavaScript package registry. So simple nobody gave it a thought: thousands of projects used it, directly or, more often, through other packages. Among them, Node and Babel.

## The removal

After a dispute, its author, Azer Koçulu, pulled more than 250 of his modules from npm, `left-pad` included. The moment the package disappeared, every install depending on it failed: one missing package in the chain is enough to block an entire build.

## The comeback

Laurie Voss, npm's CTO, then restored a version of `left-pad`, after a new maintainer asked for it. Within hours, thousands of projects were repaired. Above all, the incident made visible something few people saw: a modern project depends on hundreds of small packages written by strangers.

## What to take from it

What you install, you depend on. A lock file (`package-lock.json`) pins versions. An internal mirror or a cache of critical dependencies keeps a copy if the supplier removes a package. In a CI/CD pipeline, this is a real reliability question, not only a security one.

## Sources

- [How one developer just broke Node, Babel and thousands of projects in 11 lines of JavaScript — The Register (23/03/2016)](https://www.theregister.com/2016/03/23/npm_left_pad_chaos/)
