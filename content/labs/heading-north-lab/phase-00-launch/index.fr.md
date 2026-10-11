---
title: "Phase 0 — Pourquoi ce lab"
description: "Le scénario, le point de départ et l'architecture cible de Heading North Lab."
date: 2026-10-13
draft: true
summary: "Une agence de voyages piratée en pleine saison, un partenaire soumis à NIS2, un seul admin pour tout reconstruire. Voici le scénario, le point de départ et le plan."
tags: ["Heading North Lab", "Phase 0", "Architecture"]
---

**Une agence de voyages piratée en pleine saison. Un partenaire qui menace de partir. Un seul admin pour tout reconstruire.**

## Pourquoi un seul projet au long cours

Je termine un Bachelor Administrateur Système DevOps. Plutôt que d'empiler des exercices isolés, j'applique tout ce que j'apprends à **une seule infrastructure**, sur mon propre serveur Proxmox, phase après phase. Chaque nouvelle compétence doit répondre à un vrai besoin de la même entreprise, et chaque phase s'appuie sur les précédentes.

## Le scénario : Norrøn Voyages

**Norrøn Voyages** est une agence de voyages française créée en 2012. Ses 15 salariés organisent des voyages d'aventure en petits groupes vers l'Islande, les îles Féroé et la Norvège : randonnée, trek, aurores boréales. L'essentiel de l'équipe travaille au siège ; les commerciaux se déplacent beaucoup, et Bjarni, le guide-coordinateur, travaille depuis Reykjavik.

L'agence manipule des données sensibles : identités des voyageurs, copies de passeports, informations médicales pour les treks, paiements. Des données soumises au RGPD.

**L'incident.** Au printemps dernier, en pleine saison de réservations, le site WordPress a été défiguré via une extension non mise à jour. Il est resté hors ligne plusieurs jours.

**Le déclencheur.** Le principal partenaire norvégien de l'agence, soumis à la directive NIS2, exige désormais des garanties de sécurité de ses fournisseurs. Sans elles, le contrat ne sera pas renouvelé.

**Mon rôle.** Hélène Marchand, la fondatrice, recrute un administrateur systèmes DevOps : moi. La mission : reconstruire l'infrastructure proprement, l'automatiser, puis être capable de la défendre.

> Norrøn Voyages est une entreprise fictive, créée pour servir de scénario au lab.

## Le point de départ

Comme dans beaucoup de petites entreprises, l'informatique de l'agence s'est construite sans plan :

- **un vieux serveur unique** qui fait tout ;
- **un réseau à plat** : tous les postes et serveurs peuvent se joindre ;
- **des mots de passe partagés** entre collègues ;
- **un site WordPress modifié directement en production**, avec des extensions rarement mises à jour.

Le site défiguré n'est pas un coup de malchance : c'est la conséquence logique de cette organisation. Sur un réseau à plat, une machine compromise n'est qu'à un pas de toutes les autres.

## La cible

![Le réseau à plat d'aujourd'hui à côté de l'architecture cible, segmentée en VLAN derrière pfSense](architecture-fr.png)

La cible est un réseau segmenté : chaque zone est un VLAN distinct, et **tout flux entre deux zones passe par le pare-feu pfSense**. Tout est bloqué par défaut ; chaque flux est ouvert explicitement, pour une raison précise.

- **Administration** : les interfaces d'administration de Proxmox et de pfSense ne sont accessibles que depuis cette zone ;
- **Serveurs / DMZ** : le site WordPress et sa base de données, seule partie exposée à Internet ;
- **Utilisateurs** : les postes des salariés, qui accèdent au site comme n'importe quel visiteur ;
- **VPN** : Bjarni et les commerciaux passent par Internet ; leur tunnel chiffré aboutit sur pfSense, qui ne les laisse atteindre que les services dont ils ont réellement besoin ;
- **Supervision / SIEM** : dans son propre VLAN. Les logs de toutes les zones y arrivent en sens unique, pour qu'un attaquant qui compromet un serveur ne puisse pas atteindre le SIEM pour effacer ses traces ;
- **Lab offensif** : une machine d'attaque isolée pour la dernière phase. Elle pourra atteindre la DMZ pendant les tests de la phase 12, jamais les zones Administration ou Utilisateurs.

C'est **un plan, pas quelque chose de déjà construit**. Il évoluera au fil de la construction, et chaque changement sera expliqué.

## Les 13 phases

| # | Phase | Le besoin de Norrøn Voyages |
|---|---|---|
| 0 | Lancement | Présenter le projet et le scénario |
| 1 | Architecture | Auditer l'existant : le réseau à plat |
| 2 | Proxmox, VM, réseau | Reconstruire sur des bases saines |
| 3 | Sécurisation | Plus jamais l'incident du printemps |
| 4 | Accès distant | Bjarni doit travailler depuis Reykjavik en sécurité |
| 5 | WordPress | Réinstaller le site proprement |
| 6 | Git / GitHub | Fini les modifications en direct sur la production |
| 7 | Jenkins | Mettre à jour le site sans coupure |
| 8 | Docker | Un environnement identique du test à la production |
| 9 | Kubernetes | Tenir le pic de réservations de janvier |
| 10 | Terraform / Ansible | Plan de reprise : tout reconstruire vite |
| 11 | Supervision | Savoir qu'il y a un problème avant les clients |
| 12 | Blue Team | Prouver au partenaire NIS2 qu'on détecte les attaques |

La dernière phase boucle la boucle : j'attaquerai l'infrastructure que j'ai moi-même construite et sécurisée, et je montrerai ce que ma détection repère.

## Comment je vais le documenter

Chaque phase suit la même structure : **le besoin de l'entreprise → ce que j'ai mis en place → ce qui a coincé ou ce que j'ai appris → la prochaine étape**. Erreurs comprises : elles font partie de l'apprentissage, et ce sont souvent les plus utiles.

Je partage chaque étape sur [LinkedIn](https://www.linkedin.com/in/c%C3%A9dric-vervoord-07940915b/) chaque semaine, avec la version détaillée ici.
