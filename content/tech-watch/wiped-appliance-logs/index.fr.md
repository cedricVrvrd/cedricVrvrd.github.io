---
title: "Deux attaques, un même réflexe : effacer les journaux"
description: "Dans les attaques contre Ivanti Connect Secure et BeyondTrust Remote Support, révélées en octobre 2026, les attaquants ont effacé ou modifié les journaux des appareils piratés."
date: 2026-10-20
draft: false
summary: "Ivanti Connect Secure et BeyondTrust Remote Support : deux failles, deux attaquants, et dans les deux cas des journaux effacés ou modifiés sur l'appareil piraté. Des journaux qui restent sur l'équipement ne prouvent plus rien."
tags: ["Tech Watch", "Journaux", "Supervision", "VPN"]
---

**Deux failles, deux attaquants différents, un même réflexe : effacer les journaux de l'appareil piraté.**

## Ce qui s'est passé

**Ivanti Connect Secure.** Le 13 octobre 2026, Volexity a révélé une chaîne de trois failles inconnues sur ce boîtier VPN. L'appareil attaqué était à jour au moment des faits. L'attaquant a obtenu les droits les plus élevés (root), récupéré des identifiants et des clés de récupération BitLocker, puis **modifié les journaux** pour effacer les traces de son passage. L'outil de vérification d'intégrité fourni par Ivanti ne détecte pas cette attaque, car le code n'est modifié qu'en mémoire.

**BeyondTrust Remote Support.** Le 15 octobre 2026, Mandiant a décrit l'exploitation d'une faille de cet outil d'assistance à distance depuis fin août. L'attaquant a installé un web shell, récupéré des identifiants stockés, et **supprimé les journaux de l'appareil tout au long de l'intrusion**.

## Pourquoi c'est important

Ces équipements sont exposés à Internet et ont une position privilégiée dans le réseau. Une fois l'attaquant à l'intérieur avec les droits les plus élevés, tout ce qui est stocké sur l'appareil est à sa portée, journaux compris.

Mandiant recommande donc d'envoyer les journaux de l'appareil **en continu vers un système de collecte externe** (SIEM), et de garder aussi ceux des équipements autour : pare-feu, proxy. Et il note qu'**une interruption dans les journaux transmis** est en soi un indice fort de manipulation.

## Ce qu'il faut en retenir

- **Un journal stocké uniquement sur l'appareil compromis ne prouve plus rien.** Il doit partir ailleurs, au fil de l'eau, avant que l'attaquant arrive.
- **Le silence est un signal.** Une source qui cesse soudain d'envoyer ses journaux mérite une alerte, pas un haussement d'épaules.
- **« À jour » ne veut pas dire « sûr ».** Le boîtier Ivanti était à jour : seules des traces conservées ailleurs permettent de reconstituer ce qui s'est passé.
- **Croiser les sources.** Les journaux du pare-feu ou du proxy devant l'appareil gardent une trace que l'attaquant ne peut pas modifier depuis l'appareil.

## Sources

- [Ivanti Connect Secure zero-day actively exploited — CyberScoop (13/10/2026)](https://cyberscoop.com/ivanti-connect-secure-zero-day-actively-exploited/)
- [Attackers chained three Ivanti zero-days to gain root on fully patched VPN appliances — Help Net Security (14/10/2026)](https://www.helpnetsecurity.com/2026/10/14/ivanti-zero-days-gain-root-patched-vpn-appliances/)
- [ARMORY CASTLE exploits BeyondTrust — Mandiant / Google Threat Intelligence (15/10/2026)](https://cloud.google.com/blog/topics/threat-intelligence/armory-castle-exploits-beyondtrust)
