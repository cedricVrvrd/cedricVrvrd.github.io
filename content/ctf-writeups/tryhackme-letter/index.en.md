---
title: "TryHackMe — Letter: an OSINT investigation from a damaged letter"
date: 2026-11-04
draft: false
description: "Write-up of the TryHackMe Letter room: tracking down a person from a handwritten note and a damaged newspaper clipping. My approach, with answers and clues masked."
summary: "A soaked envelope, a torn newspaper clipping, a personal note: my step-by-step approach to end up at one specific person. Answers and clues masked."
tags: ["CTF", "TryHackMe", "OSINT", "Write-up"]
---

**Letter** is an **OSINT** (open-source intelligence) CTF.

> **Answers and clues masked.** So as not to spoil the room for those still working on it, the clues, the answers and the screenshots that reveal them are masked or blurred. Only the approach is left readable.

## The brief

> It's just another Monday morning on your mail delivery route when an unusual letter catches your eye. The envelope is battered, riddled with holes as if it's been through a storm. The address is barely legible, and your coworkers at the post office wave it off as a lost cause.
>
> But something about it nags at you.
>
> You carefully open the damp envelope. Inside, you find a faded newspaper clipping and a short handwritten note. The clipping is torn and water-damaged, with key sections missing. The note is personal, clearly not meant for your eyes, but the fragments you can read hint at a story buried in time.

**Objective**: use the clues provided in the zip file to uncover the full name and age of the person mentioned in the note.

**Flag format**: `THM{Name_Surname_age}`, only the first letter of the name and surname should be capitalised.
Example: `THM{Pierre-Henry_Lagaffe_23}`

## The letter

I download the file. Inside is a letter (in French, translated here):

> *My dear Édouard,*
>
> *Today, while tidying the attic at my grandparents' house, I came across this old newspaper clipping. **[passage masked: two clues about the person being sought]***
>
> *He would be so proud to see you **[masked]** in your turn.*
>
> *With all my love,*
> *Audette*

**Interesting clues:**

- **[clue masked]**
- **[clue masked]**

## The article

I take a closer look at the clipping.

{{< figure src="01-journal-floute.jpg" alt="Masthead and headlines of the newspaper clipping, blurred" caption="The top of the clipping (blurred: it contains clues)." >}}

It is a **[masked]** newspaper. One of the articles is badly damaged: it must be the one that matters. Some headlines are readable and could help me find the original piece. On the middle article, I can make out **[keywords masked]**.

## The envelope

I have a look at the envelope from the file.

{{< figure src="02-enveloppe.jpg" alt="Soaked, holed envelope with an illegible address" caption="The envelope, badly damaged." >}}

Nothing of interest: it is all damaged.

## The search

I start with a search using the keywords **[masked]**. I land on a site telling the story of this event and reproducing the matching article **[link masked]**.

{{< figure src="03-article-floute.jpg" alt="Original newspaper article, blurred" caption="The original article I found (blurred)." >}}

In the original article I find the place: **[masked]**, postcode **[masked]** (the room's first answer).

## The candidates

The site also has a list of people with their ages. Applying the letter's clues, only one profile fits: **[masked]**, **[masked]** years old.

{{< figure src="04-equipages-floute.jpg" alt="List of people with names and ages, blurred" caption="The list (blurred: it contains the answer)." >}}

**Answer**: `THM{██████_██████_██}`

## What I took from it

- **One clue to search, one to tell candidates apart.** Separating the two keeps you from drowning in results.
- **Start from what is readable.** With a degraded document, you don't guess the missing content: you look for the original.
- **Go from the event to the people.** Once the event is identified, a named list with ages lets you filter.
- **Local sources are valuable, but not enough on their own.** They remain one source among others, to be cross-checked whenever possible.
- **Format matters.** Capitalisation, hyphens, order: a small formatting slip invalidates a correct result.

*TryHackMe room "Letter".*
