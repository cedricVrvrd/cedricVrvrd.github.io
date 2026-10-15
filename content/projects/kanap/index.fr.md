---
title: "Kanap — un site e-commerce en JavaScript"
description: "Partie dynamique d'un site de vente de canapés en JavaScript : catalogue, fiche produit, panier et commande."
date: 2022-09-30
draft: false
weight: 30
summary: "Rendre dynamique un site e-commerce en JavaScript pur : catalogue chargé depuis une API, panier, validation du formulaire et commande."
categories: ["Développement web"]
tags: ["OpenClassrooms", "JavaScript"]
showTaxonomies: true
---

*Projet de la formation Développeur Web d'OpenClassrooms, 2022.*

**Un site de vente de canapés, rendu dynamique en JavaScript sans aucun framework.**

## Le projet

Kanap vend des canapés en ligne. Les pages HTML et CSS étaient fournies, ainsi qu'une API Express. Ma mission : **écrire tout le JavaScript** qui relie les deux.

## Ce que j'ai réalisé

- le catalogue, chargé depuis l'API avec **fetch** et inséré dans la page ;
- une fiche produit générée à partir de l'identifiant passé dans l'adresse, avec le choix de la couleur et de la quantité ;
- un **panier enregistré dans le localStorage** : fusion des articles identiques, modification des quantités, suppression, calcul du total ;
- la **validation du formulaire** de commande avec des expressions régulières ;
- l'envoi de la commande à l'API, puis la page de confirmation avec le numéro de commande.

## La démo en ligne

À l'origine, le site interrogeait l'API Express en local. Pour le publier sur GitHub Pages, qui n'héberge que des fichiers statiques, j'ai adapté une **version de démonstration** : le catalogue est lu dans un fichier JSON, et la commande est simulée (le numéro est généré dans le navigateur, rien n'est envoyé). Le code d'origine, back-end compris, est inchangé dans le dépôt.

## Technologies

JavaScript · DOM · Fetch API · localStorage · expressions régulières · HTML · CSS

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/P5-Dev-Web-Kanap/" target="_blank" rel="noopener" >}}
Voir le site
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/P5-Dev-Web-Kanap" target="_blank" rel="noopener" >}}
Code sur GitHub
{{< /button >}}
</div>
