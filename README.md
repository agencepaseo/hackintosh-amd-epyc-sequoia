# Hackintosh AMD EPYC — macOS Sequoia 15.7 en bare metal avec SMT 32 threads

> **Première mondiale documentée** : macOS Sequoia 15.7.7 bootant nativement sur un serveur AMD EPYC, sans VM, sans passthrough, avec le SMT pleinement actif (32 threads reconnus par le kernel).

[![Geekbench 6 Multi-Core](https://img.shields.io/badge/Geekbench%206%20Multi-8207-brightgreen)](https://browser.geekbench.com/v6/cpu/18196255)
[![Geekbench 6 Single-Core](https://img.shields.io/badge/Geekbench%206%20Single-1217-brightgreen)](https://browser.geekbench.com/v6/cpu/18196255)
[![SMT Threads](https://img.shields.io/badge/SMT-32%20threads-blue)]()
[![macOS](https://img.shields.io/badge/macOS-Sequoia%2015.7.7-lightgrey)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📖 Article complet

L'histoire technique complète — les 40+ échecs de boot, les impasses, la recherche multilingue (EN/FR/DE/CN/RU/VN/KR/JP), les 4 blocages conceptuels résolus, les réglages BIOS Supermicro, les remerciements — est sur mon blog :

### 👉 [Lire l'article complet sur paseo.cloud](https://paseo.cloud/macos-sequoia-15-7-sur-amd-epyc-en-bare-metal/)

---

## En résumé

Après plus de 40 tentatives de boot et des semaines de travail, j'ai réussi à faire booter macOS Sequoia 15.7.7 nativement sur un AMD EPYC 7302P (Zen 2 Rome, 16C/32T) sur une carte serveur Supermicro H11SSL-i v2.0, avec les 32 threads SMT pleinement reconnus par le kernel.

À ma connaissance, **aucun cas de boot bare-metal Sequoia sur EPYC n'avait été documenté auparavant dans le monde**. Le seul cas EPYC + macOS référencé est une VM Proxmox avec passthrough PCIe, ce qui n'est pas la même catégorie de problème technique.

## Hardware

| Composant | Détail |
|---|---|
| Carte mère | Supermicro H11SSL-i v2.0 (serveur, IPMI/BMC ASPEED AST2500) |
| CPU | AMD EPYC 7302P (Zen 2 Rome, 16C/32T, TDP 155W) |
| GPU | AMD Radeon RX 6800 16 Go (RDNA 2, Navi 21) |
| RAM | 64 Go DDR4 ECC Registered SK Hynix |
| Stockage | NVMe Crucial P310 2 To (PCIe Gen4) |
| OS | macOS Sequoia 15.7.7 (build 24G720) |
| Bootloader | OpenCore 1.0.5 |

## Résultats

- ✅ **32 threads SMT** reconnus par macOS (`hw.ncpu=32`, `hw.logicalcpu=32`, flag HTT actif)
- ✅ Geekbench 6 Single-Core : **1217** (+7,3 % au-dessus de la moyenne mondiale natif Linux/Windows)
- ✅ Geekbench 6 Multi-Core : **8207** (+3,6 % au-dessus de la moyenne mondiale)
- ✅ GPU OpenCL RX 6800 : **89761** (niveau Mac Pro 2019)
- ✅ Ethernet Intel natif, audio natif, USB 3.0 mappé proprement
- ✅ Boot direct depuis NVMe, station de travail stable, aucun freeze

**Résultat Geekbench public vérifiable :**
👉 https://browser.geekbench.com/v6/cpu/18196255

---

## Ce que ce repo ne contient PAS

⚠️ Je ne publie **pas** :
- Mon `config.plist`
- Mon dossier EFI complet
- Mes patches kernel binaires
- Mon image système

Ce projet est une **expérimentation personnelle, non commerciale, à but pédagogique**. Faire tourner macOS sur du matériel non-Apple ne respecte pas l'EULA d'Apple, qui réserve l'installation de macOS au matériel Apple. Pour un usage professionnel sérieux, un vrai Mac reste la voie sans risque.

## Remerciements

- **Micking (Michael Perche)** — qui m'a débloqué sur la question T2/SMBIOS quand j'étais sur le point d'abandonner
- **AMD_Vanilla** (algrey, Shaneee, Zormeister, Visual, Goldfish64) — sans leurs patches kernel, rien n'est possible
- **Acidanthera** — OpenCore, Lilu, VirtualSMC, WhateverGreen, NVMeFix, RestrictEvents
- Les communautés **amd-osx.com** et **InsanelyMac** — pour des années de documentation qui m'ont mené à 70 % du chemin

---

## Contact

Pour toute question technique : **contact@agence-paseo.fr**

— Jeremy « PASEO » Choulant
