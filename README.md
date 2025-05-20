# 📡 Projet d'Analyse Réseau avec Wireshark/tshark  
*Capture et analyse des protocoles ARP, TCP, UDP sur Alcasar (10.10.0.1)*  

---

## 🧰 1. Installation et Configuration
### Prérequis
- 2 VMs Linux (Debian/Ubuntu)
- Interface réseau connectée à Alcasar (`10.10.0.1`)

### Installation
```bash
sudo apt update
sudo apt install wireshark tshark -y
sudo usermod -aG wireshark $USER
newgrp wireshark
```

🔍 2. Capture des Trames (Alcasar)
Commandes de base
bash
# Lancer Wireshark
sudo wireshark &

# Capture CLI avec tshark (30 secondes)
sudo tshark -i eth0 -a duration:30 -w alcasar_capture.pcapng
Filtres essentiels
Protocole	Filtre Wireshark	Exemple d'utilisation
ARP	arp	Résolution MAC/IP
TCP	tcp.port == 80	Traffic HTTP
UDP	udp.port == 53	Requêtes DNS
📊 3. Analyse OSI des Trames
Exemple de trame TCP
plaintext
ETHERNET II (Couche 2)
  SRC MAC: 08:00:27:ab:cd:ef
  DST MAC: 08:00:27:12:34:56
IPV4 (Couche 3)
  SRC IP: 10.10.0.100
  DST IP: 10.10.0.1
TCP (Couche 4)
  SRC PORT: 54321
  DST PORT: 80 (HTTP)
