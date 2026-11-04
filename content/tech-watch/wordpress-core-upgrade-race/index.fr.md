---
title: "WordPress : la mise à jour elle-même ouvrait une porte"
description: "WordPress 7.1.4 corrige une faille de condition de concurrence dans le processus de mise à jour du cœur, exploitable sans compte. La CISA l'a ajoutée à son catalogue des failles exploitées le 3 novembre."
date: 2026-11-05
draft: false
summary: "Pendant quelques secondes, à chaque mise à jour, une copie de WordPress restait à une adresse prévisible. Des attaquants guettaient ce moment. La faille est corrigée dans WordPress 7.1.4 et la CISA la classe comme exploitée."
tags: ["Tech Watch", "Développement web", "WordPress", "Mises à jour"]
---

**Pendant quelques secondes, à chaque mise à jour, une copie complète de WordPress restait à une adresse devinable.**

## Ce qui s'est passé

Le 28 octobre 2026, WordPress a publié la version **7.1.4**, une mise à jour de sécurité qui corrige 22 vulnérabilités. La plus grave se trouve dans le **processus de mise à jour du cœur lui-même** : une condition de concurrence (« race condition ») qui peut mener à l'exécution de code à distance pendant la fenêtre de mise à jour. Elle a été signalée par le chercheur Umut Bayram.

Le mécanisme est simple à comprendre. Lors d'une mise à jour complète, WordPress décompresse les nouveaux fichiers dans un dossier temporaire, `wp-content/upgrade/`. Avant la 7.1.4, ce dossier portait un **nom prévisible** et était accessible depuis le web. Il contenait aussi les scripts d'installation de WordPress. Un attaquant sans compte qui « gagne la course » contre la fin de la décompression peut atteindre ces fichiers et exécuter du code sur le serveur.

La fenêtre est très courte : selon Wordfence, en laboratoire, le dossier vulnérable ne restait accessible que quelques secondes. Cela n'a pas empêché les attaques : Wordfence a observé des sondages automatisés dès la publication du correctif, certaines sources interrogeant de petits groupes de sites pendant environ 14 h 30, pour attraper le bon moment.

La faille touche WordPress de la version 4.7 à la 7.1.3. Elle a reçu l'identifiant **CVE-2026-119977** (score CVSS 8,1, complexité d'attaque élevée). Le 3 novembre, la **CISA** l'a ajoutée à son catalogue des vulnérabilités connues comme exploitées (KEV).

## Pourquoi c'est important

- **Aucun compte n'est nécessaire.** L'attaquant n'a pas besoin de se connecter à WordPress.
- **La fenêtre revient à chaque mise à jour.** Y compris pour les mises à jour automatiques, que personne ne regarde.
- **L'exploitation est confirmée.** Le classement dans le catalogue KEV ne repose pas sur une hypothèse.
- **Les anciennes branches sont couvertes, mais pas toutes.** Les correctifs ont été rétroportés jusqu'à la 4.7 ; les versions 4.6 et antérieures ne reçoivent plus de mises à jour de sécurité.

## Ce qu'il faut en retenir

- **Mettre à jour vers WordPress 7.1.4 (ou la version corrigée de sa branche), puis vérifier le numéro de version** : une mise à jour automatique n'est pas toujours passée.
- **Bloquer l'accès web au dossier `wp-content/upgrade/`** dans la configuration du serveur. C'est une protection supplémentaire, utile même quand tout est à jour.
- **Regarder les journaux** : des requêtes vers des fichiers PHP sous `wp-content/upgrade/` ou des fichiers inconnus sont un signal à vérifier.
- **Une mise à jour est une opération sensible, pas seulement un correctif.** Pendant qu'on installe la protection, le système est temporairement plus exposé.

## Sources

- [WordPress 7.1.4 — annonce officielle (28/10/2026)](https://wordpress.org/news/2026/10/wordpress-7-1-4/)
- [Version 7.1.4 — documentation WordPress.org](https://wordpress.org/support/wordpress-version/version-7-1-4/)
- [CISA — ajout d'une vulnérabilité au catalogue KEV (03/11/2026)](https://www.cisa.gov/news-events/alerts/2026/11/03/cisa-adds-one-known-exploited-vulnerability-catalog)
- [The Hacker News — faille WordPress exploitée après le correctif](https://thehackernews.com/2026/10/wordpress-rce-flaw-draws-nearly-63000.html)
- [SecurityWeek — nouvelle faille WordPress dans le viseur des attaquants](https://securityweek.com/fresh-wordpress-vulnerability-in-attackers-crosshairs)
- [WebHostingToday — WordPress 7.1.4 (analyse de Patchstack)](https://webhosting.today/2026/10/29/wordpress-7-1-4-fixes-22-flaws-one-in-the-core-update-process/)
