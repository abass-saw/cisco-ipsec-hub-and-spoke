# Conception et Déploiement d'un VPN IPsec Hub-and-Spoke

Projet Technique Personnel — Ingénierie Réseaux & Sécurité WAN
Auteur : Mahmoud Abass SAWADOGO (Fès, Maroc)
Environnement : Cisco IOS c7200, GNS3, Wireshark, VPCS

---

Description du Projet
Interconnexion sécurisée et étanche entre le réseau local d'un Siège (10.10.0.0/24) et deux agences distantes (10.20.0.0/24 et 10.30.0.0/24) à travers un réseau WAN public d'opérateur Internet simulé, sans routage privé préalable (RFC 1918).

Points Clés de l'Architecture
- Découplage Underlay/Overlay : liaisons WAN en sous-réseaux /30 et routage par défaut étanche (0.0.0.0/0).
- Suite Cryptographique : IKEv1 Phase 1 (AES-256, SHA-1, DH Groupe 2, PSK) et IPsec Phase 2 (ESP-AES-256 en Mode Tunnel).
- Transit Inter-Agences (Hairpinning) : relais et ré-encapsulation chiffrée par le concentrateur central pour relier Spoke 1 et Spoke 2 sans maillage complet.

Validation et Résultats
- Audit Wireshark : flux entièrement encapsulé en protocole ESP (IP 50) sur le lien opérateur public, masquage des adresses privées et corrélation exacte des registres SPI.
- Fiabilité Cisco : zéro erreur de commutation chiffrée (#send errors 0, #recv errors 0).
- Test Applicatif : ping à 100% avec TTL=61 (preuve de traversée de 3 routeurs dont le Hub) et terminaison de sonde UDP par code ICMP Type 3 / Code 3.

Contenu du Dépôt
- configs/ : configurations complètes des routeurs Cisco (R1-HUB, R-ISP, R2-SPOKE1, R3-SPOKE2) et des VPCS.
- LAB_VPN_IP_IPSEC_HUB_SPOKE.gns3 : topologie prête à l'emploi sous GNS3.
- RAPPORTS_DE_PROJET_VPN_IPSEC.pdf : rapport technique d'ingénierie complet avec captures et analyses.
