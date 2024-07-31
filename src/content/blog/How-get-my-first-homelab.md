---
title: How to get my first homelab
author: Roman Cottinet
pubDatetime: 2024-07-30T22:00:00.000Z
modDatetime: 2024-07-30T22:00:00.000Z
slug: my-first-homelab
featured: true
draft: false
tags:
  - selfhost
  - homelab
description: ''
---

# Introduction

Vous avez toujours rêvé de gérer vos propres applications et services sans dépendre des grandes plateformes cloud souvent coûteuses et complexes ? Cet article est fait pour vous. Nous allons vous montrer comment créer un homelab pour déployer vos applications très simplement en utilisant Coolify et un serveur VPS chez Hetzner. Le tout, sans compromis sur la sécurité, la performance ou le contrôle de vos données.

### Prérequis

Avant de commencer, il est recommandé d'avoir quelques notions de base :

1. Connaître Docker
2. Savoir ce qu'est un VPS
3. Posséder un nom de domaine

## Table des matières

1. [Pourquoi un Homelab ?](#pourquoi-un-homelab)
2. [Par où commencer](#par-où-commencer)
   1. [Choisir et configurer votre serveur](#choisir-et-configurer-votre-serveur)
   2. [Connecter votre nom de domaine](#connecter-votre-nom-de-domaine)
3. [Installer Coolify](#installer-coolify)
   1. [Installation et configuration de Coolify](#installation-et-configuration-de-coolify)
   2. [Déployer vos premières applications](#déployer-vos-premières-applications)
4. [Pour aller plus loin](#pour-aller-plus-loin)
   1. [Backups sur S3](#backups-sur-s3)
   2. [Notifications sur Telegram](#notifications-sur-telegram)

***

## Pourquoi un Homelab ?

### Les avantages d'un homelab

Si je vous dis qu'il est possible de déployer des dizaines d'applications en 5 minutes depuis votre téléphone tout en gardant le contrôle total de vos données, le tout pour un coût financier entièrement maîtrisé, vous me croiriez ?

> *Mais pourquoi faire ça alors que j'ai déjà Vercel ou Supabase ? Il existe déjà plein de solutions pour déployer mes sites web ou applications rapidement..."*

C'est vrai, il existe de nombreuses options pour héberger vos applications, mais elles viennent souvent avec des inconvénients majeurs :

* **Complexité accrue** : Les plateformes comme AWS, Google Cloud ou Azure sont puissantes, mais leur courbe d'apprentissage est abrupte.
* **Coûts élevés** : Des services comme Vercel, Heroku ou d'autres startups promettent une simplicité d'utilisation, mais ces solutions peuvent rapidement devenir coûteuses, surtout si votre usage augmente.
* **Dépendance et limitations** : Beaucoup de ces services imposent des restrictions qui peuvent limiter vos projets ou vous lier à une plateforme spécifique.

### Pourquoi Hetzner et Coolify ?

En combinant un serveur VPS chez Hetzner et la plateforme Coolify, vous pouvez obtenir :

* **Contrôle total** : Vous êtes maître de vos données et de votre infrastructure.
* **Simplicité** : Coolify simplifie grandement le déploiement de vos applications grâce à une interface intuitive.
* **Coût maîtrisé** : Hetzner propose des VPS à des prix très compétitifs, ce qui vous permet de gérer vos coûts sans mauvaises surprises.

***

## Par où commencer

### Choisir et configurer votre serveur

#### Choisir la configuration

Chez [Hetzner](https://www.hetzner.com/cloud/), vous avez le choix entre plusieurs configurations de serveurs, allant du VPS basique à des machines plus puissantes. Pour un homelab de base, un VPS avec 2 vCPU, 4 Go de RAM et 40 Go de stockage est généralement suffisant. Vous pouvez toujours augmenter les ressources plus tard si nécessaire.

#### Configurer le serveur

Une fois votre serveur commandé, vous recevrez les accès SSH. Connectez-vous à votre serveur pour effectuer les premières configurations de sécurité :

1. **Mettre à jour le système** :

```bash
sudo apt update && sudo apt upgrade -y
```

1. **Configurer un pare-feu** :

```bash
sudo ufw allow OpenSSH
sudo ufw enable
```

### Connecter votre nom de domaine

Pour connecter votre nom de domaine à votre serveur, vous devrez créer un enregistrement A pointant vers l'adresse IP de votre VPS dans la gestion DNS de votre registrar. Cela permet d'accéder à vos services via un nom de domaine personnalisé.

***

## Installer Coolify

### Installation et configuration de Coolify

[Coolify](https://coolify.io/docs/introduction) se déploie via Docker, ce qui le rend facile à installer sur n'importe quel serveur. Pour l'installer :

1. **Installer Docker** :

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

1. **Installer Coolify** :

```bash
docker run -d --name coolify -v /var/run/docker.sock:/var/run/docker.sock -p 3000:3000 coollabsio/coolify
```

1. **Configurer Coolify** : Rendez-vous à l'adresse IP de votre serveur suivi du port `3000` (par exemple `http://votre-ip:3000`) pour accéder à l'interface de Coolify. Suivez les instructions pour finaliser la configuration.

### Déployer vos premières applications

Avec Coolify, déployer une application devient aussi simple que de remplir un formulaire :

1. **Ajouter une application** : Depuis l'interface de Coolify, sélectionnez "Add Application" et choisissez le type d'application que vous souhaitez déployer (Node.js, PHP, Docker, etc.).
2. **Configurer les paramètres** : Spécifiez les détails comme le dépôt Git, les variables d'environnement, et autres paramètres nécessaires.
3. **Déployer** : Cliquez sur "Deploy" et votre application sera en ligne en quelques minutes.

***

\
En suivant ce guide, vous serez en mesure de créer et gérer votre propre homelab, en ayant le contrôle total sur vos services, tout en maîtrisant vos coûts. Plongez-vous dans l’aventure du self-hosting et découvrez la liberté qu’un homelab peut offrir.
