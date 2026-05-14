# 🌐 Projet Solea — Infrastructure Hybride Multi-Sites
 
![Architecture Status](https://img.shields.io/badge/Status-Completed-success)
![Technology](https://img.shields.io/badge/Stack-Cisco%20|%20Proxmox%20|%20Debian-blue)
![Academic](https://img.shields.io/badge/Formation-L3%20TRI%20USMB-orange)
![Year](https://img.shields.io/badge/Année-2025--2026-lightgrey)
 
---
 
## 📌 Présentation du Projet
 
**Solea** est un projet d'infrastructure réseau et système complexe réalisé dans le cadre de la **Licence 3 TRI (Télécommunications et Réseaux Informatiques)** à l'**Université Savoie Mont Blanc (USMB)**, dans le cadre des modules **ETRS528_SPI** et **ETRS625_SPI**.
 
Le scénario simule une **refonte complète du système d'information** d'une entreprise spécialisée dans la conception et l'installation de panneaux solaires, en pleine forte croissance. L'infrastructure existante était vieillissante, mal sécurisée, difficile à gérer et manquait de robustesse.
 
### 🏢 Contexte Entreprise
 
| Site | Localisation | Rôle | Collaborateurs |
|------|-------------|------|---------------|
| Site 1 | Aix-les-Bains | Site principal | ~300 collaborateurs |
| Site 2 | Valence | Site secondaire (rachat récent) | ~30 collaborateurs |
 
**Objectifs de la refonte :**
- Concevoir et déployer une architecture réseau segmentée et sécurisée
- Mettre en place l'administration système (virtualisation, services)
- Déployer une solution de téléphonie IP (ToIP) sur les deux sites
- Interconnecter les deux sites de manière sécurisée via VPN
---
 
## 🏗️ Architecture Technique
 
L'infrastructure repose sur un **environnement hybride** combinant matériel physique et virtualisation :
 
### Couche Physique
- **Serveur :** Dell PowerEdge T340 (stockage en RAID 1 sur 2 disques physiques, 3ème disque en backup)
- **Réseau :** Routeurs et commutateurs Cisco (niveaux 2 et 3)
- **Accès distant :** iDRAC (Integrated Dell Remote Access Controller)
### Couche Virtualisation
- **Hyperviseur :** Cluster Proxmox VE
- **VMs déployées :** Templates Debian/Ubuntu minimalistes, machines de test TinyCore
### Services Déployés
 
| Catégorie | Services |
|-----------|---------|
| **Réseau** | DHCP, Routage Inter-VLAN (802.1Q), NAT/PAT, STP, VTP |
| **Système** | Serveurs Web, Base de données MariaDB, Serveur SSH |
| **Sécurité** | Firewall pfSense, VPN WireGuard (interconnexion inter-sites) |
| **ToIP** | IPBX, IP-Phones (site 1), Softphones & IP-Phones (site 2) |
 
### Segmentation VLAN
 
| VLAN | Usage |
|------|-------|
| VLAN 140 | Réseau interne principal (Aix-les-Bains) |
| VLAN 170 | Réseau secondaire / DMZ |
 
---
 
## 🖼️ Schéma de l'Infrastructure
 
![Architecture Réseau](./schemas/Solea_Architecture.png)
 
> Les schémas sources Draw.io sont disponibles dans le dossier `/schemas`.
 
---
 
## 🔄 Déroulement du Projet (3 Étapes)
 
Le projet a été réalisé en **3 sprints de 8h** avec rotation des sous-groupes pour partage de compétences :
 
### Étape 1 — Fondations (8h)
- **Sous-groupe A :** Simulation VLAN + Routage Inter-VLAN sous Cisco Packet Tracer
- **Sous-groupe B :** Mise en place serveur Dell T340 — Installation Proxmox VE — Configuration iDRAC
### Étape 2 — Services de base (8h)
- **Sous-groupe B :** Reprise simulation Packet Tracer + Ajout serveur DHCP
- **Sous-groupe A :** Création template VM Linux (Debian/Ubuntu) + Configuration commutateurs virtuels VLAN 140/170 sous Proxmox
### Étape 3 — Services avancés (8h)
- **Sous-groupe A :** Simulation NAT/PAT + Redirection de ports (accès SSH externe, hébergement web)
- **Sous-groupe B :** Configuration VLAN sur commutateurs physiques + Déploiement machine de test TinyCore (SSH, tcpdump, netcat, DHCP client)
---
 
## 🛠️ Compétences Validées
 
- **Design Réseau :** Conception de plans d'adressage IP et segmentation par VLAN
- **Configuration Cisco CLI :** Administration de switchs et routeurs (STP, VTP, routage statique/dynamique, NAT/PAT, 802.1Q)
- **Virtualisation :** Installation et optimisation de VMs sous Proxmox VE, gestion iDRAC, RAID 1
- **Administration Système :** Déploiement de services réseaux (DHCP, SSH, Web, MariaDB) sur Debian/Ubuntu
- **Sécurité :** Firewall pfSense, tunnels VPN WireGuard inter-sites, filtrage de flux
- **ToIP :** Déploiement IPBX, configuration IP-Phones et Softphones
- **Automatisation :** Scripts Bash/Python pour tests de connectivité et recettes techniques
- **Documentation Professionnelle :** Rédaction de cahiers de recettes, de tests et de documentations techniques au format professionnel
---
 
## 📂 Structure du Dépôt
 
```
Projet-Solea/
│
├── docs/                          # Documentations techniques
│   ├── Mise_en_place_physique.docx       # Guide déploiement physique (serveur, RAID, iDRAC)
│   ├── Proxmox_IDRAC_solea2.docx         # Configuration Proxmox et iDRAC
│   ├── PacketTracer_solea2.docx          # Documentation simulations réseau
│   ├── Cahier_tests.docx                 # Cahier de tests complet
│   └── Cahier_de_recette.docx            # Recettes techniques de validation
│
├── schemas/                       # Schémas et architectures
│   ├── Solea_Architecture.png            # Export PNG de l'architecture finale
│   ├── Architecture_reseaux.drawio       # Fichier source Draw.io
│   └── Carte_Solea.drawio                # Carte réseau globale
│
├── pkt/                           # Simulations Cisco Packet Tracer
│   ├── PacketTracer_etape1_solea2_sga.pkt
│   ├── PacketTracer_etape2_solea2_sgb.pkt
│   ├── PacketTracer_etape3_solea2_sga.pkt
│   └── PacketTracer_etape3_solea2_V4.pkt
│
├── scripts/                       # Scripts d'automatisation
│   └── (Scripts Bash/Python — tests de connectivité)
│
├── Suivi_de_projets.xlsx          # Tableau de suivi d'avancement
└── README.md
```
 
---
 
## 🚀 Technologies Utilisées
 
![Cisco](https://img.shields.io/badge/Cisco-CLI-1ba0d7?logo=cisco&logoColor=white)
![Proxmox](https://img.shields.io/badge/Proxmox-VE-E57000?logo=proxmox&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-Linux-A81D33?logo=debian&logoColor=white)
![pfSense](https://img.shields.io/badge/pfSense-Firewall-003f8c)
![WireGuard](https://img.shields.io/badge/WireGuard-VPN-88171A?logo=wireguard&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-Database-003545?logo=mariadb&logoColor=white)
![Draw.io](https://img.shields.io/badge/Draw.io-Schemas-F08705?logo=diagrams.net&logoColor=white)
![Packet Tracer](https://img.shields.io/badge/Packet%20Tracer-Simulation-1ba0d7?logo=cisco&logoColor=white)
 
---
 
## 👥 Équipe & Encadrement
 
| Rôle | Nom |
|------|-----|
| Étudiant (auteur) | **Omar Benmansour** |
| Encadrant (Proxmox/Système) | E. Rochefeuille |
| Encadrant (Réseau) | F. Lorne |
| Encadrants | E. Herault, B. Fléchet, PB. Vigneron |
 
---
 
## 📎 Informations Académiques
 
| Champ | Détail |
|-------|--------|
| **Formation** | L3 Télécommunications et Réseaux Informatiques (TRI) |
| **Établissement** | Université Savoie Mont Blanc (USMB) — Le Bourget-du-Lac |
| **Modules** | ETRS528_SPI · ETRS625_SPI |
| **Année** | 2025 – 2026 |
| **Date de présentation** | 17 Novembre 2025 |
 
---
 
## 🔗 Liens
 
- 🌐 **Portfolio :** [omarben04.github.io/portfolio](https://omarben04.github.io/portfolio/)
- 💼 **LinkedIn :** [linkedin.com/in/omar-benmansour](https://linkedin.com/in/omar-benmansour)
---
 
> *Ce projet représente un environnement de production simulé réel, intégrant haute disponibilité, segmentation réseau avancée et interconnexion sécurisée multi-sites.*
