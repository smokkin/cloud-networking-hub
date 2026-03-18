# Azure Cloud Shell - Complete Guide

&gt; **TL;DR:** Azure Cloud Shell is a browser-based shell environment for managing Azure resources without installing local tools. It comes pre-configured with PowerShell, Bash, Azure CLI, and 20+ tools, with persistent storage via CloudDrive.

---

## Table of Contents

- [What is Azure Cloud Shell?](#what-is-azure-cloud-shell)
- [Real-World Use Case: Emergency VM Recovery](#real-world-use-case-emergency-vm-recovery)
- [How to Access Cloud Shell](#how-to-access-cloud-shell)
- [Understanding Your Shell Environment](#understanding-your-shell-environment)
- [Working with Files & Scripts](#working-with-files--scripts)
- [Available Tools & Add-ons](#available-tools--add-ons)
- [Key Limitations & Tips](#key-limitations--tips)

---

## What is Azure Cloud Shell?

Azure Cloud Shell provides a **temporary, browser-based virtual machine** pre-loaded with administrative tools. It allows you to:

- Manage Azure resources from any device with a browser
- Access both **PowerShell** and **Bash** environments
- Store scripts/files persistently using CloudDrive
- Work without installing Azure CLI or PowerShell locally

**Session Details:**
- **Allocation:** New temporary VM per session
- **Timeout:** Auto-terminates after **20 minutes of inactivity**
- **Persistence:** Files in `CloudDrive` survive between sessions

---

## Real-World Use Case: Emergency VM Recovery

### Scenario
You're an IT admin on-call during a weekend family visit. The dev team reports a **non-responsive Azure VM** after application maintenance. They can't access the underlying infrastructure, so you must intervene—but you only have a laptop without your admin workstation or diagnostic tools.

### Step-by-Step Resolution

| Step | Action | Details |
|------|--------|---------|
| 1 | **Connect** | Open browser → Navigate to Azure Portal |
| 2 | **Authenticate** | Sign in with organizational Azure AD credentials |
| 3 | **Launch Shell** | Open Azure Cloud Shell from the portal |
| 4 | **Mount Storage** | Attach your Azure File Share (contains diagnostic scripts) |
| 5 | **Execute Scripts** | Run diagnostic tools from the mounted share |
| 6 | **Remediate** | Identify and fix the VM issue |
| 7 | **Verify** | Confirm VM is responsive and dev team can reconnect |

**Result:** Crisis resolved in minutes using only a browser—no local tooling required.

---

## How to Access Cloud Shell

Choose the method that fits your workflow:

### Method 1: Direct URL (Fastest)
https://shell.azure.com

Best for: Quick access without navigating the portal

### Method 2: Azure Portal
1. Sign in to [portal.azure.com](https://portal.azure.com)
2. Click the **Cloud Shell icon** (terminal symbol) in the top toolbar
3. Select your preferred shell experience (see below)

### Method 3: Microsoft Learn
- Click **"Try It"** buttons in code snippets during tutorials
- Automatically opens Cloud Shell with context-aware commands

---

## Understanding Your Shell Environment

### First-Time Setup
When you open Cloud Shell for the first time:

```bash
# You'll be prompted to choose:
# [1] Bash
# [2] PowerShell

Switching Later: Use the shell selector dropdown in the Cloud Shell window
Session Lifecycle
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Session Start  │────▶│  Active Usage   │────▶│  20min Inactive │
│  (New VM Alloc) │     │  (Files persist)│     │  (Auto-terminate)│
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │                                               │
         └───────────────────────────────────────────────┘
                    (Start new session to resume)

Working with Files & Scripts

CloudDrive: Your Persistent Storage

Location: ~/clouddrive or $HOME/clouddrive

What persists:
✅ Files uploaded to CloudDrive
✅ Scripts and configuration files
✅ SSH keys and credentials (stored securely)

What doesn't persist:
❌ Files outside CloudDrive (e.g., /tmp, $HOME non-clouddrive)
❌ Installed software (session-bound)
❌ Running processes

Managing Files

# View CloudDrive contents
ls ~/clouddrive

# Upload files (drag & drop in browser, or use Azure portal upload)

# Create/edit files
touch ~/clouddrive/myscript.sh

# Access from any device later
# Simply open Cloud Shell on new device → files are there

Azure File Share Integration

For team collaboration or larger storage:
# Mount an existing Azure File Share
# (Configure via Cloud Shell settings in Azure Portal)

# Access via mounted path
ls /mnt/myfileshare

Editing Files

Option 1: Cloud Shell Editor (GUI)
Click the curly braces {} icon in the toolbar
Navigate to file or click "Open File"

Option 2: Terminal Editor
# Using built-in editors
code temp.txt      # Cloud Shell editor (Classic mode only)
vim config.yml     # Vim
nano script.sh     # Nano
emacs notes.txt    # Emacs

&gt; **⚠️ Note:** The `code` command requires **Classic mode**.
&gt; Enable via: `...` (More) → Settings → Go to Classic version

---

## Available Tools & Add-ons

Cloud Shell comes pre-installed with 30+ tools across categories:

### Azure Management

| Tool | Purpose | Example Use |
|------|---------|-------------|
| `az` (Azure CLI) | Primary Azure management | `az vm list` |
| `azcopy` | Bulk data transfer | `azcopy copy ./data https://[account].blob.core.windows.net/[container]` |
| `func` | Azure Functions CLI | `func init MyFunctionProj` |
| `sfctl` | Service Fabric management | `sfctl cluster select` |

### Containers & Orchestration

| Tool | Purpose | Quick Command |
|------|---------|---------------|
| `docker` | Container management | `docker ps` |
| `kubectl` | Kubernetes control | `kubectl get nodes` |
| `helm` | Kubernetes package manager | `helm install mychart ./chart` |
| `dcos` | DC/OS cluster management | `dcos node list` |

### Infrastructure as Code

| Tool | Purpose | Example |
|------|---------|---------|
| `terraform` | Multi-cloud IaC | `terraform plan` |
| `ansible` | Configuration management | `ansible-playbook site.yml` |
| `packer` | Image building | `packer build template.json` |
| `chef` | Compliance & automation | `chef-client` |

### Databases

| Tool | Database | Connection Example |
|------|----------|-------------------|
| `mysql` | MySQL | `mysql -h [server].mysql.database.azure.com -u admin` |
| `psql` | PostgreSQL | `psql -h [server].postgres.database.azure.com` |
| `sqlcmd` | SQL Server | `sqlcmd -S [server].database.windows.net` |

### Development & Build

| Tool | Category | Usage |
|------|----------|-------|
| `git` | Source control | `git clone https://...` |
| `npm` | Node.js packages | `npm install` |
| `maven` | Java builds | `mvn clean install` |
| `pip` | Python packages | `pip install requests` |
| `make` | Build automation | `make build` |

### Linux Utilities

- `bash`, `zsh`, `sh` - Shell environments
- `tmux` - Terminal multiplexer
- `dig` - DNS lookup utility

### Other Tools

| Tool | Use Case |
|------|----------|
| `ipython` | Interactive Python |
| `cf` (Cloud Foundry) | PaaS application deployment |
| `o365` | Office 365 management |

---

## Key Limitations & Tips

### ⚠️ Important Constraints

| Limitation | Workaround |
|------------|------------|
| **20-minute timeout** | Keep session active; save work to CloudDrive frequently |
| **No sudo/root access** | Use containerized alternatives or Azure Container Instances |
| **Session-bound installs** | Add installation steps to startup scripts in CloudDrive |
| **No persistent background processes** | Use Azure Automation or Logic Apps for long-running tasks |

### 💡 Pro Tips

1. **Always save to CloudDrive**

   ```bash
   # Good practice
   cp important-script.sh ~/clouddrive/
   
   # Bad practice (will be lost)
   cp important-script.sh /tmp/

2. **Use Azure File Shares for team scripts**
   - Mount shared storage for scripts used across your team
   - Ensures consistency and version control integration

3. **Leverage the editor for complex edits**
   - The GUI editor (`{}` icon) is easier than vim/nano for multi-file edits

4. **Combine with Azure Portal**
   - Use Cloud Shell alongside the Portal's resource explorer for visual + CLI workflow

---

# Essential commands to bookmark

# Azure CLI basics
az login                    # Already logged in via Portal
az account show             # Verify subscription
az resource list            # List all resources
az vm list                  # List VMs
az vm start -g [rg] -n [vm] # Start a VM

# CloudDrive operations
cd ~/clouddrive             # Navigate to persistent storage
ls -la                      # List files
mkdir scripts               # Create directory
code script.ps1             # Edit in GUI editor (Classic mode)

# File upload/download
# Use Azure Portal drag-and-drop or:
az storage file upload --share-name [share] --source [localfile]

---

## Summary

Azure Cloud Shell transforms any browser into a fully-equipped Azure administration workstation. Whether you're responding to a 3 AM production incident from a hotel tablet or running routine maintenance from your phone, Cloud Shell provides consistent, secure access to your Azure environment without local tooling dependencies.

&gt; **Key Takeaway:** Your Azure management console is now as portable as your Azure subscription—accessible from any device, anywhere, with your scripts and tools always available via CloudDrive.

---

**Last Updated:** 2026-03-18  
**Azure Service:** Cloud Shell  
**Documentation:** [Microsoft Learn - Azure Cloud Shell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview)
