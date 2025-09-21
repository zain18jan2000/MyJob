# PACS Project — Step-by-step Setup Guide (Windows → WSL2 → Docker)

**Purpose:** This README walks a non-technical user, step-by-step, to install and run the PACS project on a **Windows machine using WSL2 (Ubuntu)** and **Docker Desktop**. After following these steps you should be able to open the UI at **http://localhost:3010** (default).

---

## Quick-start checklist (one-liner)
1. Have **Windows** with admin rights.
2. Run `wsl --install` from an **Administrator PowerShell** (this installs WSL + Ubuntu).
3. Install **Docker Desktop for Windows** and enable WSL 2 integration.
4. Open **Ubuntu (WSL)**, clone the project, `cd` into it, then run `docker compose up -d --build`.
5. Open your browser to **http://localhost:3010**.

> The full, beginner-friendly steps are below (copy–paste friendly commands included).

---

## Before you begin — Requirements
- A Windows PC with **Administrator** rights (you will need them for installations).
- A reasonably modern Windows version (WSL 2 is available on Windows 10 and Windows 11).
- Internet connection (downloads for WSL, Docker images, etc.).
- If possible, a person with admin access to the machine to allow installs and reboots.

---

## Step 1 — Install WSL (Windows Subsystem for Linux) and Ubuntu
1. Open **Start → Windows Terminal** (or PowerShell). Right-click and **Run as administrator**.
2. Copy and paste this single command and press Enter:

```powershell
wsl --install
```

3. When the command finishes, **restart your computer** if prompted.
4. After restart, open **Ubuntu** from the Start menu. On first run it will ask you to create a **Linux username and password** — remember them.

Notes / alternatives:
- If your machine is older or `wsl --install` fails, see the manual WSL install instructions in your company guide or contact support.

---

## Step 2 — Install Docker Desktop and enable WSL integration
1. Download **Docker Desktop for Windows** from Docker's website (your IT or support can do this if you prefer).
2. Run the Docker Desktop installer. During install, allow it to use **WSL 2** if prompted (this is usually a checkbox in the installer).
3. After installation start **Docker Desktop** (from Start menu).
4. Open Docker Desktop settings (click the gear icon) → **Resources** → **WSL Integration**. Make sure the Ubuntu distribution is checked/enabled so Docker uses WSL.

---

## Step 3 — Open Ubuntu (WSL) and prepare tools
1. Open **Ubuntu** from the Start menu (this runs inside WSL).
2. Update packages and install `git` (if not already installed):

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git
```

3. (Optional) If you prefer a graphical editor you can open files in Windows Notepad directly from WSL using `notepad.exe filename`.

---

## Step 4 — Get the project files
**Option A — Using Git (recommended if you have a repo URL)**
1. In Ubuntu, navigate to where you want the project (example uses `~/projects`):

```bash
mkdir -p ~/projects
cd ~/projects
```

2. Clone the repository (replace the URL below):

```bash
git clone https://github.com/your-org/your-pacs-repo.git
cd your-pacs-repo
```

**Option B — Download ZIP from GitHub**
1. On Windows, open the project page on GitHub and click **Code → Download ZIP**. Extract it into a folder.
2. In Ubuntu, `cd /mnt/c/Users/<YourWindowsUser>/Downloads/your-pacs-repo` (or the folder you extracted to).

---

## Step 5 — Configure the project (.env and persistent folders)
1. Most projects include a sample environment file named `.env.example` or `.env.template`. Copy it to `.env`:

```bash
cp .env.example .env    # or cp .env.template .env
```

2. Edit `.env` to set any project-specific values. For a non-technical user, the typical things to check are:
   - Host/Port (UI port is usually `3010`) — leave as is if already set.
   - Any passwords or secret fields — your company should provide these.

Tips for editing if you aren’t comfortable with terminal editors:
- From WSL you can open the file in Windows Notepad by running: `notepad.exe .env`.
- Make edits, save, and close Notepad.

---

## Step 6 — Start the application (Docker Compose)
From inside the project directory (where `docker-compose.yml` or `docker-compose.yaml` or `compose` files live), run:

```bash
# Modern Docker: use 'docker compose' (no hyphen)
docker compose up -d --build

# If your environment uses the old compose binary instead, use:
# docker-compose up -d --build
```

What this does:
- Downloads any required Docker images (first run), builds local images, and starts the containers in the background.

---

## Step 7 — Verify the UI and services
1. Open a web browser on Windows and go to:

```
http://localhost:3010
```

2. If the UI appears, you’re done — congratulations! If not, proceed to the troubleshooting section below.

---

## Common troubleshooting (copy–paste commands to run)
**Check if Docker Desktop is running** (in Windows system tray) — Docker must be running.

**Check WSL distributions and versions** (run in Windows PowerShell or Ubuntu):
```powershell
wsl -l -v
```

**Check running containers**:
```bash
docker ps
# or for compose projects
docker compose ps
```

**Follow logs** (replace `<service>` with a service name from your compose file):
```bash
docker compose logs -f --tail=200 <service>
# or show all services
docker compose logs -f --tail=200
```

**Show logs for a single container**:
```bash
docker logs -f <container-name-or-id>
```

**Stop the project**:
```bash
docker compose down
```

**Restart the project**:
```bash
docker compose down && docker compose up -d --build
```

**Common hints**:
- If `docker` commands error: make sure Docker Desktop is running and WSL integration is enabled.
- If `wsl --install` failed: ensure you ran PowerShell as Administrator and rebooted when asked.
- If `git clone` fails: check internet or ask support for a ZIP file of the project.

---

## What to collect if you need help (copy these and send to support)
Run these commands and send the full output to your technical contact or support team:

```bash
# in Windows PowerShell (admin)
wsl -l -v

# in WSL or Ubuntu
docker version
docker compose version
docker compose ps
# and last 200 lines of logs
docker compose logs --tail=200
```

Also include a screenshot of the Docker Desktop status window and any error messages shown in the browser.

---

## Safe housekeeping & data
- If the project stores patient or medical data (PACS), **do not** share real patient data with outside parties. Follow your company's PHI/GDPR policies.
- Backups: if the project uses local volumes for data, your admin should set up scheduled backups of those folders.

---

## Stopping, removing and freeing space (if required)
To free disk space and remove stopped containers & unused images:
```bash
# stop the app
docker compose down

# remove dangling images and unused data (be careful)
docker system prune -a
```

> **Caution:** `docker system prune -a` removes unused images and can require re-downloading them later.

---

## Frequently asked — Quick answers
- **Q:** I don’t see the web UI at `localhost:3010`.
  - **A:** Check Docker Desktop is running, run `docker compose ps` and `docker compose logs -f` to find errors. If a container failed to start, copy the logs to support.

- **Q:** I’m afraid to run commands — can someone do this for me?
  - **A:** Yes — provide the support team remote access or send the machine to IT.

---

## Notes for the technical author (where to edit this README)
- Replace `https://github.com/your-org/your-pacs-repo.git` with the repository URL for your project.
- If the project uses a non-standard compose filename or extra steps (migrations, license files, secrets manager), add those exact commands under Step 5/6.
- Consider adding a separate `UPDATING.md` describing how to update the running instance safely (this file is intentionally setup-only).

---

## Support
If you get stuck, please send the requested command outputs above to **support@example.com** (replace with your support address) and include the time you tried the steps.

---

**End of setup guide.**

If you want, I can now:
- Customize this README with your repo URL and any special commands (DB migrations, license keys, or exact compose service names), or
- Create a separate `UPDATING.md` that explains how to apply project updates safely.

(If you want customization, paste the repo URL and any special instructions and I will update the README.)

