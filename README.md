# 🛠️ Mon Aide-Mémoire Linux & PowerShell

Ce dépôt centralise les commandes essentielles pour administrer des systèmes Linux et automatiser des tâches sous Windows via PowerShell.

---

## 🐧 Section 1 : Linux (Bash / Shell)

### 📁 Gestion des Fichiers et Dossiers
| Commande | Description |
| :--- | :--- |
| `ls -lh` | Liste les fichiers avec une taille lisible (Ko, Mo) |
| `cd ..` | Remonter d'un dossier dans l'arborescence |
| `mkdir -p dossier/sous-dossier` | Créer une structure de dossiers complète |
| `cp -r source destination` | Copier un dossier et tout son contenu |
| `rm -rf cible` | **Attention :** Supprime récursivement et sans confirmation |

### 🔒 Permissions (chmod & chown)
| Commande | Action |
| :--- | :--- |
| `chmod 755 fichier` | Propriétaire (RWX), Groupe & Autres (R-X) |
| `chmod +x script.sh` | Rend un script exécutable |
| `sudo chown user:group fichier` | Change le propriétaire et le groupe |

### 🔍 Recherche et Système
| Commande | Action |
| :--- | :--- |
| `grep "mot" fichier` | Chercher un mot spécifique dans un fichier |
| `top` (ou `htop`) | Visualiser les ressources système en temps réel |
| `df -h` | Vérifier l'espace disque disponible |

---

## 🟦 Section 2 : PowerShell (Windows)

### ⚙️ Commandes de base (Cmdlets)
| Commande | Description |
| :--- | :--- |
| `Get-ChildItem` (ou `ls`) | Lister le contenu du dossier actuel |
| `Set-Location` (ou `cd`) | Changer de dossier |
| `Get-Help <commande> -Online` | Ouvre l'aide officielle dans le navigateur |

### 🌊 Utilisation du Pipeline ( | )
PowerShell fait passer des **objets** entre les commandes, pas juste du texte.
| Exemple | Utilité |
| :--- | :--- |
| `Get-Service | Where-Object Status -eq 'Running'` | Liste les services en cours d'exécution |
| `Get-Process | Sort-Object CPU -Descending | Select-Object -First 5` | Affiche les 5 processus les plus gourmands |

### 🛡️ Administration & Réseau
| Commande | Action |
| :--- | :--- |
| `Test-NetConnection -ComputerName 8.8.8.8` | Un "Ping" amélioré avec diagnostic portuaire |
| `Get-ExecutionPolicy` | Vérifier si l'exécution de scripts est autorisée |
| `Set-ExecutionPolicy RemoteSigned` | Autorise tes scripts locaux à s'exécuter |
# 📂 Analyse et Nettoyage de Disque (PowerShell)

Ce guide regroupe des commandes utiles pour identifier les fichiers volumineux et nettoyer l'espace disque sur Windows.

> **Note :** Toutes ces commandes doivent être exécutées dans un terminal **PowerShell** en mode **Administrateur**.

---

## 🔍 Analyse de l'espace disque

### Lister les 20 plus gros fichiers du disque
Cette commande scanne tout le disque `C:\`, trie les fichiers par taille et affiche les 20 premiers résultats dans un tableau lisible.
```powershell
Get-ChildItem -Path "C:\" -Recurse -File -ErrorAction SilentlyContinue | `
Sort-Object Length -Descending | `
Select-Object -First 20 | `
Select-Object Name, @{Name="Size(GB)";Expression={[Math]::Round($_.Length / 1GB, 2)}}, FullName
---


## 💡 Notes personnelles
> * Sous Linux, tout est fichier.
> * Sous PowerShell, tout est objet.
> * En cas de doute sous Linux : `man <commande>`.

# 🎹 Cheat Sheet : Gestion de Musique & Serveur Orange Pi

Ce guide récapitule les commandes essentielles pour synchroniser de la musique depuis Windows vers un serveur Navidrome sur Orange Pi, ainsi que la gestion des services Docker.

## 🚀 Transfert de fichiers (Depuis Windows PowerShell)

Utilisation de **Rclone** pour une synchronisation intelligente (évite les doublons).

| Commande | Description |
| :--- | :--- |
| `rclone copy "D:\Music" :sftp:/home/orangepi/navidrome/music/ --sftp-host 192.168.1.53 --sftp-user orangepi --sftp-ask-password --progress --ignore-existing` | Synchronise le disque D: vers l'OPI (ignore les fichiers déjà présents). |
| `scp -r "D:\Music\Album" orangepi@192.168.1.53:/home/orangepi/navidrome/music/` | Copie rapide d'un dossier spécifique via SSH. |

## 🐳 Gestion des services Docker (Sur l'Orange Pi)

| Commande | Description |
| :--- | :--- |
| `docker ps` | Liste les containers actifs (Navidrome, Home Assistant, etc.). |
| `docker ps -a` | Liste tous les containers (même arrêtés). |
| `docker logs -f <nom_container>` | Affiche les logs en temps réel (pour débugger). |
| `docker restart <nom_container>` | Redémarre un service spécifique. |
| `docker stats` | Affiche la consommation CPU/RAM des containers en direct. |

## ⚙️ Maintenance & Système (Sur l'Orange Pi)

| Commande | Description |
| :--- | :--- |
| `hostname -I` | Affiche toutes les adresses IP du serveur (Local, Tailscale, Docker). |
| `df -h` | Vérifie l'espace disque restant sur la carte SD. |
| `sudo systemctl enable docker` | Active le lancement automatique de Docker au démarrage. |
| `sudo apt autoremove` | Nettoie les paquets système inutiles. |
| `sudo reboot` | Redémarre proprement le serveur. |

## 📂 Navigation & Nettoyage des dossiers

| Commande | Description |
| :--- | :--- |
| `ls -lhF` | Liste les fichiers et dossiers avec détails et tailles. |
| `tree -d -L 2` | Affiche l'arborescence des dossiers (Artistes > Albums). |
| `fdupes -r /chemin/` | Recherche les fichiers doublons (basé sur le contenu). |
| `fdupes -rdN /chemin/` | Supprime les doublons automatiquement en gardant un seul exemplaire. |
| `find . -type d -empty -delete` | Supprime tous les dossiers vides après un nettoyage. |

## 🌐 Accès aux Services
- **Navidrome :** `http://192.168.1.53:4533`
- **Home Assistant :** `http://192.168.1.53:8123`
- **IP Tailscale (Distance) :** `100.68.96.85`
