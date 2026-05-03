# 🚀 Commencer le développement IA gratuitement

> **Pour qui ?** Les débutants complets, y compris les enfants, qui veulent créer des applications web avec l'aide de l'IA — sans payer.

> 📅 **Guide créé en mai 2026.** Les modèles gratuits disponibles sur NVIDIA Build peuvent changer à tout moment : certains peuvent devenir payants, de nouveaux peuvent apparaître, ou NVIDIA peut modifier son offre gratuite. Vérifie toujours la liste des modèles disponibles au moment où tu démarres un projet. La bonne nouvelle : OpenCode te permet de changer de modèle très facilement, même en cours de session.

---

## Table des matières

1. [Ce dont tu as besoin](#1-ce-dont-tu-as-besoin)
2. [Créer un compte NVIDIA et obtenir une clé API gratuite](#2-créer-un-compte-nvidia-et-obtenir-une-clé-api-gratuite)
3. [Choisir un modèle IA gratuit sur NVIDIA Build](#3-choisir-un-modèle-ia-gratuit-sur-nvidia-build)
4. [Installer Node.js et OpenCode](#4-installer-nodejs-et-opencode)
5. [Configurer OpenCode avec NVIDIA et Playwright MCP](#5-configurer-opencode-avec-nvidia-et-playwright-mcp)
6. [Créer ton compte GitHub et installer Git](#6-créer-ton-compte-github-et-installer-git)
7. [Construire ton application web avec l'IA](#7-construire-ton-application-web-avec-lia)

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
2. Clique sur le filtre **Free Endpoint**
3. Clique sur **Apply** pour appliquer le filtre — la liste se met à jour avec uniquement les modèles gratuits
4. Clique sur un modèle pour voir sa fiche — note l'**API endpoint ID** (ex: `mistralai/mistral-7b-instruct-v0.3`)

### Modèles recommandés pour débutants :

| Modèle | Spécialité | Points forts |
|---|---|---|
| `mistralai/mistral-7b-instruct-v0.3` | Général | Rapide, léger, parfait pour commencer |
| `minimaxai/minimax-m2.7` | Codage | Très capable, 204K contexte |
| `z-ai/glm4.7` | Codage & raisonnement | 358B paramètres, très puissant |

> 💡 Pour coder des applications web, **MiniMax M2.7** ou **GLM 4.7** sont d'excellents choix.

---

## 4. Installer Node.js et OpenCode

**Node.js** est un environnement qui permet d'exécuter du code en dehors d'un navigateur — il est nécessaire pour OpenCode et Playwright. On l'installe en premier, puis on installe OpenCode.

> 💡 **C'est quoi le terminal ?** C'est une fenêtre où tu tapes des commandes textuelles pour interagir avec ton ordinateur. Sur macOS, cherche "Terminal" dans Spotlight (⌘+Espace). Sur Windows, cherche "PowerShell" dans le menu Démarrer. Sur Linux, cherche "Terminal" dans les applications.

### Sur macOS :

1. Va sur [https://nodejs.org](https://nodejs.org) et télécharge la version **LTS**
2. Lance l'installateur `.pkg` et suis les étapes
3. Ouvre le **Terminal**, puis tape :

```bash
npm install -g opencode-ai
```

### Sur Linux (Ubuntu/Debian) :

Ouvre un **Terminal** et tape :

```bash
sudo apt update && sudo apt install nodejs npm
npm install -g opencode-ai
```

### Sur Windows :

**Option A — Téléchargement direct (recommandé pour les débutants) :**
1. Va sur [https://nodejs.org](https://nodejs.org) et télécharge la version **LTS**
2. Lance l'installateur `.msi` et suis les étapes
3. Ouvre **PowerShell** (menu Démarrer → "PowerShell"), puis tape :

```powershell
npm install -g opencode-ai
```

**Option B — Via Chocolatey** (gestionnaire de paquets Windows) :
```powershell
# Dans PowerShell en mode administrateur :
choco install nodejs
npm install -g opencode-ai
```

**Option C — Via Scoop** :
```powershell
scoop install nodejs
npm install -g opencode-ai
```

> 💡 **Conseil Windows** : Installe [Windows Terminal](https://aka.ms/terminal) (gratuit sur le Microsoft Store) pour une meilleure expérience en ligne de commande.

### Vérifier l'installation :

Dans ton terminal, tape les commandes suivantes pour vérifier que tout est bien installé :

```bash
node --version      # doit afficher quelque chose comme v22.11.0
opencode --version  # doit afficher quelque chose comme 1.14.25
```

Si les deux commandes affichent un numéro de version, c'est parfait ! ✅

---

## 5. Configurer OpenCode avec NVIDIA et Playwright MCP

OpenCode a besoin de savoir comment se connecter à NVIDIA. On va créer un fichier de configuration qui inclut également **Playwright MCP** — l'outil qui permet à l'IA de contrôler un navigateur web.

### Lancer OpenCode une première fois :

OpenCode crée automatiquement son dossier de configuration au premier démarrage. Lance-le depuis n'importe quel dossier :

```bash
opencode
```

Appuie sur **q** pour quitter dès que l'interface s'affiche. Le dossier de configuration a été créé.

### Ouvrir le fichier de config :

Dans ton terminal, ouvre le fichier de configuration :

```bash
# Sur macOS / Linux :
nano ~/.config/opencode/opencode.json

# Sur Windows (PowerShell) :
notepad "$HOME\.config\opencode\opencode.json"
```

### Coller la configuration complète :

Remplace tout le contenu du fichier par ce qui suit (remplace `TA_CLE_API` par ta vraie clé NVIDIA) :

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

Sauvegarde avec **Ctrl+O** puis **Entrée**, puis quitte avec **Ctrl+X** (ou simplement sauvegarde et ferme sur Windows).

### Tester la connexion :

Lance OpenCode dans un dossier quelconque :

```bash
cd ~
opencode
```

La première fois, OpenCode télécharge les paquets nécessaires (environ 1 minute).  
Tape `/models` pour voir tes modèles disponibles — tu devrais voir **MiniMax M2.7** et **GLM 4.7**. ✅

> 💡 Playwright MCP télécharge automatiquement un navigateur lors de sa première utilisation. Si tu obtiens une erreur liée au navigateur, exécute `npx playwright install chromium` dans ton terminal.

---

## 6. Créer ton compte GitHub et installer Git

**GitHub** est un service gratuit pour stocker ton code en ligne et le partager avec le monde.

### Créer un compte GitHub :

1. Va sur [https://github.com](https://github.com)
2. Clique sur **Sign up** et crée un compte gratuit

### Installer Git :

**Git** est l'outil qui permet de versionner ton code et de le publier sur GitHub.

**Sur macOS :**  
Dans le Terminal, tape `git --version`. Si Git n'est pas encore installé, macOS te proposera automatiquement de l'installer — clique sur **Installer** et suis les étapes.

**Sur Linux (Ubuntu/Debian) :**
```bash
sudo apt install git
```

**Sur Windows :**  
Télécharge et installe **Git for Windows** depuis [https://git-scm.com/download/win](https://git-scm.com/download/win). L'installateur est simple et guidé.

### Installer le GitHub CLI (gh) :

**gh** est l'outil officiel de GitHub en ligne de commande — il simplifie l'authentification et la création de dépôts.

Télécharge l'installateur pour ton système depuis [https://cli.github.com](https://cli.github.com) et suis les instructions.

### Configurer ton identité et se connecter :

Dans ton terminal, tape :

```bash
git config --global user.name "Ton Prénom"
git config --global user.email "ton@email.com"
gh auth login
```

Suis les étapes à l'écran pour t'authentifier avec ton compte GitHub.

---

## 7. Construire ton application web avec l'IA

Tu es maintenant prêt ! Voici comment créer une application web complète avec l'aide de l'IA.

### Créer ton dossier de projet :

```bash
mkdir mon-projet
cd mon-projet
opencode
```

### Choisir ton modèle :

Tape `/models` et sélectionne **MiniMax M2.7** ou **GLM 4.7**.

### Demander à l'IA de créer ton application :

Tu peux écrire des instructions en français directement à l'IA :

```
Crée une application web simple avec une page HTML qui affiche une liste de tâches à faire.
L'utilisateur doit pouvoir ajouter une tâche, la cocher comme terminée, et la supprimer.
Utilise du CSS moderne pour rendre l'interface jolie et responsive.
```

L'IA va créer tous les fichiers nécessaires et écrire le code complet.

### Tester avec Playwright :

Une fois l'application créée, demande à l'IA de la tester dans un navigateur :

```
Utilise Playwright pour ouvrir mon application dans un navigateur et vérifie que les
fonctionnalités principales fonctionnent correctement. Fais-moi un rapport de ce que tu as testé.
```

L'IA va ouvrir un navigateur, cliquer sur les éléments et te signaler tout problème. 🤖

### Publier sur GitHub :

Quand tu es satisfait du résultat, demande à l'IA de créer un dépôt GitHub et d'y publier ton code :

```
Crée un dépôt GitHub public pour ce projet, appelle-le "mon-projet-web", et pousse tout le code dessus.
```

L'IA utilisera `gh repo create` et `git push` pour tout faire automatiquement.

### Mettre ton site en ligne avec GitHub Pages :

Une fois le code sur GitHub, tu peux héberger ton application gratuitement :

1. Va sur ton dépôt GitHub (ex: `https://github.com/TON_NOM/mon-projet-web`)
2. Clique sur **Settings** → **Pages**
3. Dans **Source**, sélectionne la branche **main**
4. Ton site sera disponible à : `https://TON_NOM.github.io/mon-projet-web` 🎉

---

## 🎓 Et après ?

- Essaie de demander à l'IA de **modifier** quelque chose dans ton projet
- Demande-lui d'**expliquer** le code qu'elle a écrit
- Crée un deuxième projet : un jeu, une calculatrice, un portfolio...
- Explore d'autres modèles gratuits sur [build.nvidia.com](https://build.nvidia.com)

---

## ❓ Problèmes fréquents

**OpenCode ne trouve pas mon modèle :**  
→ Vérifie que ta clé API est correcte dans `~/.config/opencode/opencode.json`

**Playwright ne se lance pas :**  
→ Lance `npx playwright install chromium` dans le terminal puis réessaie

**Git me demande un mot de passe :**  
→ Lance `gh auth login` et suis les étapes

**`npm install -g opencode-ai` affiche une erreur de permission :**  
→ Sur macOS/Linux, ajoute `sudo` devant : `sudo npm install -g opencode-ai`

---

*Guide créé avec ❤️ pour aider les débutants à découvrir le développement assisté par IA.*
