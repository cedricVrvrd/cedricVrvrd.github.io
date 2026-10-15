---
title: "Kasa — une application React"
description: "Application de location de logements entre particuliers développée avec React et React Router."
date: 2022-11-26
draft: false
weight: 20
summary: "Le dernier projet de ma formation de développeur : une application React de location de logements, construite à partir de composants réutilisables."
categories: ["Développement web"]
tags: ["OpenClassrooms", "React"]
showTaxonomies: true
---

*Projet de la formation Développeur Web d'OpenClassrooms, 2022.*

**Une application de location de logements, découpée en composants réutilisables.**

## Le projet

Kasa est une plateforme de location de logements entre particuliers. C'est le dernier projet de la formation : développer le front-end en **React** à partir d'une maquette, avec une page par logement générée à partir des données.

## Ce que j'ai réalisé

- une page d'accueil qui affiche les logements à partir d'un fichier de données JSON ;
- une **fiche par logement**, construite à partir de son identifiant dans l'adresse, avec redirection vers la page 404 si le logement n'existe pas ;
- des composants réutilisables : **carrousel** de photos, **accordéons** pour la description et les équipements, **note en étoiles**, étiquettes ;
- une page « À propos » et une page d'erreur 404 ;
- la navigation entre les pages avec **React Router**.

## Technologies

React 18 · React Router 6 · JSX · CSS · Create React App

<div style="display:flex;flex-wrap:wrap;gap:0.75rem;margin-top:1.5rem">
{{< button href="https://cedricvrvrd.github.io/kasa/" target="_blank" rel="noopener" >}}
Voir le site
{{< /button >}}
{{< button href="https://github.com/cedricVrvrd/kasa" target="_blank" rel="noopener" >}}
Code sur GitHub
{{< /button >}}
</div>
