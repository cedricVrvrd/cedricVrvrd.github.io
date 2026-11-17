---
title: "Le ver qui voulait compter"
description: "1988 : un étudiant voulait mesurer la taille d'Internet. Son programme a paralysé une partie du réseau."
date: 2026-11-06
draft: false
summary: "Le 2 novembre 1988, un étudiant de Cornell lâche un programme censé mesurer Internet. Une erreur le rend incontrôlable. Premier ver à grande échelle, première condamnation du genre aux États-Unis."
tags: ["Friday Fun Fact", "Cybersécurité", "Histoire", "Malware"]
---

**Le 2 novembre 1988, un étudiant lance un programme pour compter les machines d'Internet. Quelques heures plus tard, une partie du réseau ne répond plus.**

## Une expérience, pas une attaque

Robert Tappan Morris est étudiant en informatique à Cornell. Il lance son programme depuis un ordinateur du MIT, auquel il accède à distance depuis Cornell. Selon le FBI, l'objectif était de mesurer la taille d'Internet, qui compte alors environ 60 000 machines. Le programme se copie de machine en machine en exploitant des failles connues des systèmes Unix, dont `sendmail` et `fingerd`, ainsi que des mots de passe faibles.

## L'erreur qui change tout

Le ver devait ne s'installer qu'une fois par machine. Morris a pourtant craint qu'un administrateur ne le trompe en lui répondant « déjà infecté ». Il a donc fait en sorte que le ver se recopie de temps en temps malgré tout. Résultat : les machines se retrouvent à faire tourner de nombreuses copies, ralentissent, et refusent de nouvelles connexions. Les administrateurs ne peuvent parfois même plus ouvrir une session pour intervenir.

Le ver ne détruit ni ne vole aucune donnée. Les dégâts viennent de la surcharge. On cite souvent environ 6 000 machines touchées, soit à peu près 10 % du réseau, mais ce chiffre reste une estimation contestée.

## Les suites

Morris est le premier condamné aux États-Unis au titre du Computer Fraud and Abuse Act de 1986. Il est devenu depuis professeur au MIT. L'incident a aussi poussé à créer une équipe de réponse aux incidents, le futur CERT.

## Ce qu'on en retient

Une protection ajoutée par prudence peut devenir la cause du problème. Et une faille connue mais non corrigée reste une faille : les mots de passe faibles et les services mal à jour ont fait le travail il y a plus de trente ans, comme aujourd'hui.

## Sources

- [Morris worm — Wikipedia](https://en.wikipedia.org/wiki/Morris_worm)
- [Morris worm — Tom's Hardware, reprenant la rétrospective du FBI](https://www.tomshardware.com/tech-industry/cyber-security/on-this-day-in-1988-the-morris-worm-slithered-out-and-sparked-a-new-era-in-cybersecurity-10-percent-of-the-internet-was-infected-within-24-hours)
- Eugene Spafford, « The Internet Worm Program: An Analysis » (Purdue, 1988)
