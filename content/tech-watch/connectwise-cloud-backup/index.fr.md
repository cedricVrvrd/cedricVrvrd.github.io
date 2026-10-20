---
title: "Une application de sauvegarde a ouvert 162 environnements Microsoft 365"
description: "Avec un identifiant volé à ConnectWise, des attaquants se sont connectés à des environnements Microsoft 365 en tant qu'application, sans passer par aucun compte utilisateur."
date: 2026-10-20
draft: false
summary: "Les attaquants n'ont piraté aucun compte : ils se sont connectés en tant que l'application de sauvegarde ConnectWise, déjà autorisée chez ses clients. La double authentification des utilisateurs n'entrait pas en jeu."
tags: ["Tech Watch", "Cloud", "Microsoft 365", "Fournisseurs"]
---

**Les attaquants n'ont pas volé un seul mot de passe utilisateur. Ils se sont connectés en tant qu'application de sauvegarde.**

## Ce qui s'est passé

**ConnectWise Cloud Backup** (anciennement SkyKick) sauvegarde les données Microsoft 365 de ses clients : messagerie, OneDrive, SharePoint, Teams. Pour cela, chaque client a autorisé l'application à accéder à son environnement.

Le **15 octobre 2026**, entre 6 h 13 et 8 h 34 UTC, des attaquants ont utilisé un identifiant de l'application, volé chez l'éditeur, pour se connecter **en tant qu'application** chez ses clients, depuis une seule adresse IP et de façon automatisée. Au 16 octobre, Huntress confirmait des connexions non autorisées dans **162 environnements**. Selon une mise à jour, l'adresse a tenté de se connecter à près de 1 000 environnements, avec succès dans plus de 300.

Dans une cinquantaine d'environnements surveillés par Huntress, des applications ConnectWise se sont attribué des rôles d'administration, surtout Exchange. Dans au moins un cas, l'une d'elles s'est donné le rôle d'**administrateur global**, puis a ajouté de nouveaux secrets à deux autres applications : de quoi revenir plus tard.

ConnectWise a coupé l'accès au service le 17 octobre. L'éditeur dit n'avoir, à ce stade, aucun indice que les données sauvegardées aient été compromises.

## Pourquoi c'est important

Une connexion « en tant qu'application » n'implique **aucun utilisateur**. Il n'y a donc ni mot de passe à saisir ni double authentification à valider. Les protections pensées pour les comptes ne s'appliquent pas.

Or une application de sauvegarde a, par nature, accès à presque tout. Elle concentre les droits de lecture de toute l'organisation. Microsoft parle d'une attaque active de la chaîne d'approvisionnement.

## Ce qu'il faut en retenir

- **Une application tierce est une identité à part entière**, souvent avec plus de droits que n'importe quel salarié. Il faut savoir lesquelles ont accès à quoi, et retirer celles qui ne servent plus.
- **La double authentification protège les comptes, pas les applications.** Les connexions et les changements de rôle des applications doivent être surveillés comme ceux des administrateurs.
- **Désactiver plutôt que supprimer.** Huntress recommande de désactiver l'application concernée sans la supprimer, pour garder l'historique, puis de vérifier tous les secrets ajoutés aux applications depuis le 13 octobre.
- **La sécurité d'un fournisseur fait partie de la sienne.** C'est précisément ce que demandent des réglementations comme NIS2.

## Sources

- [ConnectWise (SkyKick) Vendor Credentials Abused in M365 Attacks — Huntress (16/10/2026)](https://www.huntress.com/blog/vendor-credential-enables-unauthorized-access)
- [Hackers breach Microsoft 365 tenants via ConnectWise supply chain attack — BleepingComputer (17/10/2026)](https://www.bleepingcomputer.com/news/security/hackers-breach-microsoft-365-tenants-via-connectwise-supply-chain-attack/)
- [ConnectWise Cloud Backup Compromise in Microsoft 365: What Happened and What to Do Now — Security Boulevard](https://securityboulevard.com/2026/10/connectwise-cloud-backup-compromise-in-microsoft-365-what-happened-and-what-to-do-now/)
