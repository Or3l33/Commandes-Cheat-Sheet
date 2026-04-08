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
