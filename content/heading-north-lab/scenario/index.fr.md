---
title: "Le scénario : Norrøn Voyages"
description: "L'entreprise fictive derrière Heading North Lab : son activité, son incident, et pourquoi elle doit tout reconstruire."
date: 2026-10-11
draft: false
weight: 10
summary: "Une agence de voyages piratée en pleine saison, un partenaire soumis à NIS2, un seul admin pour tout reconstruire. Voici l'entreprise fictive derrière le lab."
tags: ["Heading North Lab", "Scénario"]
---

**Une agence de voyages piratée en pleine saison. Un partenaire qui menace de partir. Un seul admin pour tout reconstruire.**

> Norrøn Voyages est une entreprise fictive, créée pour servir de scénario au lab.

## L'entreprise

**Norrøn Voyages** est une agence de voyages française créée en 2012. Ses 15 salariés organisent des voyages d'aventure en petits groupes vers l'Islande, les îles Féroé et la Norvège : randonnée, trek, aurores boréales.

- **Hélène Marchand**, la fondatrice, est une ancienne guide de randonnée. Pragmatique et pas technicienne, elle veut des résultats concrets et comprendre les enjeux.
- **Bjarni**, le guide-coordinateur, travaille depuis Reykjavik et doit accéder aux outils internes à distance.
- **Les commerciaux** se déplacent beaucoup et utilisent le site et les outils de réservation en mobilité.

L'agence manipule des données sensibles : identités des voyageurs, copies de passeports, informations médicales pour les treks, paiements. Des données soumises au RGPD.

## Le point de départ

Comme dans beaucoup de petites entreprises, l'informatique de l'agence s'est construite sans plan :

- **un vieux serveur unique** qui fait tout ;
- **un réseau à plat** : tous les postes et serveurs peuvent se joindre ;
- **des mots de passe partagés** entre collègues ;
- **un site WordPress modifié directement en production**, avec des extensions rarement mises à jour.

## L'incident

Au printemps dernier, en pleine saison de réservations, le site WordPress a été **défiguré via une extension non mise à jour**. Il est resté hors ligne plusieurs jours.

Ce n'était pas un coup de malchance : c'était la conséquence logique de l'organisation ci-dessus. Sur un réseau à plat, sans mises à jour et avec des mots de passe partagés, une seule faille suffit.

## Le déclencheur

Le principal partenaire norvégien de l'agence, soumis à la **directive NIS2**, exige désormais des garanties de sécurité de ses fournisseurs. Sans elles, le contrat ne sera pas renouvelé.

## Mon rôle

Hélène recrute un administrateur systèmes DevOps : moi. Seul technicien, rattaché directement à elle. La mission : **reconstruire l'infrastructure proprement, l'automatiser, puis être capable de la défendre**.

Prochain article : le plan.
