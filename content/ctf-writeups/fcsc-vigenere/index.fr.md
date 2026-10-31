---
title: "FCSC : Vigenère, à la main"
date: 2026-10-31
draft: false
tags: ["CTF", "FCSC", "Cryptographie", "Write-up"]
summary: "Déchiffrer un message Vigenère à la main, lettre par lettre."
---

## L'épreuve

Une épreuve d'introduction du FCSC (France Cybersecurity Challenge) : déchiffrer un message chiffré avec la méthode de Vigenère. La clé est fournie : `FCSC`. Le flag est le nom de la ville mentionnée dans le message.

```
Gqfltwj emgj clgfv ! Aqltj rjqhjsksg ekxuaqs, ua xtwk
n'feuguvwb gkwp xwj, ujts f'npxkqvjgw nw tjuwcz
ugwygjtfkf qz uw efezg sqk gspwonu. Jgsfwb-aqmu f
Pspygk nj 29 cntnn hqzt dg igtwy fw xtvjg rkkunqf.
```

## Le principe de Vigenère

Vigenère, c'est un chiffre de César dont le décalage change à chaque lettre. Chaque lettre de la clé donne un décalage (A=0, B=1… Z=25), et la clé se répète tout au long du message.

Avec `FCSC`, on obtient quatre décalages qui tournent en boucle :

| Lettre de la clé | F | C | S | C |
|---|---|---|---|---|
| Décalage | 5 | 2 | 18 | 2 |

Pour déchiffrer, on **soustrait** le décalage à chaque lettre (en repartant de Z quand on passe sous A).

## Le déchiffrement à la main

J'ai tout fait lettre par lettre, pour bien comprendre la mécanique.

Premier mot :

| Chiffré | G | q | f | l | t | w | j |
|---|---|---|---|---|---|---|---|
| Clé | F | C | S | C | F | C | S |
| Décalage | −5 | −2 | −18 | −2 | −5 | −2 | −18 |
| Clair | B | o | n | j | o | u | r |

« Bonjour » dès le premier mot : la clé est bonne, je peux continuer.

**Le piège :** la clé n'avance que sur les lettres. Les espaces, la ponctuation, les apostrophes et les chiffres (le « 29 ») sont recopiés tels quels et ne consomment pas de lettre de clé. Si on fait avancer la clé sur un espace, tout le reste devient illisible.

## Résultat

```
Bonjour cher agent ! Votre prochaine mission, si vous
l'acceptez bien sur, sera d'infiltrer le reseau
souterrain ou se cache nos ennemis. Rendez-vous a
Nantes le 29 avril pour le debut de votre mission.
```

**Flag :** `FCSC{Nantes}`

## Ce que j'en retiens

- C'est en le faisant à la main que la logique s'ancre : le décalage, le retour à Z, la clé qui n'avance que sur les lettres.
- Repérer tôt un mot connu (« Bonjour ») permet de vérifier vite qu'on est sur la bonne piste.
- Vigenère a résisté trois siècles, mais une fois la clé connue, ce n'est plus que de l'arithmétique.
