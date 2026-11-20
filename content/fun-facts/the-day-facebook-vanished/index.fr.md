---
title: "Le jour où Facebook a disparu d'Internet"
description: "Le 4 octobre 2021, une commande de maintenance a coupé Facebook, Instagram et WhatsApp pendant environ six heures, et les outils pour réparer sont tombés avec."
date: 2026-11-20
draft: false
summary: "Une commande censée vérifier la capacité du réseau a déconnecté tous les data centers de Meta. Les serveurs DNS ont alors retiré leurs propres routes BGP, et les ingénieurs ont dû se rendre sur place pour réparer."
tags: ["Friday Fun Fact", "Réseau", "DevOps", "Histoire"]
---

**Le 4 octobre 2021, Facebook a disparu d'Internet. Pas à cause d'un pirate : à cause d'une commande de maintenance.**

## Une commande de routine

À 15 h 39 UTC, Facebook, Instagram, WhatsApp, Messenger et Oculus deviennent inaccessibles dans le monde entier. Meta explique ensuite ce qui s'est passé : pendant une maintenance, une commande destinée à vérifier la capacité du réseau fédérateur (le « backbone » qui relie ses data centers) a déconnecté toutes les liaisons de ce réseau.

Un outil d'audit aurait dû bloquer cette commande. Un bug l'en a empêché.

## Quand le DNS retire ses propres routes

Les serveurs DNS de Facebook perdent le contact avec les data centers. Ils demandent alors à BGP, le protocole qui annonce les adresses IP de Facebook au reste d'Internet, de retirer ces annonces.

Résultat : les serveurs DNS fonctionnent toujours, mais personne ne sait plus où les trouver. Sans réponse DNS, plus de facebook.com, plus d'instagram.com, plus de whatsapp.com.

## Enfermés dehors

Le plus difficile reste à venir. Les outils internes sont inaccessibles et, selon Meta, l'accès de secours est tombé avec le reste. Les ingénieurs doivent aller dans les data centers pour intervenir sur les machines, ce qui prend du temps à cause des protections physiques en place.

Selon le New York Times, des badges d'accès ne fonctionnaient plus, et des employés se sont parlé via LinkedIn et Discord. Les services reviennent en soirée, après environ six heures.

## Ce qu'on peut en retenir

- **L'accès de secours doit être indépendant.** Un accès « out-of-band » qui dépend du réseau principal ne sert à rien le jour où ce réseau tombe.
- **Un garde-fou peut avoir ses propres bugs.** Aucune commande ne devrait pouvoir, seule, avoir de telles conséquences.
- **Une panne n'est pas toujours une attaque.** Ici, il s'agissait d'une erreur interne.

## Sources

- Meta Engineering, [« More details about the October 4 outage »](https://engineering.fb.com/2021/10/05/networking-traffic/outage-details/) (05/10/2021)
- CACM, [« What Caused the Facebook Outage »](https://cacm.acm.org/news/what-caused-the-facebook-outage)
- The Register, [« Facebook back online »](https://www.theregister.com/2021/10/04/facebook_back_online/) (04/10/2021)
- Silicon Republic, [« What brought down Facebook, WhatsApp and Instagram for six hours? »](https://siliconrepublic.com/?p=947340) (05/10/2021)
- AppleInsider, [« Facebook shows signs of life after hours-long outage »](https://appleinsider.com/articles/21/10/04/facebook-shows-signs-of-life-after-hours-long-outage) (04/10/2021)
