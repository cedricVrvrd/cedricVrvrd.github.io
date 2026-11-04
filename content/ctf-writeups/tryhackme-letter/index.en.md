---
title: "TryHackMe — Letter: an OSINT investigation from a damaged letter"
date: 2026-11-04
draft: false
description: "Write-up of the TryHackMe Letter room: tracking down a person from a handwritten note and a damaged newspaper clipping. The method, no spoilers."
summary: "A soaked envelope, a torn newspaper clipping, a personal note: how I approach an OSINT puzzle to end up at one specific person. The method, not the answer."
tags: ["CTF", "TryHackMe", "OSINT", "Write-up"]
---

## The room in a nutshell

**Letter** is an OSINT (open-source intelligence) challenge on TryHackMe. You play a mail carrier on an ordinary Monday morning. One envelope catches your eye: it is battered, full of holes, the address is barely legible, and your colleagues write it off as lost mail. Something about it nags at you anyway. Inside, you find a damaged newspaper clipping with whole sections missing, and a short handwritten note that is clearly personal.

**Objective**: using the clues in the zip file, find the **full name and age** of the person mentioned in the note. The flag has a fixed format, `THM{Name_Surname_age}`, with only the first letters capitalised.

> **Why no flag here?** TryHackMe's rules do not allow publishing flags, answers or step-by-step walkthroughs for rooms that are still active. So this article covers my **approach** and what I took from it. It does not give the answer, nor the names, places or dates that would let you guess it.

## What's in the file

- **The note**: an affectionate message to a relative. Its real value is two clues about the person being sought: one related to their age, one related to their place within a group.
- **The newspaper clipping**: the paper's name is readable, several headlines are partly readable, and the central article is badly damaged.
- **The envelope**: too damaged to give me anything usable.

## My method

1. **Take inventory before searching.** I re-read the brief, the note, the clipping and the envelope, and write down what is certain, what is partial and what is only hinted at.
2. **Turn the note into filters.** The note's two clues are not for searching: they are for **telling candidates apart** later. I set them aside as checkable criteria.
3. **Find the most solid anchor in the clipping.** You cannot rebuild a damaged document directly. What is readable (the paper's name, a thematic keyword, a geographic area) becomes a foothold to find the original article elsewhere.
4. **Search with few words, but the right ones.** A handful of well-chosen keywords, taken from what was readable, led me to a local-history page reproducing the original article.
5. **Go from the event to the people.** Once the event is identified, I look for a source listing the people involved along with their ages.
6. **Apply the note's filters.** Among those people, only one profile satisfies both criteria set in step 2.
7. **Check the format before submitting.** Exact spelling of the name as it appears in the source, hyphens, capitalisation, order of elements: the flag format is strict.

## What I took from it

- **One clue to search, one to tell candidates apart.** Separating the two keeps you from drowning in results.
- **Start from what is readable.** With a degraded document, don't guess the missing content: look for the original.
- **Local sources are valuable, but not enough on their own.** A local-history page can hold exactly the detail you need; it is still one source among others, to be cited and cross-checked whenever possible.
- **Format details matter.** Capitalisation, hyphens, ordering: in OSINT as in system administration, a small formatting slip can invalidate a correct result.
- **Ethics don't stop at the CTF.** Here the investigation is about historical events. In a real setting, identifying a living person from open sources raises genuine privacy and legitimacy questions.

## Skills used

Document analysis, advanced searching, source correlation, careful verification, respect for the platform's rules.

*TryHackMe room "Letter".*
