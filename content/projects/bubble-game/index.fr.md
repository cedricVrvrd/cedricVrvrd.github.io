---
title: "Bubble Game — un mini-jeu en JavaScript"
description: "Un petit jeu en JavaScript : des bulles apparaissent, on clique pour les éclater, un compteur suit le score."
date: 2023-01-09
draft: false
weight: 70
summary: "Un exercice court en JavaScript : créer des éléments à la volée, gérer les clics et animer les bulles en CSS."
tags: ["Projets", "Exercice", "JavaScript"]
---

**Un mini-jeu en une trentaine de lignes de JavaScript : éclater des bulles avant qu'elles disparaissent.**

## L'exercice

Des bulles de taille et de trajectoire aléatoires montent à l'écran. Chaque clic sur une bulle l'éclate et augmente le score.

## Ce que j'ai pratiqué

- la **création d'éléments à la volée** dans le DOM, à intervalles réguliers ;
- les **événements** : un clic éclate la bulle et met à jour le compteur ;
- le nettoyage : chaque bulle est retirée de la page au bout de quelques secondes ;
- une **animation CSS** dont la direction est réglée depuis JavaScript par une variable CSS.

## Technologies

JavaScript · DOM · événements · animations CSS · variables CSS

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/bubbleGame/" target="_blank" rel="noopener" >}}
Voir le site
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/bubbleGame" target="_blank" rel="noopener" >}}
Code sur GitHub
{{< /button >}}
</div>
