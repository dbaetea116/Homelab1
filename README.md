# Homelab : mini-infrastructure d'entreprise virtualisée

Projet personnel réalisé sous VirtualBox pour pratiquer l'administration systèmes et réseaux. **Statut : en cours.**

## Objectif
Simuler le réseau d'une petite entreprise : un routeur-pare-feu, un contrôleur de domaine Windows, un poste client Windows 11 et un serveur Linux, répartis sur deux réseaux séparés.

## Architecture

| Machine | Rôle | Réseau | Adresse IP |
| --- | --- | --- | --- |
| OPNsense | Routeur / pare-feu | WAN (NAT), LAN-Entreprise, LAN-Serveurs | 192.168.10.1 et 192.168.20.1 |
| SRV-DC01 | Windows Server : Active Directory, DNS, DHCP | LAN-Entreprise | 192.168.10.10 (fixe) |
| PC-CLIENT01 | Windows 11 Pro | LAN-Entreprise | DHCP (192.168.10.100 à 200) |
| SRV-LINUX01 | Debian (sans interface graphique) | LAN-Serveurs | 192.168.20.10 (fixe) |

## Avancement
- [x] Machines virtuelles et réseaux internes VirtualBox
- [x] OPNsense installé, interfaces WAN / LAN / OPT1 et adresses configurées
- [x] Windows Server : domaine Active Directory `entreprise.local`, DNS, DHCP
- [x] Unités d'organisation, groupes (GRP-Compta, GRP-IT) et utilisateurs
- [x] Poste Windows 11 joint au domaine, adresse reçue par DHCP
- [x] GPO (verrouillage d'écran, Panneau de configuration) : créées, application au poste en cours de diagnostic
- [x] Serveur Debian : SSH par clé et pare-feu ufw
- [x] Règles de filtrage OPNsense entre les deux réseaux et tests de validation

## Difficultés rencontrées
- **Installateur pfSense** : il proposait uniquement la version Plus. J'ai choisi OPNsense, gratuit et installable avec une ISO classique.
- **Windows 11 dans VirtualBox** : écran noir au démarrage et message TPM / Secure Boot. Résolu en réglant la VM sans EFI et en contournant la vérification à l'installation.
- **Adresses IP et DNS incorrects sur le poste** : j'ai identifié, avec la ligne « Serveur DHCP » de `ipconfig /all`, que deux serveurs DHCP répondaient (OPNsense et Windows Server), puis j'ai désactivé celui d'OPNsense.
- **GPO non appliquées** : diagnostic avec `gpresult /r`, vérification de l'unité d'organisation des comptes et des liens des GPO.

## Prochaines étapes
Terminer les GPO, installer le serveur Debian avec accès SSH par clé, puis segmenter les réseaux avec les règles OPNsense.

## Outils
VirtualBox, OPNsense, Windows Server 2022, Windows 11, Debian, Active Directory, GPO, DNS, DHCP, SSH.
