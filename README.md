# 🦈 Projet Wireshark - Analyse Réseau sous Linux

![Banner Wireshark](https://www.wireshark.org/assets/images/wsrk-banner@2x.png)

## 📌 Objectifs
- Capturer et analyser les trames réseau (ARP, TCP, UDP, DNS)
- Comprendre le modèle OSI à travers des cas pratiques
- Automatiser les captures avec `tshark`

## 🚀 Installation
```bash
sudo apt update && sudo apt install wireshark tshark -y
sudo usermod -aG wireshark $USER
newgrp wireshark
```
Analyse : Three-way handshake
sequenceDiagram
    Client->>Serveur: SYN
    Serveur->>Client: SYN-ACK
    Client->>Serveur: ACK


📊 Analyse OSI (Exemple TCP)
Couche	Données
Liaison (2)	MAC Source: 08:00:27:ab:cd:ef
Réseau (3)	IP Destination: 10.10.0.1
Transport (4)	Port TCP: 443 (HTTPS)



⚠️ Sécurité
FTP : Identifiants visibles en clair

bash
tshark -Y "ftp.request.command == USER" -V
HTTPS : Données chiffrées (TLS)

🤖 Scripts d'Automatisation
bash
#!/bin/bash
# Capture DNS pendant 60s
tshark -i eth0 -Y "dns" -a duration:60 -w captures/dns.pcapng
