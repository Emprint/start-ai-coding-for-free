# 🚀 Start AI Coding for Free

> **Who is this for?** Complete beginners — including kids — who want to build web apps with AI help, for free.

> 📅 **Guide created in May 2026.** The free models available on NVIDIA Build can change at any time: some may become paid, new ones may appear, or NVIDIA may modify or remove its free tier entirely. Always check what's available when you start a new project. The good news: OpenCode lets you switch models very easily, even in the middle of a session.

---

## Table of Contents

1. [What you need](#1-what-you-need)
2. [Create an NVIDIA account and get a free API key](#2-create-an-nvidia-account-and-get-a-free-api-key)
3. [Choose a free AI model on NVIDIA Build](#3-choose-a-free-ai-model-on-nvidia-build)
4. [Install Node.js and OpenCode](#4-install-nodejs-and-opencode)
5. [Configure OpenCode with NVIDIA and Playwright MCP](#5-configure-opencode-with-nvidia-and-playwright-mcp)
6. [Create your GitHub account and install Git](#6-create-your-github-account-and-install-git)
7. [Build your web app with AI](#7-build-your-web-app-with-ai)

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
2. Click the **Free Endpoint** filter
3. Click **Apply** to apply the filter — the list updates to show only free models
4. Click on a model to see its card — note the **API endpoint ID** (e.g. `mistralai/mistral-7b-instruct-v0.3`)

### Recommended models for beginners:

| Model | Specialty | Highlights |
|---|---|---|
| `minimaxai/minimax-m2.7` | Coding | Very capable, 204K context |
| `z-ai/glm4.7` | Coding & reasoning | 358B parameters, very powerful |

> 💡 For web app development, **MiniMax M2.7** or **GLM 4.7** are excellent choices.

---

## 4. Install Node.js and OpenCode

**Node.js** is a runtime environment needed for OpenCode and Playwright. We install it first, then install OpenCode through it.

> 💡 **What is the terminal?** It's a window where you type text commands to interact with your computer. On macOS, search "Terminal" in Spotlight (⌘+Space). On Windows, search "PowerShell" in the Start menu. On Linux, search "Terminal" in your applications.

### On macOS:

1. Go to [https://nodejs.org](https://nodejs.org) and download the **LTS** version
2. Run the `.pkg` installer and follow the steps
3. Once the installation is complete, open the **Terminal** (⌘+Space, search "Terminal") and type:

```bash
npm install -g opencode-ai
```

### On Linux (Ubuntu/Debian):

Open a **Terminal** and type:

```bash
sudo apt update && sudo apt install nodejs npm
npm install -g opencode-ai
```

### On Windows:

**Option A — Direct download (recommended for beginners):**
1. Go to [https://nodejs.org](https://nodejs.org) and download the **LTS** version
2. Run the `.msi` installer and follow the steps
3. Open **PowerShell** (Start menu → "PowerShell"), then type:

```powershell
npm install -g opencode-ai
```

**Option B — Via Chocolatey** (Windows package manager):
```powershell
# In PowerShell as Administrator:
choco install nodejs
npm install -g opencode-ai
```

**Option C — Via Scoop**:
```powershell
scoop install nodejs
npm install -g opencode-ai
```

> 💡 **Windows tip**: Install [Windows Terminal](https://aka.ms/terminal) (free on the Microsoft Store) for a much better command-line experience.

### Verify the installation:

In your terminal, type the following commands to confirm everything is installed:

```bash
node --version      # should display something like v22.11.0
opencode --version  # should display something like 1.14.25
```

If both commands display a version number, you're all set! ✅

---

## 5. Configure OpenCode with NVIDIA and Playwright MCP

OpenCode needs to know how to connect to NVIDIA. We'll create a configuration file that also includes **Playwright MCP** — the tool that allows the AI to control a web browser.

### Launch OpenCode once first:

OpenCode automatically creates its config folder on first startup. Run it from any folder:

```bash
opencode
```

Press **q** to quit as soon as the interface appears. The config folder has been created.

### Open the config file:

In your terminal, open the configuration file:

```bash
# On macOS / Linux:
nano ~/.config/opencode/opencode.json

# On Windows (PowerShell):
notepad "$HOME\.config\opencode\opencode.json"
```

### Paste the full configuration:

Replace all the file content with the following (replace `YOUR_API_KEY` with your actual NVIDIA key):

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

Save with **Ctrl+O** then **Enter**, then exit with **Ctrl+X** (or just save and close on Windows).

### Test the connection:

Launch OpenCode in any folder:

```bash
cd ~
opencode
```

The first time, OpenCode downloads the required packages (about 1 minute).  
Type `/models` to see your available models — you should see **MiniMax M2.7** and **GLM 4.7**. ✅

> 💡 Playwright MCP automatically downloads a browser on its first use. If you get a browser-related error, run `npx playwright install chromium` in your terminal.

---

## 6. Create your GitHub account and install Git

**GitHub** is a free service to store your code online and share it with the world.

### Create a GitHub account:

1. Go to [https://github.com](https://github.com)
2. Click **Sign up** and create a free account

### Install Git:

**Git** is the tool that versions your code and lets you publish it to GitHub.

**On macOS:**  
In the Terminal, type `git --version`. If Git is not yet installed, macOS will automatically offer to install it — click **Install** and follow the steps.

**On Linux (Ubuntu/Debian):**
```bash
sudo apt install git
```

**On Windows:**  
Download and install **Git for Windows** from [https://git-scm.com/download/win](https://git-scm.com/download/win). The installer is simple and guided.

### Install the GitHub CLI (gh):

**gh** is GitHub's official command-line tool — it simplifies authentication and repository creation.

Download the installer for your system from [https://cli.github.com](https://cli.github.com) and follow the instructions.

### Configure your identity and log in:

In your terminal, type:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
gh auth login
```

Follow the on-screen steps to authenticate with your GitHub account.

---

## 7. Build your web app with AI

You're ready! Here's how to create a complete web application with AI assistance.

### Create your project folder:

```bash
mkdir my-project
cd my-project
opencode
```

- `mkdir my-project` — creates a new folder called `my-project`
- `cd my-project` — moves into that folder (cd = *change directory*)
- `opencode` — launches the OpenCode tool inside that folder

### Choose your model:

Type `/models` and select **MiniMax M2.7** or **GLM 4.7**.

### Ask the AI to build your app:

You can write instructions directly to the AI in plain language:

```
Create a simple web app with an HTML page that shows a to-do list.
The user should be able to add a task, check it as done, and delete it.
Use modern CSS to make the interface look nice and work on mobile.
```

The AI will create all the necessary files and write the complete code.

### Test with Playwright:

Once the app is created, ask the AI to test it in a real browser:

```
Use Playwright to open my application in a browser and check that the main
features work correctly. Give me a report of what you tested.
```

The AI will open a browser, interact with your app and report any issues. 🤖

### Publish to GitHub:

When you're happy with the result, ask the AI to create a GitHub repository and push your code:

```
Create a public GitHub repository for this project, call it "my-web-project",
and push all the code to it.
```

The AI will use `gh repo create` and `git push` to handle everything automatically.

### Go live with GitHub Pages:

Once your code is on GitHub, you can host your app online for free:

1. Go to your GitHub repository (e.g. `https://github.com/YOUR_USERNAME/my-web-project`)
2. Click **Settings** → **Pages**
3. Under **Source**, select branch **main**
4. Your site will be live at: `https://YOUR_USERNAME.github.io/my-web-project` 🎉

---

## 🎓 What's next?

- Ask the AI to **modify** something in your project
- Ask it to **explain** the code it wrote
- Build a second project: a game, a calculator, a portfolio...
- Explore more free models at [build.nvidia.com](https://build.nvidia.com)

---

## ❓ Common problems

**OpenCode can't find my model:**  
→ Check that your API key is correct in `~/.config/opencode/opencode.json`

**Playwright won't start:**  
→ Run `npx playwright install chromium` in your terminal then try again

**Git asks for a password:**  
→ Run `gh auth login` and follow the steps

**`npm install -g opencode-ai` shows a permission error:**  
→ On macOS/Linux, add `sudo`: `sudo npm install -g opencode-ai`

---

*Guide made with ❤️ to help beginners discover AI-assisted development.*
