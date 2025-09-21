
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
4. Open Docker Desktop settings (click the gear icon) → **Resources** → **WSL Integration**. Make sure the Ubuntu distribution is checked/enabled so Docker uses WSL (See the image).

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/WSL%20Integragion.PNG" alt="Centered Image" width="750"/>
</p>

---

## Step 3 — Open Ubuntu (WSL) and prepare tools
1. Open **Ubuntu** from the Start menu or run the following command on cmd.

```bash
wsl
```

3. Once ubuntu is started inside wsl, update packages using the following command,

```bash
sudo apt update && sudo apt upgrade -y
```

4. Navigate to home directory using following command. Make sure to replace <username> with your **Linux username**.

```bash
cd /home/<username>
```

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/wsl_home_directory.PNG" alt="Centered Image" width="850"/>
</p>



## Step 4 — Download ZIP file and Configure the project (.env)
1. Download the project zip file and extract it.
3. Inside project folder and rename **.env.example** file to **.env**

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/rename%20.env.PNG" alt="Centered Image" width="850"/>
</p>

4. Now open the file on notepad. Here we need to add the **USER_UID**, **USER_GID** **PROJECT_ROOT** and **LOG_PATH**. In order to get **USER_UID**, **USER_GID** go back to ubuntu terminal and enter following command,

```bash
id
```

Note the the **uid** and **gid** values.

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/UID_GID.PNG" alt="Centered Image" width="850"/>
</p>

To get the user use the following command,

```bash
whoami
```

**PROJECT_ROOT** and **LOG_PATH** will be as given below, make sure to replace <username> with your linux username.

PROJECT_ROOT=/home/<username>/FASTapi-PACS-main
LOG_PATH=/home/<username>/FASTapi-PACS-main/logs

Now enter these values in .env file as shown in image,

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/update_env.PNG" alt="Centered Image" width="850"/>
</p>

5. Save the **.env** and close the notepad.

---


## Step 5 — Configure the project

3. Assuming your project folder is at c/Users/<YourWindowsUser>/Downloads/FASTapi-PACS-main/FASTapi-PACS-main. Where <YourWindowsUser> is the system username. Move the folder to wsl home directory using following command.

```bash
mv /mnt/c/Users/<YourWindowsUsername>/Downloads/FASTapi-PACS-main/FASTapi-PACS-main ./
```

4. Now move to project folder using following command,

```bash
cd FASTapi-PACS-main
```
 Now you should be inside your project folder just like shown in image.

<p align="center">
  <img src="https://github.com/zain18jan2000/MyJob/blob/main/move_project.PNG" alt="Centered Image" width="850"/>
</p>
 
---


## Step 6 — Build Docker images and start application

1. Make sure the docker window is active and then copy and paste the following command to setup monitoring services,

```bash
docker compose -f compose.yaml -f monitoring.yaml up --build -d
```

This will take sometimes. 

2. Once all containers are started, Confirm if the containers are running on docker desktop.

<p align="center">
  <img src="https://drive.google.com/file/d/13-MDWlJO5cjK9j93YkVNFuy05eHSUjIO/view?usp=sharing" alt="Centered Image" width="850"/>
</p>

3. Now open a web browser on Windows and go to:

```
http://localhost:3010
```

4. Register and login.


