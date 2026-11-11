# TP : Configuration d'un tunnel GRE over IPsec

## 1. Présentation du projet

Ce TP consiste à mettre en place un VPN Site-to-Site en utilisant les technologies **GRE (Generic Routing Encapsulation)** et **IPsec** sur des routeurs Cisco.

L'objectif est de permettre la communication sécurisée entre deux réseaux locaux distants à travers un réseau WAN.

## 2. Objectifs du TP

- Configurer les interfaces LAN et WAN des routeurs.
- Mettre en place le routage et la traduction NAT.
- Créer un tunnel GRE entre deux routeurs.
- Configurer IPsec pour sécuriser le trafic GRE.
- Vérifier la connectivité entre les deux sites.
- Analyser les paquets ESP avec Wireshark.

## 3. Environnement utilisé

- **GNS3** : Simulation de la topologie réseau.
- **Cisco IOS** : Configuration des routeurs.
- **Wireshark** : Capture et analyse du trafic réseau.

## 4. Topologie et adressage IP

| Équipement | Interface | Adresse IP |
|---|---|---|
| RouterA | Fa0/0 | 10.0.10.1/24 |
| RouterA | Serial1/0 | 201.20.20.1/30 |
| WAN | Serial0/0 | 201.20.20.2/30 |
| WAN | Serial0/1 | 204.20.20.1/30 |
| RouterB | Serial0/0 | 204.20.20.2/30 |
| RouterB | Fa0/0 | 10.0.20.1/24 |
| Tunnel GRE A | Tunnel0 | 172.16.1.1/24 |
| Tunnel GRE B | Tunnel0 | 172.16.1.2/24 |

## 5. Étapes de réalisation

### Partie 1 : Configuration du tunnel GRE

- Configuration des interfaces réseau.
- Configuration du NAT et des ACL.
- Configuration des routes par défaut.
- Création du tunnel GRE entre RouterA et RouterB.
- Configuration des routes statiques pour joindre les réseaux distants.

### Partie 2 : Sécurisation avec IPsec

- Activation du protocole ISAKMP.
- Configuration de la politique de sécurité VPN.
- Configuration de la clé pré-partagée.
- Création du transform-set IPsec.
- Création de l'ACL pour sélectionner le trafic GRE.
- Configuration et application de la crypto map.

## 6. Vérification et tests

Les commandes suivantes permettent de vérifier le fonctionnement du VPN :

```bash
show crypto isakmp sa
show crypto ipsec sa
show running-config
ping 10.0.20.1
```

Résultats observés :

- Association ISAKMP : ACTIVE.
- État de négociation : QM_IDLE.
- Associations IPsec ESP : ACTIVE.
- Connectivité vers le réseau distant : 100 % de réussite (5/5) lors du test final.
- Capture Wireshark : présence de paquets ESP dans les deux sens.

## 7. Analyse Wireshark

Une capture du trafic a été réalisée sur l'interface série de RouterA.

Le filtre utilisé est :

```bash
esp
```

La capture permet d'observer les paquets ESP échangés entre les deux routeurs, confirmant le chiffrement du trafic GRE sur le réseau WAN.

## 8. Conclusion

Ce TP nous a permis de comprendre et de mettre en pratique la configuration d'un VPN Site-to-Site basé sur GRE over IPsec.

GRE permet l'encapsulation du trafic entre les deux réseaux locaux, tandis qu'IPsec assure sa confidentialité et son intégrité pendant son transport sur le réseau WAN.

Les tests de connectivité, les commandes Cisco et l'analyse Wireshark ont permis de vérifier le fonctionnement de la solution.

---
