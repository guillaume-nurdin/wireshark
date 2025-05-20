Partie 1 : Prise en main de Wireshark
1. Présentation de Wireshark
Wireshark est un analyseur de paquets permettant :

La capture en temps réel du trafic réseau.

Le filtrage des trames (par protocole, adresse IP, port, etc.).

La désencapsulation des paquets selon les couches OSI.

2. Questions théoriques
🔹 Différence entre une trame et un paquet ?

Trame (Couche 2 - Liaison) : Contient les adresses MAC (ex: 08:00:27:ab:cd:ef).

Paquet (Couche 3 - Réseau) : Contient les adresses IP (ex: 10.10.0.1).

🔹 Formats PCAP et PCAPNG ?

PCAP : Ancien format de capture.

PCAPNG : Nouveau format (supporte métadonnées, commentaires).

3. Capture des paquets sur Alcasar (IP : 10.10.0.1)
   
Installation et lancement :
bash
sudo apt update && sudo apt install wireshark tshark -y
sudo wireshark &  # Lancement en root
Interface à sélectionner : eth0 (ou celle connectée à Alcasar).


🔹 Paquets à capturer :
Protocole	Filtre Wireshark	Exemple d'analyse

ARP	--- arp	= Résolution IP → MAC

UDP ---	udp =	Flux média, DNS

TCP ---	tcp	= HTTP, HTTPS, FTP


Exemple de trame TCP :

---MAC Source : 08:00:27:ab:cd:ef

---IP Source : 10.10.0.100

---MAC Destination : 08:00:27:12:34:56

---IP Destination : 10.10.0.1 (Alcasar)

🔹 Désencapsulation OSI :

Couche        	    Élément analysé

Liaison (2)	        Adresses MAC

Réseau (3)	        Adresses IP

Transport (4)     	Ports TCP/UDP

Application (7)   	HTTP, DNS, FTP



🔹 Connexion TCP (3-Way Handshake)

Client → SYN → Serveur

Client ← SYN-ACK ← Serveur

Client → ACK → Serveur

Partie 2 : Analyse avancée des protocoles

1. Protocoles à étudier (VM en NAT)
Protocole	     Filtre Wireshark	      Observations

DHCP	      -- bootp  --             	Attribution IP

DNS	        -- dns	  --              Résolution de noms

mDNS	      -- mdns	  --              DNS local (.local)

FTP         -- ftp	  --              ⚠️ Mots de passe en clair !

HTTPS       -- tls    --	            Chiffré (sécurisé)



3. Sécurité des protocoles

_ FTP non sécurisé : Login/mot de passe visibles dans les paquets.

_ HTTPS/TLS : Données chiffrées → impossible de lire les identifiants.

_ Partie 3 : Automatisation avec tshark


1. Installation
```sudo apt install tshark```

3. Commandes utiles
Action	Commande
Capture DNS	```sudo tshark -i eth0 -Y "dns" -w dns.pcapng```

Capture HTTP	```sudo tshark -i eth0 -Y "http" -w http.pcapng```

Export en texte	```tshark -r capture.pcapng -V > analyse.txt```

5. Filtres avancés
```bash
tshark -i eth0 -Y "ip.src == 10.10.0.1"  # Filtre par IP source
tshark -i eth0 -Y "tcp.port == 443"      # HTTPS
```
Conclusion & Compétences Validées
✅ Administration réseau : Capture et analyse des trames.
✅ Sécurité : Identification des protocoles non sécurisés (FTP).
✅ Automatisation : Scripts Bash avec tshark.
