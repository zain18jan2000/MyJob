
# Step-by-step Setup Guide (Windows → WSL2 → Docker)

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
1. Download **Docker Desktop For Windows-x64_86** from [Docker's website](https://docs.docker.com/desktop/setup/install/windows-install/)
2. Run the Docker Desktop installer. During install, allow it to use **WSL 2** if prompted (this is usually a checkbox in the installer).
3. After installation start **Docker Desktop** (from Start menu).
4. Open Docker Desktop settings (click the gear icon) → **Resources** → **WSL Integration**. Make sure the Ubuntu distribution is checked/enabled so Docker uses WSL.

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/WSL%20Integragion.PNG" alt="Centered Image" width="70vh"/>
</p>

---

## Step 3 — Open Ubuntu (WSL) and prepare tools
1. Open **Ubuntu** from the Start menu (this runs inside WSL).
2. Update packages and install `git` using the following command,

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y git
```

## Step 4 --
1. Navigate to home directory using following command. Replace <username> with your username

```bash
cd /home/<username>
```

2. Download Project ZIP file and extract it into a folder.
3. Assuming your project folder is at c/Users/<YourWindowsUser>/Downloads/FASTapi-PACS. Where <YourWindowsUser> is the system username. Move the folder to wsl home directory using following command.

```bash
mv /mnt/c/Users/<YourWindowsUsername>/Downloads/FASTapi-PACS ./
```
4. Now move to project folder using follwing command,

```bash
cd FASTapi-PACS
```

