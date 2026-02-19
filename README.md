🛡️ Hardening & Sécurisation d'une Infrastructure Linux
Présentation du Projet
Ce projet consiste en la mise en place d'une infrastructure "endurcie" (Hardened) sur Ubuntu Server. L'objectif est de passer d'une configuration par défaut vulnérable à une architecture robuste capable de résister aux scans de reconnaissance et aux attaques par force brute.

Architecture du Lab
Le projet utilise une architecture virtualisée sous VMware Workstation comprenant trois entités:
-Serveur (Cible) : Ubuntu Server (IP : 192.168.1.10).
-Client (Confiance) : Debian (IP : 192.168.1.20) - Seule machine autorisée à l'administration.
-Attaquant : Kali Linux (IP : 192.168.1.30) - Utilisé pour l'audit et les tests d'intrusion.

Implémentations Techniques
1. Sécurisation du flux SSH
-Changement de port : Migration du port standard 22 vers le port 2222 pour éviter les scans automatisés.
-Filtrage IP (UFW) : Mise en place d'une politique default deny. Seule l'adresse IP de la machine Debian est autorisée à solliciter le port 2222.

2. Sécurisation du Serveur Web (Apache)
-Chiffrement SSL/TLS : Génération d'un certificat auto-signé pour activer le HTTPS sur le port 443.
-Redirection  : Configuration du module rewrite pour rediriger automatiquement tout le trafic du port 80 vers le port 443.
-Analyse de flux : Validation de la redirection et du chiffrement via Wireshark (observation des paquets 301 Moved Permanently).

3. Défense Active (Fail2Ban)
-Surveillance : Mise en place d'une "prison" (jail) surveillant les échecs d'authentification dans /var/log/auth.log.
-Politique de bannissement : Bannissement automatique d'une durée d'une heure après 3 tentatives infructueuses.

Conclusion
Ce Projet démontre que la sécurité ne repose pas sur un outil unique mais sur la complémentarité des couches défensives. L'audit régulier via des tests d'intrusion est indispensable pour valider la robustesse de la configuration technique
