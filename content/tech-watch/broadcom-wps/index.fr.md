---
title: "Box et routeurs : une faille Wi-Fi que certains modèles ne corrigeront jamais"
description: "Le vieux module WPS de Broadcom, présent dans des box et routeurs de nombreuses marques, peut être exploité à portée radio sans le mot de passe Wi-Fi. Broadcom n'a pas attribué de CVE."
date: 2026-10-22
draft: true
summary: "Une faille dans le vieux module WPS de Broadcom touche des box et routeurs de nombreuses marques. Elle s'exploite à portée radio, sans le mot de passe Wi-Fi. Pas de CVE, et pas de correctif pour certains modèles anciens."
tags: ["Tech Watch", "Réseau", "Wi-Fi", "Fin de support"]
---

**Pas besoin du mot de passe Wi-Fi. Il suffit d'être à portée radio.**

## Ce qui s'est passé

Le 16 octobre 2026, à la conférence Hexacon, le chercheur Quentin Kaiser a présenté une faille dans **WPS Monitor**, l'ancien composant de Broadcom qui gère le WPS, ce bouton qui permet de connecter un appareil au Wi-Fi sans taper le mot de passe.

Ce composant ne vérifie pas correctement la taille des messages WPS qu'il reçoit et réassemble. Un attaquant **à portée du Wi-Fi**, **sans connaître le mot de passe** et sans passer par l'appairage WPS, peut provoquer une corruption de mémoire. Le chercheur a démontré une fuite de mémoire contrôlée et l'**exécution de code** sur l'appareil. Les conséquences exactes dépendent du modèle et de son micrologiciel.

La liste des produits concernés, non exhaustive, cite des équipements de nombreuses marques : ARRIS, Arcadyan, Askey, Cisco, Comtrend, Huawei, Netgear, Nokia, TP-Link, ZTE, Zyxel… Pour certains modèles, la vulnérabilité est confirmée ; pour d'autres, elle reste à vérifier selon le micrologiciel.

## Pourquoi c'est important

- **Broadcom n'a pas attribué de CVE.** L'entreprise explique avoir remplacé ce composant en 2018 et considère les produits concernés comme obsolètes ou hors de sa période de support.
- **Désactiver le WPS ne suffit pas toujours.** Selon le chercheur, l'option des réglages peut laisser le composant vulnérable actif.
- **Certains appareils n'auront jamais de correctif.** Les produits les plus anciens, basés sur le système eCos, n'ont parfois aucune voie de mise à jour.

## Ce qu'il faut en retenir

- **Un réglage n'est pas un correctif.** Décocher une option ne garantit pas que le code vulnérable a disparu.
- **Le matériel réseau a une date de péremption.** Un équipement qui ne reçoit plus de mises à jour reste vulnérable à vie : il se remplace.
- **La box fournie par l'opérateur fait partie du réseau.** C'est à l'opérateur ou au fabricant de fournir la mise à jour, mais c'est à l'utilisateur de la demander.
- **La portée radio est une surface d'attaque.** Le Wi-Fi déborde des murs : une faille exploitable sans mot de passe s'attaque depuis le trottoir.

## Sources

- [Broadcom WPS — Quentin Kaiser, présentation à Hexacon 2026 (16/10/2026)](https://qkaiser.github.io/broadcom-wps)
- [Weekly Security Intelligence Briefing, semaine du 19/10/2026 — Tech Jacks Solutions](https://techjacksolutions.com/security/briefing/weekly-security-intelligence-briefing-week-of-2026-10-19/)
