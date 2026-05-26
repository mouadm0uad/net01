#  Rapport de Configuration Réseau

---

##  Paramètres Réseau

### 1. Configuration de l'interface principale

| Paramètre | Valeur |
|-----------|--------|
| **Adresse IP** | `192.168.0.201` |
| **Masque de sous-réseau** | `255.255.255.0` |
| **Passerelle par défaut** | `192.168.0.1` |
| **Serveur DNS primaire** | `205.151.222.250` |
| **Serveur DNS secondaire** | `205.151.222.251` |

---

### 2. Type d'adresse IP

**→ Adresse IP privée** 

> L'adresse `192.168.0.201` appartient à la plage **192.168.0.0 – 192.168.255.255**, qui est réservée aux adresses privées (RFC 1918).

#### Pourquoi est-ce une adresse privée ?

-  Ces plages sont conçues pour les **réseaux locaux (LAN)** uniquement
-  Elles ne sont **pas routables sur Internet** — un routeur NAT est nécessaire pour communiquer avec l'extérieur
-  Elles permettent de **préserver les adresses IPv4 publiques**, dont le nombre est limité

#### Les trois plages d'adresses privées (RFC 1918)

| Plage | Usage courant |
|-------|--------------|
| `10.0.0.0 – 10.255.255.255` | Grandes entreprises |
| `172.16.0.0 – 172.31.255.255` | Entreprises moyennes |
| `192.168.0.0 – 192.168.255.255` | Réseaux domestiques / PME |

---

### 3. Configuration de l'interface virtuelle (VM)

| Paramètre | Valeur |
|-----------|--------|
| **Adresse IP** | `10.0.2.15` |
| **Passerelle par défaut** | `10.0.2.2` |

>  La plage `10.0.2.x` est typiquement utilisée par les hyperviseurs (VirtualBox, QEMU) pour le réseau NAT des machines virtuelles. La passerelle `10.0.2.2` correspond à l'hôte physique.

---