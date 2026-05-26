# 🌐 Rapport de Diagnostic Réseau

---

##  Résultats des Tests

### Test 1 — Ping vers `google.com`

```
PING google.com (142.250.69.78) 56(84) bytes of data.
64 bytes from tzyula-aa-in-f14.1e100.net (142.250.69.78): icmp_seq=1 ttl=255 time=19.9 ms
64 bytes from tzyula-aa-in-f14.1e100.net (142.250.69.78): icmp_seq=2 ttl=255 time=262 ms
64 bytes from tzyula-aa-in-f14.1e100.net (142.250.69.78): icmp_seq=3 ttl=255 time=1156 ms
64 bytes from tzyula-aa-in-f14.1e100.net (142.250.69.78): icmp_seq=4 ttl=255 time=149 ms
```

---

### Test 2 — Ping vers `8.8.8.8` (DNS Google)

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=255 time=1066 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=255 time=1553 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=255 time=409 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=255 time=24.6 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3752ms
rtt min/avg/max/mdev = 24.560/763.204/1552.854/588.622 ms, pipe 2
```

---

### Test 3 — Traceroute

```
Command 'traceroute' not found, but can be installed with:
  sudo apt install traceroute            # version 1:2.1.5-1
  sudo apt install inetutils-traceroute  # version 2:2.5-3ubuntu4.1
```

>  **traceroute** n'est pas installé sur cette machine.

---

### Test 4 — Résolution DNS de `google.com`

```
Server:   127.0.0.53
Address:  127.0.0.53#53

Non-authoritative answer:
Name:    google.com
Address: 142.250.69.78
Name:    google.com
Address: 2607:f8b0:4020:802::200e
```

---

### Test 5 — Résolution DNS de `github.com`

```
Server:   127.0.0.53
Address:  127.0.0.53#53

Non-authoritative answer:
Name:    github.com
Address: 140.82.114.4
```

---

##  Analyse des Résultats

### 1. Que font ces commandes ?

| Commande | Rôle |
|----------|------|
| `ping` | Teste la connectivité réseau en envoyant des paquets ICMP vers une destination et mesure le temps de réponse (latence). |
| `nslookup` *(tests 4 & 5)* | Interroge un serveur DNS pour obtenir l'adresse IP associée à un nom de domaine. |
| `traceroute` *(test 3)* | Affiche le chemin parcouru par les paquets jusqu'à la destination — **non installé ici**. |

---

### 2. Ce que les résultats révèlent

-  **Connexion Internet fonctionnelle** — 0% de perte de paquets
-  **Latence variable et élevée** — les temps de réponse fluctuent fortement (de 19 ms à 1553 ms), ce qui peut indiquer une instabilité réseau
-  **DNS opérationnel** — les noms de domaine sont correctement résolus :
  - `google.com` → `142.250.69.78`
  - `github.com` → `140.82.114.4`
- ℹ **Résolveur DNS local** utilisé : `127.0.0.53` (systemd-resolved)

---

### 3. Différence entre `ping google.com` et `ping 8.8.8.8`

| | `ping google.com` | `ping 8.8.8.8` |
|---|---|---|
| **Résolution DNS** |  Oui — traduit le nom en IP |  Non — IP directe |
| **Ce qui est testé** | DNS **+** connectivité réseau | Connectivité réseau uniquement |
| **Utilité** | Vérifie que le DNS fonctionne | Isole les problèmes réseau purs |

>  Si `ping 8.8.8.8` fonctionne mais pas `ping google.com`, le problème vient du DNS et non de la connexion réseau.


