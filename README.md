# 🖧 Communication entre Machines Virtuelles sous VMware Workstation

> Rapport technique — Configuration d'un réseau interne isolé entre deux machines
> virtuelles VMware Workstation sur Debian, sans connexion internet sur la machine hôte.

---

## 📋 Description

Ce dépôt contient le rapport technique complet rédigé en **LaTeX** couvrant
la mise en place d'une infrastructure réseau virtuelle isolée.
Le document traite de la création de deux machines virtuelles sous
**VMware Workstation**, de leur mise en réseau via un adaptateur
**Host-only**, et de la configuration d'adresses IP statiques persistantes
sous **Debian**.

---
### Pour reproduire la manipulation

| Logiciel | Rôle |
|---|---|
| VMware Workstation | Hyperviseur |
| Debian 11 / 12 | Système invité des VMs |
| Machine hôte | Windows / Linux |

---

## 🚀 Compilation
```bash
# Cloner le dépôt
git clone https://github.com/<votre-user>/<nom-du-depot>.git
cd <nom-du-depot>

---

## 📖 Contenu du rapport

| Chapitre | Contenu |
|---|---|
| 1. Introduction | Contexte, objectifs, environnement de travail |
| 2. Création des VMs | Assistant VMware, paramètres, ISO |
| 3. Configuration réseau | Virtual Network Editor, mode Host-only |
| 4. Configuration IP | Adresses statiques, suppression DHCP, persistance Debian |
| 5. Tests de communication | Ping bidirectionnel, SSH |
| 6. Résolution des problèmes | Problèmes courants et solutions |
| 7. Conclusion | Récapitulatif et points clés |

---

## 🌐 Architecture mise en place
```
┌─────────────────────────────────────────────────┐
│              Machine hôte (VMware)              │
│                                                 │
│  ┌─────────────┐   VMnet1    ┌─────────────┐   │
│  │     VM1     │◄───────────►│     VM2     │   │
│  │             │  Host-only  │             │   │
│  │ 192.168.10.1│             │ 192.168.10.2│   │
│  │   Debian    │             │   Debian    │   │
│  └─────────────┘             └─────────────┘   │
│                                                 │
│            Pas d'accès internet                 │
└─────────────────────────────────────────────────┘
```

---

## ⚙️ Commandes essentielles
```bash
# Vérifier les interfaces réseau
ip link show

# Supprimer une adresse DHCP résiduelle
sudo dhclient -r ens33
sudo ip addr del <IP>/24 dev ens33

# Configurer une adresse statique (temporaire)
sudo ip addr add 192.168.10.1/24 dev ens33
sudo ip link set ens33 up

# Tester la communication
ping -c 4 192.168.10.2
```

---

## 📝 Auteur

**Manoach HOSSOU DODO**
Mars 2026

---

## 📄 Licence

Ce document est partagé à des fins pédagogiques.
Toute réutilisation doit mentionner l'auteur original.
