---
title: "Piquante — une API sécurisée"
description: "API REST Node.js / Express / MongoDB pour une application d'avis sur des sauces piquantes, avec authentification et mesures de sécurité inspirées de l'OWASP."
date: 2022-11-26
draft: false
weight: 10
summary: "Le seul projet back-end de ma formation de développeur, et le plus proche de ce que je fais aujourd'hui : une API Node.js où l'essentiel du travail porte sur la sécurité."
categories: ["Développement web"]
tags: ["OpenClassrooms", "Node.js", "Sécurité"]
showTaxonomies: true
---

*Projet de la formation Développeur Web d'OpenClassrooms, 2022.*

**Une API où l'essentiel du travail ne se voit pas : l'authentification, les contrôles d'accès et la protection des données.**

## Le projet

Piquante est une application où les utilisateurs publient des sauces piquantes et les notent avec des « j'aime » ou « je n'aime pas ». Le front-end Angular était fourni par OpenClassrooms. Ma mission : **construire l'API qui le fait fonctionner**, avec une attention particulière à la sécurité.

## Ce que j'ai réalisé

- une API REST complète : création, lecture, modification et suppression des sauces, gestion des likes et dislikes ;
- l'inscription et la connexion des utilisateurs, avec un **jeton JWT** pour chaque requête authentifiée ;
- un **contrôle de propriété** : seul l'auteur d'une sauce peut la modifier ou la supprimer, et l'identifiant de l'utilisateur est pris dans le jeton, jamais dans la requête du client ;
- l'envoi d'images avec multer.

## La sécurité

- mots de passe **hachés avec bcrypt**, et politique de mot de passe imposée (longueur, majuscules, chiffres, symboles) ;
- adresses e-mail **pseudonymisées avec un HMAC** avant d'être stockées : la base ne contient pas les adresses en clair ;
- en-têtes HTTP durcis avec **helmet**, nettoyage des entrées contre le **XSS**, **limitation du nombre de requêtes** par adresse IP ;
- tous les secrets (base de données, clés de signature) dans des **variables d'environnement**, jamais dans le code.

## Technologies

Node.js · Express · MongoDB · Mongoose · JWT · bcrypt · crypto-js · helmet · express-rate-limit · multer · dotenv

## Pourquoi il compte aujourd'hui

C'est le projet de ma formation développeur le plus proche de mon orientation actuelle vers le DevSecOps : penser d'abord à ce qu'un attaquant pourrait faire, puis le rendre difficile.

Pas de démo en ligne : une API a besoin d'un serveur et d'une base de données, ce que GitHub Pages ne fournit pas.

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://github.com/cedricVrvrd/PIQUANTE" target="_blank" rel="noopener" >}}
Code sur GitHub
{{< /button >}}
</div>
