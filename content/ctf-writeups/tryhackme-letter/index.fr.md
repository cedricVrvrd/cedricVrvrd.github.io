---
title: "TryHackMe — Letter : une enquête OSINT à partir d'une lettre abîmée"
date: 2026-11-04
draft: false
description: "Write-up de la room Letter (TryHackMe) : retrouver une personne à partir d'une note manuscrite et d'une coupure de presse endommagée. Ma démarche, réponses et indices masqués."
summary: "Une enveloppe trempée, une coupure de journal déchirée, une note personnelle : ma démarche pas à pas pour remonter jusqu'à une personne précise. Réponses et indices masqués."
tags: ["CTF", "TryHackMe", "OSINT", "Write-up"]
---

**Letter** est un CTF basé sur l'**OSINT** (renseignement en sources ouvertes).

> **Réponses et indices masqués.** Pour ne pas gâcher la room à ceux qui la font encore, les indices, les réponses et les captures qui les révèlent sont masqués ou floutés. Seule la démarche reste lisible.

## L'énoncé

> C'est un lundi matin comme un autre sur ta tournée de facteur quand une lettre inhabituelle attire ton regard. L'enveloppe est cabossée, criblée de trous, comme si elle avait traversé une tempête. L'adresse est à peine lisible, et tes collègues du bureau de poste la considèrent comme perdue d'avance.
>
> Mais quelque chose te chiffonne. Tu ouvres avec précaution l'enveloppe humide. À l'intérieur : une coupure de journal fanée et une courte note manuscrite. La coupure est déchirée et abîmée par l'eau, des passages clés manquent. La note est personnelle, clairement pas destinée à tes yeux, mais les fragments lisibles évoquent une histoire enfouie dans le temps.

**Objectif** : utiliser les indices du fichier zip pour retrouver le **nom complet et l'âge** de la personne mentionnée dans la note.

**Format du flag** : `THM{Prénom_Nom_âge}`, seules les premières lettres du prénom et du nom en majuscule.
Exemple : `THM{Pierre-Henry_Lagaffe_23}`

## La lettre

Je télécharge le fichier. Dedans, on trouve une lettre :

> *Mon cher Édouard,*
>
> *Aujourd'hui, en rangeant le grenier chez mes grands-parents, je suis tombée sur cette vieille coupure de journal. **[passage masqué : deux indices sur la personne recherchée]***
>
> *Il serait si fier de te voir **[masqué]** à ton tour.*
>
> *Avec toute mon affection,*
> *Audette*

**Indices intéressants :**

- **[indice masqué]**
- **[indice masqué]**

## L'article

Je regarde de plus près la coupure de presse.

{{< figure src="01-journal-floute.jpg" alt="Bandeau et titres de la coupure de presse, floutés" caption="Le haut de la coupure (flouté : il contient des indices)." >}}

Il s'agit d'un journal **[masqué]**. Un des articles est très abîmé : ce doit être celui qui nous concerne. On y lit des titres qui pourraient aider à retrouver l'œuvre originale. Sur l'article du milieu, on distingue **[mots-clés masqués]**.

## L'enveloppe

Je jette un œil à l'enveloppe du fichier.

{{< figure src="02-enveloppe.jpg" alt="Enveloppe trempée et trouée, adresse illisible" caption="L'enveloppe, très abîmée." >}}

Rien d'intéressant dessus : tout est abîmé.

## La recherche

Je commence par une recherche avec les mots-clés **[masqués]**. Je tombe sur un site qui raconte l'histoire de cet événement et reproduit l'article correspondant **[lien masqué]**.

{{< figure src="03-article-floute.jpg" alt="Article de presse original, flouté" caption="L'article original retrouvé (flouté)." >}}

Dans l'article original, je trouve le lieu : **[masqué]**, code postal **[masqué]** (première réponse de la room).

## Les candidats

Le site contient aussi une liste de personnes avec leur âge. En appliquant les indices de la lettre, un seul profil correspond : **[masqué]**, **[masqué]** ans.

{{< figure src="04-equipages-floute.jpg" alt="Liste de personnes avec noms et âges, floutée" caption="La liste (floutée : elle contient la réponse)." >}}

**Réponse** : `THM{██████_██████_██}`

## Ce que j'en retiens

- **Un indice sert à chercher, l'autre à départager.** Les séparer évite de se perdre dans les résultats.
- **Partir de ce qui est lisible.** Face à un document dégradé, on ne devine pas le contenu manquant : on cherche l'original.
- **Passer de l'événement aux personnes.** Une fois l'événement identifié, une liste nominative avec les âges permet de filtrer.
- **Les sources locales sont précieuses, mais ne se suffisent pas.** Elles restent une source parmi d'autres, à recouper dès que c'est possible.
- **Le format compte.** Casse, tirets, ordre : une petite erreur de forme invalide un résultat correct.

*Room [« Letter »](https://tryhackme.com/room/letter), TryHackMe.*
