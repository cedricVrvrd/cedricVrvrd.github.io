---
title: "Entretien avec 6,3 milliards"
description: "Le plus gros vol de crypto de l'histoire a commencé par un faux entretien d'embauche. Retour sur le rapport publié par Binance le 3 novembre 2026."
date: 2026-11-04
draft: false
summary: "Un faux recruteur, un faux PDG, un « exercice de code » et un jeton trouvé sur un poste de travail : comment 6,3 milliards de dollars ont quitté Binance, d'après son propre rapport."
tags: ["Friday Fun Fact", "Ingénierie sociale", "Chaîne d'approvisionnement", "Actualité"]
---

**Une série qui n'a pas besoin de scénariste. Le 29 octobre 2026, environ 6,3 milliards de dollars quittent les portefeuilles de Binance. Tout a commencé par un entretien d'embauche.**

Le 3 novembre, Binance a publié son rapport d'incident. Le FBI attribue l'attaque à la Corée du Nord, qui dément. Voici la saison, épisode par épisode.

## Les épisodes

- **Juin, *Le Homebrew*.** Un ingénieur installe une fausse version de Homebrew, l'outil d'installation de logiciels sur Mac. Binance la détecte, change son poste et renouvelle ses accès, mais le rapport indique que l'équipe portefeuilles est déjà exposée.
- **Septembre, *L'entretien*.** Un autre ingénieur est contacté pour un poste par un faux « directeur de projet », via une plateforme d'emploi (LinkedIn, d'après Fortune). Premier entretien en visio avec une fausse RH, qui lui montre un compte de réseau social rempli de photos pour inspirer confiance. Second entretien avec un faux PDG, qui lui fait télécharger un « exercice de code ». Il l'ouvre sur son ordinateur de travail : c'est un logiciel malveillant, que les outils de sécurité du poste ne repèrent pas tout de suite.
- **20 octobre, *L'assistant*.** Depuis cet ordinateur et un outil d'IA interne, les attaquants atteignent les postes de deux ingénieurs de l'équipe portefeuilles.
- **29 octobre, *Le jeton*.** Sur l'un de ces postes se trouve un jeton, une sorte de badge numérique, qui permet de déployer des conteneurs (de petits environnements d'exécution) sur l'infrastructure de Binance. Les attaquants s'en servent pour déclencher le vol. Les premiers retraits partent vers 21 h 05, heure de Paris, et l'essentiel des fonds sort en une vingtaine de minutes.

## Ce qu'on ne sait pas encore

Binance parle d'une « méthode d'autorisation de transaction avancée » sans la détailler. Sur Ethereum, les attaquants ont utilisé EIP-7702, une fonction qui permet à un portefeuille de confier ses opérations à un programme. Mais sur d'autres réseaux, les fonds sont partis par des signatures ordinaires : des analystes pensent que le système de signature de Binance a été compromis. L'enquête continue. Binance affirme par ailleurs avoir bloqué 57 tentatives similaires, liées à la Corée du Nord, depuis janvier 2026.

## Ce qu'on en retient

Le point faible n'était pas le coffre, mais un poste de développeur et des accès internes trop larges.

- Le code envoyé par un recruteur se teste dans une machine virtuelle jetable, jamais sur l'ordinateur de travail.
- Un jeton ne doit avoir que les droits dont il a besoin.
- Un outil interne ne devrait pas servir de passerelle vers d'autres postes.

**Sources** : The Register, BleepingComputer, Fortune, Axios, CoinDesk (3 novembre 2026) ; TRM Labs.
