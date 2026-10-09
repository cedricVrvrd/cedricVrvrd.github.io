---
title: "Le hacker à 75 centimes"
description: "Comment une minuscule erreur comptable a mené un astronome jusqu'à un réseau d'espionnage lié au KGB."
date: 2026-10-09
draft: false
summary: "En 1986, un écart de 75 centimes dans la facturation d'un laboratoire mène un astronome devenu administrateur système jusqu'à un pirate qui vendait des secrets au KGB."
tags: ["Friday Fun Fact", "Blue Team", "Histoire", "Honeypot"]
---

**75 centimes. C'est tout ce qui manquait sur une facture informatique. Et c'est ce qui a fait tomber un réseau d'espionnage.**

## Une erreur d'arrondi qui n'en était pas une

En 1986, Cliff Stoll est un astronome devenu administrateur système au Lawrence Berkeley Laboratory, en Californie. Les chercheurs y paient le temps machine qu'ils utilisent, et son responsable lui demande d'expliquer un écart de 75 centimes dans la comptabilité.

La plupart des gens y auraient vu une erreur d'arrondi. Stoll, lui, creuse. Il remonte jusqu'à un utilisateur inconnu qui a consommé neuf secondes de calcul sans payer. Pire : l'intrus a obtenu les droits root sur le système.

## Dix mois de traque

Plutôt que de simplement bloquer l'intrus, Stoll et ses collègues choisissent de l'observer. Pendant près de dix mois, Stoll suit chacune de ses connexions, consigne tout dans un carnet de bord, et découvre que le laboratoire n'est qu'un point de passage : l'intrus s'en sert pour atteindre des systèmes militaires américains.

## Le piège

Stoll remarque que l'intrus s'intéresse au programme de défense antimissile « Star Wars » (SDI). Il crée donc un faux compte « SDInet », rempli de documents à l'air important mais sans valeur. L'appât fonctionne : l'intrus reste connecté assez longtemps pour que la connexion soit tracée à travers les réseaux internationaux. On le présente souvent comme l'un des premiers usages documentés d'un **honeypot**.

La piste mène en Allemagne de l'Ouest, jusqu'à Markus Hess, qui revendait le fruit de ses intrusions au KGB. Il est reconnu coupable d'espionnage en 1990.

## La leçon pour un Blue Team

Une attaque se cache rarement dans une grosse alerte évidente. Elle se cache dans la petite anomalie que personne ne prend le temps d'expliquer. L'enquête de Stoll montre aussi la valeur de deux réflexes indispensables aujourd'hui :

- **Conserver et lire ses logs.** Sans les relevés de facturation, il n'y aurait eu aucun écart à remarquer.
- **Tout documenter.** Le carnet de Stoll a permis de comprendre les méthodes de l'attaquant, puis de prouver les faits.

## Sources

- Clifford Stoll, *The Cuckoo's Egg* (1989)
- Clifford Stoll, « Stalking the Wily Hacker », *Communications of the ACM* (1988)
- [Markus Hess — Wikipedia](https://en.wikipedia.org/wiki/Markus_Hess)
- [The Cuckoo's Egg — Wikipedia](https://en.wikipedia.org/wiki/The_Cuckoo%27s_Egg_(book))
- [How a Berkeley eccentric beat the Russians — California Magazine](https://alumni.berkeley.edu/california-magazine/spring-2016-war-stories/how-berkeley-eccentric-beat-russians-and-then-made/)

*Illustration : reconstitution fictive d'un relevé comptable, pas un document original de 1986.*
