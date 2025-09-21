
# PACS Project — Step-by-step Setup Guide (Windows → WSL2 → Docker)

## Before you begin — Requirements
- A Windows PC with **Administrator** rights (you will need them for installations).
- Internet connection (downloads for WSL, Docker images, etc.).

---

## Step 1 — Install WSL (Windows Subsystem for Linux) and Ubuntu
1. Open **Start → Windows Terminal** (or PowerShell). Right-click and **Run as administrator**.
2. Copy and paste this single command and press Enter:

```cmd
wsl --install
```

3. When the command finishes, **restart your computer** if prompted.
4. After restart, open **Ubuntu** from the Start menu. On first run it will ask you to create a **Linux username and password** — remember them.

---

## Step 2 — Install Docker Desktop and enable WSL integration
1. Download **Docker Desktop for Windows** from Docker's website 
