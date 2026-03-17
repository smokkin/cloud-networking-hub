# Azure Cloud Shell - Complete Guide

&gt; **Personal Learning Reference**  
&gt; A comprehensive guide to Azure Cloud Shell for managing Azure resources via browser-based command-line environment.

---

## Table of Contents
- [What is Azure Cloud Shell?](#what-is-azure-cloud-shell)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Access Methods](#access-methods)
- [Session Management](#session-management)
- [File Persistence & Storage](#file-persistence--storage)
- [Built-in Tools & Add-ons](#built-in-tools--add-ons)
- [Practical Use Cases](#practical-use-cases)
- [Quick Reference](#quick-reference)

---

## What is Azure Cloud Shell?

Azure Cloud Shell is a **browser-based command-line environment** for managing Azure resources including:
- Virtual Machines (VMs)
- Storage accounts
- Networking resources
- And all other Azure services

### Supported Shells
| Shell | Use Case |
|-------|----------|
| **Bash** | Linux/Unix administrators, shell scripting, open-source tools |
| **PowerShell** | Windows administrators, Azure PowerShell modules, automation scripts |

### Why Use Cloud Shell?
- ✅ **Always up-to-date** — Microsoft manages updates for Azure CLI and PowerShell modules
- ✅ **No local installation** — Works from any browser
- ✅ **Pre-authenticated** — Connected to your Azure account permissions automatically
- ✅ **Secure by default** — Double encryption at rest (no configuration needed)
- ✅ **Persistent storage** — CloudDrive retains files between sessions

---

## Key Features

| Feature | Description |
|---------|-------------|
| **Managed Infrastructure** | Microsoft handles maintenance and updates |
| **Dual Shell Support** | Switch between Bash and PowerShell |
| **CloudDrive Storage** | 5GB persistent storage for scripts, keys, and files |
| **Integrated Editor** | Built-in code editor for file modifications |
| **Azure File Share Mount** | Attach existing Azure File Shares |
| **Pre-installed Tools** | 30+ tools ready to use (Docker, Kubernetes, Terraform, etc.) |

---

## How It Works

### Real-World Scenario

> **Situation**: You're an IT admin for Contoso Corporation, on-call during a family visit.  
> **Problem**: A VM becomes unresponsive during maintenance; developers can't access underlying infrastructure.  
> **Solution with Cloud Shell**:
> 1. Open laptop → Browse to Azure Portal
> 2. Authenticate with organizational account
> 3. Launch Azure Cloud Shell
> 4. Mount Azure File Share containing diagnostic scripts
> 5. Diagnose and remediate VM issue
> 6. **Result**: VM restored without needing your administrative workstation

---

## Access Methods

### Method 1: Direct URL I'll create a GitHub-ready Markdown file that organizes this Azure Cloud Shell documentation with clear structure, formatting, and practical use cases for your reference.
Markdown
Copy
Code
Preview
# Azure Cloud Shell - Complete Guide

> **Personal Learning Reference**  
> A comprehensive guide to Azure Cloud Shell for managing Azure resources via browser-based command-line environment.

---

## Table of Contents
- [What is Azure Cloud Shell?](#what-is-azure-cloud-shell)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Access Methods](#access-methods)
- [Session Management](#session-management)
- [File Persistence & Storage](#file-persistence--storage)
- [Built-in Tools & Add-ons](#built-in-tools--add-ons)
- [Practical Use Cases](#practical-use-cases)
- [Quick Reference](#quick-reference)

---

## What is Azure Cloud Shell?

Azure Cloud Shell is a **browser-based command-line environment** for managing Azure resources including:
- Virtual Machines (VMs)
- Storage accounts
- Networking resources
- And all other Azure services

### Supported Shells
| Shell | Use Case |
|-------|----------|
| **Bash** | Linux/Unix administrators, shell scripting, open-source tools |
| **PowerShell** | Windows administrators, Azure PowerShell modules, automation scripts |

### Why Use Cloud Shell?
- ✅ **Always up-to-date** — Microsoft manages updates for Azure CLI and PowerShell modules
- ✅ **No local installation** — Works from any browser
- ✅ **Pre-authenticated** — Connected to your Azure account permissions automatically
- ✅ **Secure by default** — Double encryption at rest (no configuration needed)
- ✅ **Persistent storage** — CloudDrive retains files between sessions

---

## Key Features

| Feature | Description |
|---------|-------------|
| **Managed Infrastructure** | Microsoft handles maintenance and updates |
| **Dual Shell Support** | Switch between Bash and PowerShell |
| **CloudDrive Storage** | 5GB persistent storage for scripts, keys, and files |
| **Integrated Editor** | Built-in code editor for file modifications |
| **Azure File Share Mount** | Attach existing Azure File Shares |
| **Pre-installed Tools** | 30+ tools ready to use (Docker, Kubernetes, Terraform, etc.) |

---

## How It Works

### Architecture Overview
┌─────────────────┐
│   Web Browser   │
│  (Any Device)   │
└────────┬────────┘
│
▼
┌─────────────────┐
│  Azure Portal   │◄── Direct URL: https://shell.azure.com
│  or shell.azure │
└────────┬────────┘
│
▼
┌─────────────────┐
│ Temporary Host  │◄── Allocated per session (20 min timeout)
│   (Linux VM)    │
│  Bash/PowerShell│
└────────┬────────┘
│
┌────┴────┐
▼         ▼
┌────────┐ ┌──────────┐
│CloudDrive│ │Azure File│
│(5GB)   │ │  Share   │
│Persistent│ │(Optional)│
└────────┘ └──────────┘
plain
Copy

### Real-World Scenario

> **Situation**: You're an IT admin for Contoso Corporation, on-call during a family visit.  
> **Problem**: A VM becomes unresponsive during maintenance; developers can't access underlying infrastructure.  
> **Solution with Cloud Shell**:
> 1. Open laptop → Browse to Azure Portal
> 2. Authenticate with organizational account
> 3. Launch Azure Cloud Shell
> 4. Mount Azure File Share containing diagnostic scripts
> 5. Diagnose and remediate VM issue
> 6. **Result**: VM restored without needing your administrative workstation

---

## Access Methods

### Method 1: Direct URL https://shell.azure.com

<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/eab27c58-4893-4ee5-86d8-9e55c23e2a82" />

**Best for**: Quick access without navigating through portal menus

### Method 2: Azure Portal
- Click the Cloud Shell icon (`>_`) in the top navigation bar
- **Best for**: Integrated workflow with other Azure portal tasks

<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/b561bfdd-798f-48da-8107-d29c9f15fcbc" />

### First-Time Setup
When opening a new session:
1. Temporary VM is allocated (preconfigured with latest PowerShell & Bash)
2. Select your preferred shell experience
3. Optional: Mount Azure File Share for additional storage

<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/599ad201-f7c4-4dec-a095-3883b59a3cd1" />
<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/ee46b294-816c-44f0-92dd-033b142a9ff6" />

---

## Session Management

| Attribute | Specification |
|-----------|---------------|
| **Timeout** | 20 minutes of inactivity |
| **Persistence** | CloudDrive files survive session termination |
| **VM State** | Temporary host is recycled after timeout |
| **Reconnection** | New session = new VM (files remain on CloudDrive) |

> **Note**: Always save work to CloudDrive or Azure File Share. The temporary host VM is destroyed after timeout.

---

## File Persistence & Storage

### CloudDrive (Default)
- **Capacity**: 5GB
- **Persistence**: Survives session timeouts and device switches
- **Access**: Available across all sessions and devices

### Azure File Share (Optional)
- **Purpose**: Region-specific storage, team sharing, larger capacity
- **Setup**: Mount existing Azure File Share to Cloud Shell
- **Use case**: Shared scripts across team members

### File Management Commands

```bash
# List files in CloudDrive
ls ~/clouddrive

# Upload files (via Azure Portal drag-and-drop or Azure CLI)
az storage file upload --source localfile.sh --share-name myshare

# Mount Azure File Share (one-time setup)
clouddrive mount --s myshare --n mystorageaccount
