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
| `sudo chown <USER>:<GROUP> fichier` | Change le propriétaire et le groupe |

---

## 🟦 Section 2 : PowerShell (Windows)

### ⚙️ Commandes de base

| Commande | Description |
| :--- | :--- |
| `Get-ChildItem` | Lister le contenu du dossier actuel |
| `Set-Location` | Changer de dossier |
| `Get-Help <commande> -Online` | Aide officielle en ligne |

### 🔍 Analyse de l'espace disque (Admin)

```powershell
# Lister les 20 plus gros fichiers du disque C:
Get-ChildItem -Path "C:\" -Recurse -File -ErrorAction SilentlyContinue | `
Sort-Object Length -Descending | `
Select-Object -First 20 | `
Select-Object Name, @{Name="Size(GB)";Expression={[Math]::Round($_.Length / 1GB, 2)}}, FullName

🎹 Section 3 : Gestion Musique & Orange PiCe guide récapitule les commandes pour synchroniser de la musique vers un serveur Navidrome sur Orange Pi.🚀 Transfert de fichiers (Depuis PowerShell)CommandeDescriptionrclone copy "<DOSSIER_SOURCE>" :sftp:/<DESTINATION>/ --sftp-host <IP_LOCALE> --sftp-user <USER> --sftp-ask-password --progress --ignore-existingSynchronise le dossier local vers l'OPi via SFTP.scp -r "<ALBUM>" <USER>@<IP_LOCALE>:/<DESTINATION>/Copie rapide d'un album spécifique via SSH.🐳 Gestion des services DockerCommandeDescriptiondocker psListe les containers actifs (Navidrome, Home Assistant, etc.).docker logs -f <NOM_CONTAINER>Affiche les logs en temps réel pour débugger.docker restart <NOM_CONTAINER>Redémarre un service spécifique.docker update --restart unless-stopped <NOM>Active le redémarrage automatique.⚙️ Maintenance SystèmeCommandeDescriptionhostname -IAffiche toutes les adresses IP du serveur.df -hVérifie l'espace disque restant (Carte SD).sudo systemctl enable dockerActive Docker au démarrage du système.sudo apt autoremoveNettoie les paquets système inutiles.📂 Navigation & NettoyageCommandeDescriptiontree -d -L 2 /chemin/Affiche l'arborescence (Artistes > Albums).fdupes -r /chemin/Recherche les fichiers doublons.fdupes -rdN /chemin/Supprime les doublons automatiquement.🌐 Accès aux ServicesNavidrome (Local) : http://<IP_LOCALE>:4533Home Assistant : http://<IP_LOCALE>:8123Accès VPN (Tailscale) : http://<IP_TAILSCALE>:4533💡 Note : Remplacer <IP_LOCALE> par votre IP privée (ex: 192.168.1.53) et <IP_TAILSCALE> par votre IP VPN (ex: 100.x.x.x).
