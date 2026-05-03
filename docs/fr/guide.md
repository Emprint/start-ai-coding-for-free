# 🚀 Commencer le développement IA gratuitement

> **Pour qui ?** Les débutants complets, y compris les enfants, qui veulent créer des applications web avec l'aide de l'IA — sans payer.

> 📅 **Guide créé en mai 2026.** Les modèles gratuits disponibles sur NVIDIA Build peuvent changer à tout moment : certains peuvent devenir payants, de nouveaux peuvent apparaître, ou NVIDIA peut modifier son offre gratuite. Vérifie toujours la liste des modèles disponibles au moment où tu démarres un projet. La bonne nouvelle : OpenCode te permet de changer de modèle très facilement, même en cours de session.

---

## Table des matières

1. [Ce dont tu as besoin](#1-ce-dont-tu-as-besoin)
2. [Créer un compte NVIDIA et obtenir une clé API gratuite](#2-créer-un-compte-nvidia-et-obtenir-une-clé-api-gratuite)
3. [Choisir un modèle IA gratuit sur NVIDIA Build](#3-choisir-un-modèle-ia-gratuit-sur-nvidia-build)
4. [Installer Node.js et OpenCode](#4-installer-nodejs-et-opencode)
5. [Configurer OpenCode avec NVIDIA](#5-configurer-opencode-avec-nvidia)
6. [Ajouter Playwright MCP (l'IA qui contrôle le navigateur)](#6-ajouter-playwright-mcp-lia-qui-contrôle-le-navigateur)
7. [Créer ton premier projet sur GitHub](#7-créer-ton-premier-projet-sur-github)
8. [Démarrer ton application web avec l'IA](#8-démarrer-ton-application-web-avec-lia)

---

## 1. Ce dont tu as besoin

- Un ordinateur sous **macOS**, **Linux** ou **Windows** (PowerShell natif, WSL non obligatoire)
- Une connexion internet
- Environ **30 minutes** pour tout installer

Pas besoin de connaissances en programmation — c'est fait pour les débutants !

---

## 2. Créer un compte NVIDIA et obtenir une clé API gratuite

NVIDIA propose un accès **gratuit** à des modèles IA très puissants via sa plateforme **NVIDIA Build**.

> ⚠️ **Important — âge minimum requis :** Les conditions d'utilisation de NVIDIA exigent que le compte soit créé par **un adulte ayant atteint l'âge de la majorité légale** dans son pays (18 ans en France, Belgique, Canada…). Si tu es mineur, c'est **un parent ou tuteur** qui doit créer le compte et gérer la clé API à ta place.

### Étapes (à faire par un adulte si tu es mineur) :

1. Va sur [https://build.nvidia.com](https://build.nvidia.com)
2. Clique sur **Sign In / Create Account** en haut à droite
3. Crée un compte gratuit (avec ton adresse e-mail)
4. Une fois connecté, clique sur ton nom d'utilisateur en haut à droite → **API Keys**
5. Clique sur **Generate API Key**
6. Copie la clé — elle ressemble à : `nvapi-xxxxxxxxxxxxxxxxxxxx`

> ⚠️ **Important** : garde cette clé secrète, ne la partage jamais publiquement.  
> Le niveau gratuit inclut **1 000 crédits** renouvelés chaque mois, largement suffisant pour apprendre.

---

## 3. Choisir un modèle IA gratuit sur NVIDIA Build

NVIDIA Build donne accès à de nombreux modèles IA. Voici comment en choisir un gratuit :

1. Va sur [https://build.nvidia.com/models](https://build.nvidia.com/models)
2. Utilise le filtre **Free Endpoint** pour n'afficher que les modèles gratuits
3. Clique sur un modèle pour voir sa fiche — note l'**API endpoint ID** (ex: `mistralai/mistral-7b-instruct-v0.3`)

### Modèles recommandés pour débutants :

| Modèle | Spécialité | Points forts |
|---|---|---|
| `mistralai/mistral-7b-instruct-v0.3` | Général | Rapide, léger, parfait pour commencer |
| `minimaxai/minimax-m2.7` | Codage | Très capable, 204K contexte |
| `z-ai/glm4.7` | Codage & raisonnement | 358B paramètres, très puissant |

> 💡 Pour coder des applications web, **MiniMax M2.7** ou **GLM 4.7** sont d'excellents choix.

---

## 4. Installer Node.js et OpenCode

**Node.js** est nécessaire pour OpenCode, Playwright MCP et le développement web en général — autant l'installer en premier. On installe ensuite OpenCode via `npm`.

### Sur macOS :

Ouvre le **Terminal** (⌘+Espace, cherche "Terminal") et tape :

```bash
# Installer Homebrew si pas encore installé
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Installer Node.js
brew install node

# Installer OpenCode
npm install -g opencode-ai
```

### Sur Linux (Ubuntu/Debian) :

```bash
# Installer Node.js et npm
sudo apt update && sudo apt install nodejs npm

# Installer OpenCode
npm install -g opencode-ai
```

### Sur Windows (PowerShell — WSL non requis) :

Ouvre **PowerShell** (menu Démarrer → cherche "PowerShell") et choisis une des options :

**Option A — Via Chocolatey** (gestionnaire de paquets recommandé) :
```powershell
# Installer Chocolatey si pas encore installé (PowerShell en mode administrateur)
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Installer Node.js
choco install nodejs

# Installer OpenCode
npm install -g opencode-ai
```

**Option B — Via Scoop** :
```powershell
# Installer Scoop si pas encore installé
iwr -useb get.scoop.sh | iex

# Installer Node.js
scoop install nodejs

# Installer OpenCode
npm install -g opencode-ai
```

**Option C — Téléchargement direct** :
1. Va sur [https://nodejs.org](https://nodejs.org) et télécharge la version **LTS**
2. Lance l'installateur et suis les étapes
3. Ouvre un **nouveau** PowerShell, puis :
```powershell
npm install -g opencode-ai
```

> 💡 **Conseil Windows** : Installe [Windows Terminal](https://aka.ms/terminal) (gratuit sur le Microsoft Store) pour une bien meilleure expérience en ligne de commande.

### Vérifier l'installation :

```bash
node --version      # ex : v22.11.0 ✅
opencode --version  # ex : 1.14.25 ✅
```

---

## 5. Configurer OpenCode avec NVIDIA

OpenCode a besoin de savoir comment se connecter à NVIDIA. On va créer un fichier de configuration.

### Lancer OpenCode une première fois :

Lance OpenCode depuis n'importe quel dossier — il crée automatiquement son dossier de configuration au démarrage :

```bash
opencode
```

Appuie sur **q** pour quitter dès que l'interface s'affiche. Le dossier `~/.config/opencode/` existe maintenant.

### Ouvrir le fichier de config :

```bash
# Sur macOS / Linux :
nano ~/.config/opencode/opencode.json

# Sur Windows (PowerShell) :
notepad "$HOME\.config\opencode\opencode.json"
```

Colle ce contenu (remplace `TA_CLE_API` par ta vraie clé NVIDIA) :

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "nvidia-build": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "NVIDIA Build",
      "options": {
        "baseURL": "https://integrate.api.nvidia.com/v1",
        "apiKey": "TA_CLE_API"
      },
      "models": {
        "minimaxai/minimax-m2.7": {
          "name": "MiniMax M2.7 (gratuit)",
          "tool_call": true,
          "limit": { "context": 204800, "output": 8192 }
        },
        "z-ai/glm4.7": {
          "name": "GLM 4.7 (gratuit)",
          "tool_call": true,
          "limit": { "context": 131072, "output": 8192 }
        }
      }
    }
  }
}
```

Sauvegarde avec **Ctrl+O** puis **Entrée**, puis quitte avec **Ctrl+X** (ou simplement sauvegarde et ferme sur Windows).

### Tester la connexion :

Lance OpenCode dans un dossier quelconque :

```bash
cd ~
opencode
```

La première fois, OpenCode télécharge les paquets nécessaires (environ 1 minute).  
Tape `/models` pour voir tes modèles disponibles — tu devrais voir **MiniMax M2.7** et **GLM 4.7**. ✅

---

## 6. Ajouter Playwright MCP (l'IA qui contrôle le navigateur)

**Playwright MCP** donne à l'IA la capacité d'ouvrir un navigateur web, de cliquer sur des boutons, de remplir des formulaires et de prendre des captures d'écran — comme un humain le ferait.

> Node.js est déjà installé depuis l'étape 4, pas besoin de le réinstaller.

### Ajouter Playwright MCP à la config OpenCode :

Modifie ton fichier `~/.config/opencode/opencode.json` pour y ajouter la section `mcp` :

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "nvidia-build": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "NVIDIA Build",
      "options": {
        "baseURL": "https://integrate.api.nvidia.com/v1",
        "apiKey": "TA_CLE_API"
      },
      "models": {
        "minimaxai/minimax-m2.7": {
          "name": "MiniMax M2.7 (gratuit)",
          "tool_call": true,
          "limit": { "context": 204800, "output": 8192 }
        },
        "z-ai/glm4.7": {
          "name": "GLM 4.7 (gratuit)",
          "tool_call": true,
          "limit": { "context": 131072, "output": 8192 }
        }
      }
    }
  },
  "mcp": {
    "playwright": {
      "type": "local",
      "command": ["npx", "-y", "@playwright/mcp"],
      "enabled": true
    }
  }
}
```

### Installer les navigateurs Playwright :

```bash
npx playwright install chromium
```

> 💡 Avec Playwright MCP, tu peux demander à l'IA : *"Ouvre mon application dans le navigateur et teste si le bouton fonctionne"* — elle le fera automatiquement !

---

## 7. Créer ton premier projet sur GitHub

**GitHub** est un service gratuit pour stocker ton code en ligne et le partager avec le monde.

### Créer un compte GitHub :

1. Va sur [https://github.com](https://github.com)
2. Clique sur **Sign up** et crée un compte gratuit

### Créer un nouveau dépôt (repository) :

1. Une fois connecté, clique sur le **+** en haut à droite → **New repository**
2. Donne un nom à ton projet (ex: `ma-premiere-app-web`)
3. Coche **Add a README file**
4. Choisis **Public** (pour que tout le monde puisse le voir)
5. Clique sur **Create repository**

### Installer Git et cloner ton projet :

```bash
# Sur macOS :
brew install git
brew install gh

# Sur Linux (Ubuntu/Debian) :
sudo apt install git
sudo apt install gh  # ou : curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee ...

# Sur Windows (PowerShell) :
choco install git
choco install gh
# ou via Scoop :
scoop install git
scoop install gh
```

```bash
# Configurer ton identité Git (tous les systèmes) :
git config --global user.name "Ton Prénom"
git config --global user.email "ton@email.com"

# S'authentifier avec GitHub :
gh auth login
```

### Cloner ton projet sur ton ordinateur :

```bash
cd ~/Documents
gh repo clone TON_NOM_UTILISATEUR/ma-premiere-app-web
cd ma-premiere-app-web
```

---

## 8. Démarrer ton application web avec l'IA

Maintenant tu es prêt ! Voici comment travailler avec l'IA pour créer une application web.

### Lancer OpenCode dans ton projet :

```bash
cd ~/Documents/ma-premiere-app-web
opencode
```

### Choisir ton modèle :

Tape `/models` et sélectionne **MiniMax M2.7** ou **GLM 4.7**.

### Exemples de prompts pour démarrer :

Tu peux écrire des instructions en français directement à l'IA :

```
Crée une application web simple avec une page HTML qui affiche une liste de tâches à faire.
L'utilisateur doit pouvoir ajouter une tâche, la cocher comme terminée, et la supprimer.
Utilise du CSS moderne pour rendre l'interface jolie et responsive.
```

```
Crée un jeu de memory en HTML/CSS/JavaScript avec 12 cartes.
Les cartes doivent se retourner avec une animation fluide.
Ajoute un compteur de tentatives et un chronomètre.
```

L'IA va :
1. Créer les fichiers nécessaires
2. Écrire le code complet
3. Corriger les erreurs automatiquement

### Publier ton projet sur GitHub :

```bash
git add .
git commit -m "Mon premier projet avec l'IA"
git push
```

Ton code est maintenant en ligne sur GitHub ! 🎉

### Partager avec des amis :

Ton projet est visible à l'adresse :  
`https://github.com/TON_NOM_UTILISATEUR/ma-premiere-app-web`

Tu peux aussi activer **GitHub Pages** pour mettre ton application en ligne gratuitement :
1. Va dans les paramètres de ton dépôt → **Pages**
2. Sélectionne la branche **main**
3. Ton site sera disponible à : `https://TON_NOM_UTILISATEUR.github.io/ma-premiere-app-web`

---

## 🎓 Et après ?

- Essaie de demander à l'IA de **modifier** quelque chose dans ton projet
- Demande-lui d'**expliquer** le code qu'elle a écrit
- Lance une session avec Playwright : *"Ouvre mon application dans le navigateur et dis-moi si tout fonctionne"*
- Explore d'autres modèles gratuits sur [build.nvidia.com](https://build.nvidia.com)

---

## ❓ Problèmes fréquents

**OpenCode ne trouve pas mon modèle :**  
→ Vérifie que ta clé API est correcte dans `~/.config/opencode/opencode.json`

**Playwright ne se lance pas :**  
→ Lance `npx playwright install chromium` puis réessaie

**Git me demande un mot de passe :**  
→ Lance `gh auth login` et suis les étapes

---

*Guide créé avec ❤️ pour aider les débutants à découvrir le développement assisté par IA.*
