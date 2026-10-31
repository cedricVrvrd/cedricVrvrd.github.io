---
title: "FCSC: Vigenère, by hand"
date: 2026-10-31
draft: false
tags: ["CTF", "FCSC", "Cryptography", "Write-up"]
summary: "Decrypting a Vigenère cipher by hand, letter by letter."
---

## The challenge

An FCSC (France Cybersecurity Challenge) intro challenge: decrypt a message encrypted with the Vigenère cipher. The key is given: `FCSC`. The flag is the name of the city mentioned in the message.

```
Gqfltwj emgj clgfv ! Aqltj rjqhjsksg ekxuaqs, ua xtwk
n'feuguvwb gkwp xwj, ujts f'npxkqvjgw nw tjuwcz
ugwygjtfkf qz uw efezg sqk gspwonu. Jgsfwb-aqmu f
Pspygk nj 29 cntnn hqzt dg igtwy fw xtvjg rkkunqf.
```

## How Vigenère works

Vigenère is a Caesar cipher whose shift changes on every letter. Each letter of the key gives a shift (A=0, B=1… Z=25), and the key repeats along the message.

With `FCSC`, that gives four shifts that loop:

| Key letter | F | C | S | C |
|---|---|---|---|---|
| Shift | 5 | 2 | 18 | 2 |

To decrypt, you **subtract** the shift from each letter (and wrap around after A).

## Decrypting by hand

I did it letter by letter, to really understand the mechanics.

First word:

| Cipher | G | q | f | l | t | w | j |
|---|---|---|---|---|---|---|---|
| Key | F | C | S | C | F | C | S |
| Shift | −5 | −2 | −18 | −2 | −5 | −2 | −18 |
| Plain | B | o | n | j | o | u | r |

"Bonjour" on the very first word: the key is right, I can carry on.

**The trap:** the key only advances on letters. Spaces, punctuation, apostrophes and digits (the "29") are copied as they are and don't use up a key letter. If you advance the key on a space, everything after it turns to gibberish.

## Result

```
Bonjour cher agent ! Votre prochaine mission, si vous
l'acceptez bien sur, sera d'infiltrer le reseau
souterrain ou se cache nos ennemis. Rendez-vous a
Nantes le 29 avril pour le debut de votre mission.
```

**Flag:** `FCSC{Nantes}`

## What I take away from it

- Doing it by hand is what makes the logic stick: the shift, the wrap-around, the key that only moves on letters.
- Spotting a known word early ("Bonjour") is a quick way to check you're on the right track.
- Vigenère held out for three centuries, but once the key is known, it's just arithmetic.
