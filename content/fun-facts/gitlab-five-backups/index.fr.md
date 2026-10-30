---
title: "GitLab, 2017 : cinq sauvegardes, aucune ne fonctionnait"
description: "Le soir où un administrateur de GitLab.com a effacé la mauvaise base de données, et où l'équipe a découvert que ses sauvegardes ne marchaient pas."
date: 2026-10-30
draft: false
summary: "Une commande lancée sur le mauvais serveur, 300 Go effacés, et cinq méthodes de sauvegarde dont aucune ne fonctionnait. GitLab a été sauvé par une copie faite à la main, six heures plus tôt, pour tout autre chose."
tags: ["Friday Fun Fact", "DevOps", "Sauvegardes", "Histoire"]
---

**Le 31 janvier 2017, GitLab.com a perdu six heures de données. Pas à cause d'un pirate : à cause d'une commande lancée sur le mauvais serveur.**

## Une longue soirée

Ce soir-là, l'équipe de GitLab.com lutte déjà contre une base de données surchargée, probablement à cause de spams. La réplication entre le serveur principal, `db1`, et son serveur de secours, `db2`, ne suit plus. Pour la relancer, un ingénieur décide de vider le dossier de données de `db2`.

Vers 23 h 30 UTC, la commande est lancée. Mais la session est ouverte sur `db1`, le serveur de production.

L'ingénieur s'en rend compte une seconde ou deux plus tard et interrompt la commande. Trop tard : environ **300 Go de données** ont déjà disparu.

## Cinq filets de sécurité, tous troués

L'équipe se tourne vers les sauvegardes. C'est là que la soirée bascule. GitLab le résumera dans un message public : *« sur les 5 techniques de sauvegarde et de réplication déployées, aucune ne fonctionne de manière fiable ou n'a même été mise en place »*.

- **Les sauvegardes quotidiennes** vers le stockage S3 utilisaient une version de l'outil `pg_dump` (9.2) incompatible avec la base (PostgreSQL 9.6). Elles échouaient depuis un moment, et le dossier S3 était vide.
- **Les e-mails d'alerte** qui signalaient ces échecs étaient rejetés par le serveur de messagerie, faute de configuration DMARC. Personne ne les a jamais reçus.
- **Les instantanés de disque** chez Azure étaient activés pour d'autres serveurs, mais pas pour les bases de données.
- **La réplication** était justement en panne, et le serveur de secours venait d'être vidé lui aussi.

## Sauvés par une copie faite pour autre chose

Il restait une chance : un instantané du disque, fait **à la main six heures plus tôt** par un ingénieur, pour alimenter l'environnement de test. Il n'avait rien d'une sauvegarde : c'est pourtant lui qui a permis de tout restaurer.

La copie vers la production a pris environ 18 heures, sur des disques lents. Bilan : six heures de données perdues, soit au moins 5 000 projets, 5 000 commentaires et 700 comptes utilisateurs créés entre-temps. Les dépôts Git eux-mêmes, stockés ailleurs, n'ont pas été touchés.

Détail rare : GitLab a tout fait en public. Un document partagé décrivait l'avancement minute par minute, et la restauration a été **diffusée en direct sur YouTube**, avec jusqu'à 5 000 spectateurs.

## Ce que tout admin reconnaîtra

Une sauvegarde qu'on n'a jamais restaurée n'est qu'une hypothèse. Et une alerte que personne ne reçoit n'existe pas. Dans la liste des corrections publiée ensuite par GitLab, une ligne résume tout : **tester automatiquement la restauration des sauvegardes**.

## Sources

- [Postmortem of database outage of January 31 — GitLab (10/02/2017)](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/)
- [GitLab.com melts down after wrong directory deleted, backups fail — The Register (01/02/2017)](https://www.theregister.com/2017/02/01/gitlab_data_loss/)
