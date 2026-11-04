---
title: "TryHackMe — Letter : une enquête OSINT à partir d'une lettre abîmée"
date: 2026-11-04
draft: false
description: "Write-up de la room Letter (TryHackMe) : retrouver une personne à partir d'une note manuscrite et d'une coupure de presse endommagée. La méthode, sans spoiler."
summary: "Une enveloppe trempée, une coupure de journal déchirée, une note personnelle : comment je procède en OSINT pour remonter jusqu'à une personne précise. La méthode, pas la réponse."
tags: ["CTF", "TryHackMe", "OSINT", "Write-up"]
---

## La room en deux mots

**Letter** est un challenge OSINT (renseignement en sources ouvertes) de TryHackMe. Le scénario : vous êtes facteur, un lundi matin, et une enveloppe en piteux état attire votre attention. Elle est trouée, détrempée, l'adresse est presque illisible, et vos collègues la classent comme courrier perdu. Quelque chose vous intrigue quand même. À l'intérieur : une coupure de journal abîmée, dont des passages entiers manquent, et une courte note manuscrite, clairement personnelle.

**Objectif** : à partir des éléments du fichier zip, retrouver le **nom complet et l'âge** de la personne dont parle la note. Le flag suit un format imposé : `THM{Prénom_Nom_âge}`, avec une majuscule initiale seulement.

> **Pourquoi pas de flag ici ?** Les règles de TryHackMe interdisent de publier flags, réponses et walkthroughs pas à pas pour les rooms encore actives. Cet article décrit donc ma **démarche** et ce que j'en retiens. Il ne donne ni la réponse, ni les noms, lieux ou dates qui permettraient de la deviner.

## Les pièces du dossier

- **La note** : un message affectueux adressé à un proche. Elle contient surtout deux indices sur la personne recherchée : un indice lié à son âge, un autre à sa place au sein d'un groupe.
- **La coupure de presse** : le titre du journal est lisible, plusieurs titres d'articles le sont partiellement, et l'article central est très endommagé.
- **L'enveloppe** : trop abîmée pour livrer quoi que ce soit d'exploitable de mon côté.

## Ma méthode

1. **Tout inventorier avant de chercher.** Je relis la consigne, la note, la coupure et l'enveloppe, et je note ce qui est certain, ce qui est partiel et ce qui est seulement suggéré.
2. **Transformer la note en filtres.** Les deux indices de la note ne servent pas à chercher : ils servent à **départager** plus tard les candidats. Je les mets de côté, en les formulant comme des critères vérifiables.
3. **Trouver le pivot le plus solide de la coupure.** Un document abîmé ne se reconstitue pas directement. Ce qui est lisible (le nom du journal, un mot-clé thématique, une zone géographique) sert de point d'appui pour retrouver l'article d'origine ailleurs.
4. **Chercher avec peu de mots, mais les bons.** Quelques mots-clés bien choisis, issus de ce qui est lisible, m'ont mené à une page d'histoire locale qui reproduit l'article original.
5. **Passer de l'événement aux personnes.** Une fois l'événement identifié, je cherche une source qui liste les personnes concernées avec leur âge.
6. **Appliquer les filtres de la note.** Parmi ces personnes, un seul profil satisfait les deux critères posés à l'étape 2.
7. **Contrôler le format avant de valider.** Orthographe exacte du nom comme sur la source, tirets, majuscules, ordre des éléments : le format du flag est strict.

## Ce que j'en retiens

- **Un indice sert à chercher, l'autre à départager.** Distinguer les deux évite de se perdre dans les résultats.
- **Partir de ce qui est lisible.** Face à un document dégradé, inutile de deviner le contenu manquant : on cherche l'original.
- **Les sources locales sont précieuses, mais ne se suffisent pas.** Une page d'histoire locale peut contenir exactement le détail recherché ; elle reste une source parmi d'autres, à citer et à recouper dès que c'est possible.
- **Le détail du format compte.** Casse, tirets, ordre : en OSINT comme en administration système, une petite erreur de forme suffit à invalider un résultat correct.
- **L'éthique ne s'arrête pas au CTF.** Ici, l'enquête porte sur des faits historiques. Dans un contexte réel, identifier une personne vivante à partir de sources ouvertes pose de vraies questions de vie privée et de légitimité.

## Compétences mobilisées

Analyse de documents, recherche avancée, corrélation de sources, rigueur dans la vérification, respect des règles de la plateforme.

*Room « Letter », TryHackMe.
