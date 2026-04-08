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

---

## 💡 Notes personnelles
> * Sous Linux, tout est fichier.
> * Sous PowerShell, tout est objet.
> * En cas de doute sous Linux : `man <commande>`.
