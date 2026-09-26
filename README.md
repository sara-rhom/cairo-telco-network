# Réseau sécurisé pour une entreprise de télécommunications — Cairo Telco

Projet de conception et d'implémentation d'une infrastructure réseau d'entreprise sécurisée, fiable et évolutive, réalisé sur **Cisco Packet Tracer** dans le cadre d'un stage d'observation (projet laboratoire).

## 📋 Contexte

Cairo Telco est une entreprise de télécommunications fictive basée au Caire, répartie sur plusieurs départements (RH & Finance, Marketing, Admin & Corporate, IT Network & Support, Software Engineering, Cloud Engineering) et disposant d'une agence distante reliée au siège via VPN.

## 🏗️ Architecture

- Modèle hiérarchique **Cœur / Distribution / Accès**
- Segmentation par VLAN (filaire, WiFi, VoIP) avec routage inter-VLAN
- Zone **DMZ** hébergeant les serveurs (AD/DHCP/DNS, ERP, Email, File Storage, Syslog)
- Pare-feu Cisco ASA structurant le réseau en zones de sécurité (INSIDE / DMZ / OUTSIDE)
- Agence distante connectée au siège via tunnel **VPN IPsec**

## ⚙️ Technologies mises en œuvre

| Domaine | Technologies |
|---|---|
| Architecture | Hiérarchique (Cœur, Distribution, Accès) |
| Adressage | VLAN, SVI, routage inter-VLAN, DHCP (relais via `ip helper-address`) |
| Routage | OSPF (routage dynamique) |
| Sécurité | ACL standard/étendues, SSH sécurisé, pare-feu (zones, NAT, ACL d'inspection) |
| Haute disponibilité | HSRP + second commutateur de cœur, EtherChannel, STP (PortFast, BPDU Guard) |
| VoIP | Passerelle voix Cisco |
| Sans fil | Contrôleur WLAN (WLC) + points d'accès légers |
| Interconnexion | Tunnel VPN IPsec site-à-site |
| Supervision | Serveur Syslog centralisé |

## 📁 Structure du dépôt

```
├── topologie/          # Fichier(s) Packet Tracer (.pkt)
├── configs/             # Configurations CLI des équipements
├── captures/            # Captures d'écran de validation (tests, topologie)
└── README.md
```

## 🧪 Tests réalisés

Un scénario de test d'intégration valide le fonctionnement combiné de toutes les briques du réseau :

1. Attribution d'IP via DHCP (relais + OSPF)
2. Connexion SSH sécurisée à l'IP admin autorisée
3. Ping chiffré vers le site distant via le tunnel IPsec
4. Simulation de panne du commutateur de cœur principal → bascule HSRP
5. Vérification de la traçabilité de l'incident sur le serveur Syslog
6. Reprise automatique du rôle actif après rétablissement (preemption)

## 🛠️ Prérequis

- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (version 8.x recommandée)

## ⚠️ Limitations connues

Certaines fonctionnalités ont été adaptées en raison de contraintes du simulateur Packet Tracer (absence de commandes `logging` sur l'ASA simulé, protocole GLBP indisponible — HSRP utilisé en alternative).

## 👤 Auteur

Sara — Étudiante en Génie des Réseaux et Systèmes de Télécommunications (GRST), ENSA Kénitra
