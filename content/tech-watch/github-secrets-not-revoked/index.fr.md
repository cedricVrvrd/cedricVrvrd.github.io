---
title: "543 699 secrets GitHub fonctionnent encore. Personne ne les a révoqués."
description: "Une étude portant sur 224 millions de dépôts publics montre que les identifiants exposés restent valides pendant des années, faute de révocation."
date: 2026-10-11
draft: false
summary: "Sur 1,1 million d'identifiants exposés dans des dépôts GitHub publics, 543 699 fonctionnaient encore en juillet 2026. Le problème n'est pas la fuite, c'est l'absence de révocation."
tags: ["Tech Watch", "DevSecOps", "Gestion des secrets", "GitHub"]
---

**Supprimer un mot de passe de GitHub ne le désactive pas. 543 699 identifiants le prouvent.**

## Ce qui s'est passé

Le 29 septembre 2026, Truffle Security a publié une étude fondée sur The Stack v3, un jeu de données de code GitHub public collecté pour entraîner des IA : 224 millions de dépôts et 58 milliards de fichiers, récupérés jusqu'en août 2025.

Les chercheurs y ont trouvé **1 103 438 identifiants exposés**. Fin juillet 2026, ils ont testé chacun auprès du service qui l'avait émis : **543 699 fonctionnaient encore**.

Quelques chiffres marquants :

- le plus ancien identifiant encore valide est une **clé AWS publiée en 2009**, active depuis 16 ans ;
- en médiane, un identifiant était public depuis **784 jours** ;
- près de **200 000** identifiants encore valides ont été publiés **après** que GitHub a activé par défaut le blocage des secrets (*push protection*), en février 2024.

## Pourquoi c'est important

Le résultat le plus intéressant n'est pas le volume, c'est la cause. La survie d'un secret dépend de sa **révocation**, pas de sa détection :

- les jetons que leur fournisseur révoque automatiquement (GitHub, npm) sont quasiment tous morts : seuls 260 jetons GitHub et un unique jeton npm fonctionnaient encore ;
- les chaînes de connexion aux bases de données (MongoDB, Postgres, MySQL), que personne ne révoque automatiquement, sont presque toutes encore actives.

Le blocage des secrets a réduit environ de moitié la fréquence à laquelle les secrets concernés arrivent dans du code public. Mais, comme l'écrivent les chercheurs, il « n'a rien changé à ce qui arrive à un identifiant une fois qu'il est publié ». Et environ la moitié des identifiants encore valides sont de types que ce blocage ne couvre pas par défaut.

## Ce qu'il faut en retenir

- **Un secret publié est compromis**, même si le commit est supprimé une minute après. On le change d'abord, on nettoie l'historique ensuite.
- **Bloquer les fuites futures ne règle pas celles du passé.** Il faut scanner tout l'historique de ses dépôts, en particulier ce qui a été publié avant février 2024.
- **Préférer des identifiants à durée de vie courte.** La plupart des secrets exposés auraient expiré sans dommage s'ils avaient eu une date d'expiration.
- **Vérifier ses fournisseurs.** Le service utilisé révoque-t-il automatiquement les clés exposées ? Sinon, la détection seule laisse la clé fonctionner.

Pour Norrøn Voyages, l'entreprise fictive de mon lab, ce sera une règle dès la phase 6 : aucun secret dans Git, et tout secret qui s'y retrouve est changé immédiatement.

## Sources

- [GitHub Repos Exposed 543,699 Credentials. Nobody Revoked Them. — Truffle Security (29/09/2026)](https://trufflesecurity.com/blog/github-repos-exposed-543699-credentials-nobody-revoked-them)
- [500,000 Active Credentials Left Exposed on GitHub — SecurityWeek (01/10/2026)](https://www.securityweek.com/500000-active-credentials-left-exposed-on-github/)
