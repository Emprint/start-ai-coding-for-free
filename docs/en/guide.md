# 🚀 Start AI Coding for Free

> **Who is this for?** Complete beginners — including kids — who want to build web apps with AI help, for free.

> 📅 **Guide created in May 2026.** The free models available on NVIDIA Build can change at any time: some may become paid, new ones may appear, or NVIDIA may modify or remove its free tier entirely. Always check what's available when you start a new project. The good news: OpenCode lets you switch models very easily, even in the middle of a session.

---

## Table of Contents

1. [What you need](#1-what-you-need)
2. [Create an NVIDIA account and get a free API key](#2-create-an-nvidia-account-and-get-a-free-api-key)
3. [Choose a free AI model on NVIDIA Build](#3-choose-a-free-ai-model-on-nvidia-build)
4. [Install Node.js and OpenCode](#4-install-nodejs-and-opencode)
5. [Configure OpenCode with NVIDIA](#5-configure-opencode-with-nvidia)
6. [Add Playwright MCP (AI that controls your browser)](#6-add-playwright-mcp-ai-that-controls-your-browser)
7. [Create your first GitHub project](#7-create-your-first-github-project)
8. [Start building your web app with AI](#8-start-building-your-web-app-with-ai)

---

## 1. What you need

- A computer running **macOS**, **Linux**, or **Windows** (native PowerShell — WSL not required)
- An internet connection
- About **30 minutes** to set everything up

No programming knowledge required — this is made for beginners!

---

## 2. Create an NVIDIA account and get a free API key

NVIDIA offers **free** access to powerful AI models through its **NVIDIA Build** platform.

> ⚠️ **Age requirement:** NVIDIA's Terms of Use require the account to be created by **an adult of legal age of majority** in their country (18 in most countries). If you are a minor, a **parent or guardian** must create the account and manage the API key on your behalf.

### Steps (must be done by an adult if you are a minor):

1. Go to [https://build.nvidia.com](https://build.nvidia.com)
2. Click **Sign In / Create Account** in the top-right corner
3. Create a free account with your email address
4. Once logged in, click your username top-right → **API Keys**
5. Click **Generate API Key**
6. Copy the key — it looks like: `nvapi-xxxxxxxxxxxxxxxxxxxx`

> ⚠️ **Important**: keep this key secret, never share it publicly.  
> The free tier includes **1,000 credits** renewed each month — more than enough to learn.

---

## 3. Choose a free AI model on NVIDIA Build

NVIDIA Build gives access to many AI models. Here's how to find a free one:

1. Go to [https://build.nvidia.com/models](https://build.nvidia.com/models)
2. Use the **Free Endpoint** filter to show only free models
3. Click on a model to see its card — note the **API endpoint ID** (e.g. `mistralai/mistral-7b-instruct-v0.3`)

### Recommended models for beginners:

| Model | Specialty | Highlights |
|---|---|---|
| `mistralai/mistral-7b-instruct-v0.3` | General | Fast, lightweight, great to start |
| `minimaxai/minimax-m2.7` | Coding | Very capable, 204K context |
| `z-ai/glm4.7` | Coding & reasoning | 358B parameters, very powerful |

> 💡 For web app development, **MiniMax M2.7** or **GLM 4.7** are excellent choices.

---

## 4. Install Node.js and OpenCode

**Node.js** is needed for OpenCode, Playwright MCP, and web development in general — so we install it first. We then install OpenCode through `npm`.

### On macOS:

Open the **Terminal** (⌘+Space, search "Terminal") and type:

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js
brew install node

# Install OpenCode
npm install -g opencode-ai
```

### On Linux (Ubuntu/Debian):

```bash
# Install Node.js and npm
sudo apt update && sudo apt install nodejs npm

# Install OpenCode
npm install -g opencode-ai
```

### On Windows (PowerShell — WSL not required):

Open **PowerShell** (Start menu → search "PowerShell") and choose one of these options:

**Option A — Via Chocolatey** (recommended package manager):
```powershell
# Install Chocolatey if not already installed (run PowerShell as Administrator)
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# Install Node.js
choco install nodejs

# Install OpenCode
npm install -g opencode-ai
```

**Option B — Via Scoop**:
```powershell
# Install Scoop if not already installed
iwr -useb get.scoop.sh | iex

# Install Node.js
scoop install nodejs

# Install OpenCode
npm install -g opencode-ai
```

**Option C — Direct download**:
1. Go to [https://nodejs.org](https://nodejs.org) and download the **LTS** version
2. Run the installer and follow the steps
3. Open a **new** PowerShell window, then:
```powershell
npm install -g opencode-ai
```

> 💡 **Windows tip**: Install [Windows Terminal](https://aka.ms/terminal) (free on the Microsoft Store) for a much better command-line experience.

### Verify the installation:

```bash
node --version      # e.g. v22.11.0 ✅
opencode --version  # e.g. 1.14.25 ✅
```

---

## 5. Configure OpenCode with NVIDIA

OpenCode needs to know how to connect to NVIDIA. We'll create a configuration file.

### Launch OpenCode once first:

Run OpenCode from any folder — it automatically creates its config folder on first start:

```bash
opencode
```

Press **q** to quit as soon as the interface appears. The `~/.config/opencode/` folder now exists.

### Open the config file:

```bash
# On macOS / Linux:
nano ~/.config/opencode/opencode.json

# On Windows (PowerShell):
notepad "$HOME\.config\opencode\opencode.json"
```

Paste this content (replace `YOUR_API_KEY` with your actual NVIDIA key):

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "nvidia-build": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "NVIDIA Build",
      "options": {
        "baseURL": "https://integrate.api.nvidia.com/v1",
        "apiKey": "YOUR_API_KEY"
      },
      "models": {
        "minimaxai/minimax-m2.7": {
          "name": "MiniMax M2.7 (free)",
          "tool_call": true,
          "limit": { "context": 204800, "output": 8192 }
        },
        "z-ai/glm4.7": {
          "name": "GLM 4.7 (free)",
          "tool_call": true,
          "limit": { "context": 131072, "output": 8192 }
        }
      }
    }
  }
}
```

Save with **Ctrl+O** then **Enter**, then exit with **Ctrl+X** (or just save and close on Windows).

### Test the connection:

Launch OpenCode in any folder:

```bash
cd ~
opencode
```

The first time, OpenCode downloads the required packages (about 1 minute).  
Type `/models` to see your available models — you should see **MiniMax M2.7** and **GLM 4.7**. ✅

---

## 6. Add Playwright MCP (AI that controls your browser)

**Playwright MCP** gives the AI the ability to open a web browser, click buttons, fill forms and take screenshots — just like a human would.

> Node.js is already installed from step 4 — no need to reinstall it.

### Add Playwright MCP to the OpenCode config:

Edit your `~/.config/opencode/opencode.json` to add the `mcp` section:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "nvidia-build": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "NVIDIA Build",
      "options": {
        "baseURL": "https://integrate.api.nvidia.com/v1",
        "apiKey": "YOUR_API_KEY"
      },
      "models": {
        "minimaxai/minimax-m2.7": {
          "name": "MiniMax M2.7 (free)",
          "tool_call": true,
          "limit": { "context": 204800, "output": 8192 }
        },
        "z-ai/glm4.7": {
          "name": "GLM 4.7 (free)",
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

### Install Playwright browsers:

```bash
npx playwright install chromium
```

> 💡 With Playwright MCP, you can ask the AI: *"Open my app in the browser and test if the button works"* — and it will do it automatically!

---

## 7. Create your first GitHub project

**GitHub** is a free service to store your code online and share it with the world.

### Create a GitHub account:

1. Go to [https://github.com](https://github.com)
2. Click **Sign up** and create a free account

### Create a new repository:

1. Once logged in, click the **+** top-right → **New repository**
2. Give your project a name (e.g. `my-first-web-app`)
3. Check **Add a README file**
4. Choose **Public** (so everyone can see it)
5. Click **Create repository**

### Install Git and clone your project:

```bash
# On macOS:
brew install git
brew install gh

# On Linux (Ubuntu/Debian):
sudo apt install git
sudo apt install gh  # or follow: https://cli.github.com

# On Windows (PowerShell):
choco install git
choco install gh
# or via Scoop:
scoop install git
scoop install gh
```

```bash
# Configure your Git identity (all platforms):
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Authenticate with GitHub:
gh auth login
```

### Clone your project to your computer:

```bash
cd ~/Documents
gh repo clone YOUR_USERNAME/my-first-web-app
cd my-first-web-app
```

---

## 8. Start building your web app with AI

You're ready! Here's how to work with the AI to create a web application.

### Launch OpenCode in your project:

```bash
cd ~/Documents/my-first-web-app
opencode
```

### Choose your model:

Type `/models` and select **MiniMax M2.7** or **GLM 4.7**.

### Example prompts to get started:

```
Create a simple web app with a HTML page that shows a to-do list.
The user should be able to add a task, check it as done, and delete it.
Use modern CSS to make the interface look nice and work on mobile.
```

```
Create a memory card game in HTML/CSS/JavaScript with 12 cards.
Cards should flip with a smooth animation.
Add an attempt counter and a timer.
```

The AI will:
1. Create all the necessary files
2. Write the complete code
3. Fix errors automatically

### Publish your project on GitHub:

```bash
git add .
git commit -m "My first project with AI"
git push
```

Your code is now online on GitHub! 🎉

### Share with friends:

Your project is visible at:  
`https://github.com/YOUR_USERNAME/my-first-web-app`

You can also enable **GitHub Pages** to host your app online for free:
1. Go to your repository settings → **Pages**
2. Select branch **main**
3. Your site will be live at: `https://YOUR_USERNAME.github.io/my-first-web-app`

---

## 🎓 What's next?

- Ask the AI to **modify** something in your project
- Ask it to **explain** the code it wrote
- Try a Playwright session: *"Open my app in the browser and tell me if everything works"*
- Explore more free models at [build.nvidia.com](https://build.nvidia.com)

---

## ❓ Common problems

**OpenCode can't find my model:**  
→ Check that your API key is correct in `~/.config/opencode/opencode.json`

**Playwright won't start:**  
→ Run `npx playwright install chromium` then try again

**Git asks for a password:**  
→ Run `gh auth login` and follow the steps

---

*Guide made with ❤️ to help beginners discover AI-assisted development.*
