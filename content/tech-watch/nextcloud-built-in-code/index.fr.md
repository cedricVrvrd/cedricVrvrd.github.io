---
title: "Une application « pour les tests » a ouvert des serveurs Nextcloud"
description: "Une faille dans l'application optionnelle Built-in CODE de Nextcloud permettait d'exécuter des commandes sur le serveur sans compte. Elle a été exploitée dès septembre 2026."
date: 2026-10-20
draft: false
summary: "Une application Nextcloud présentée comme destinée aux tests permettait d'exécuter des commandes sur le serveur sans s'identifier. Des attaquants y ont déposé des web shells, et la désactiver ne suffisait pas."
tags: ["Tech Watch", "DevOps", "Nextcloud", "Mises à jour"]
---

**Une application optionnelle, présentée comme destinée aux tests, a suffi pour prendre la main sur des serveurs Nextcloud.**

## Ce qui s'est passé

Nextcloud propose une application, **« Collabora Online - Built-in CODE Server »** (`richdocumentscode`), qui télécharge et fait tourner une suite bureautique en ligne directement sur le serveur Nextcloud. Sa fiche la présente comme destinée aux tests locaux, à un usage personnel ou aux petites équipes.

Jusqu'à la version 26.4.302, un script de cette application insérait une partie de l'adresse demandée dans une commande système. Résultat : **une simple requête, sans compte, pouvait exécuter des commandes sur le serveur** (CVE-2026-110447). L'attaque ne fonctionnait qu'à un moment précis : quand le serveur de documents intégré était arrêté, par exemple après un redémarrage, une mise à jour ou un plantage.

Les premières attaques apparaissent dans les journaux le **10 septembre 2026**. Les attaquants ont déposé des **web shells** en PHP dans le dossier de l'application. Le correctif, la version 26.4.303, est sorti le 11 septembre.

## Pourquoi c'est important

Deux détails rendent ce cas instructif :

- **Désactiver l'application ne suffisait pas.** Ses fichiers restaient sur le serveur et accessibles. L'éditeur est clair : il faut la mettre à jour ou la supprimer.
- **L'exploitation a commencé la veille du correctif.** Un serveur mis à jour ensuite n'est plus vulnérable, mais un web shell déposé avant reste en place.

## Ce qu'il faut en retenir

- **Chaque extension installée fait partie de la surface d'attaque**, même optionnelle, même rarement utilisée. Ce qui ne sert pas se supprime.
- **Un composant « pour les tests » n'a rien à faire en production.**
- **Désactiver n'est pas supprimer.** Tant que le code est sur le disque, il peut être appelé.
- **Mettre à jour ne nettoie pas.** Après une faille exploitée, il faut aussi chercher les traces : ici, des fichiers `shx*.php` dans le dossier de l'application et des requêtes suspectes dans les journaux depuis le 10 septembre.

## Sources

- [Hackers Backdoor Nextcloud Servers Through Critical Flaw in Collabora's Built-in CODE App — The Hacker News (14/10/2026)](https://thehackernews.com/2026/10/hackers-backdoor-nextcloud-servers.html)
- [Avis de sécurité GHSA-g3vx-3m76-fghh — Collabora Online (GitHub)](https://github.com/CollaboraOnline/online/security/advisories/GHSA-g3vx-3m76-fghh)
- [Vulnerability in Nextcloud app allowed attackers to plant web shells — SC Media](https://www.scworld.com/brief/vulnerability-in-nextcloud-app-allowed-attackers-to-plant-web-shells)
