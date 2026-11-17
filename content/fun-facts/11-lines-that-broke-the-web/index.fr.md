---
title: "11 lignes de code qui ont cassé le web"
description: "Mars 2016 : un développeur retire ses paquets de npm, et des milliers de projets ne se construisent plus."
date: 2026-11-13
draft: false
summary: "En 2016, le retrait de plus de 250 modules npm, dont left-pad, une fonction de 11 lignes qui ajoute des espaces devant un texte, fait échouer les installations de milliers de projets."
tags: ["Friday Fun Fact", "DevOps", "Chaîne d'approvisionnement", "Développement"]
---

**Le 22 mars 2016, une fonction de 11 lignes disparaît d'Internet. Quelques heures plus tard, des milliers de projets ne s'installent plus.**

## Un module minuscule

`left-pad` fait une seule chose : ajouter des caractères, souvent des espaces ou des zéros, à gauche d'un texte pour atteindre une longueur donnée. Onze lignes de JavaScript, publiées sur npm, le dépôt public de paquets JavaScript. Trop simple pour qu'on se pose des questions : des milliers de projets l'utilisent, directement ou, le plus souvent, via d'autres paquets. Parmi eux, Node et Babel.

## Le retrait

À la suite d'un litige, son auteur, Azer Koçulu, retire plus de 250 de ses modules de npm, `left-pad` compris. Dès l'instant où le paquet disparaît, les installations qui en dépendent échouent : un paquet manquant dans la chaîne suffit à bloquer toute la construction.

## Le retour

Laurie Voss, directrice technique de npm, restaure alors une version de `left-pad`, après qu'un nouveau mainteneur en a fait la demande. En quelques heures, des milliers de projets sont réparés. L'incident a surtout rendu visible quelque chose que peu de gens voyaient : un projet moderne dépend de centaines de petits paquets, écrits par des inconnus.

## Ce qu'on en retient

Ce qu'on installe, on en dépend. Un fichier de verrouillage (`package-lock.json`) fige les versions. Un miroir interne ou un cache des dépendances critiques garde une copie si le fournisseur retire un paquet. Dans un pipeline CI/CD, c'est une vraie question de fiabilité, pas seulement de sécurité.

## Sources

- [How one developer just broke Node, Babel and thousands of projects in 11 lines of JavaScript — The Register (23/03/2016)](https://www.theregister.com/2016/03/23/npm_left_pad_chaos/)
