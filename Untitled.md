- Requirements for 24/7 operation.
- Step-by-step WSL 1 installation guide with official links.
- Instructions for installing compatible versions of Chrome and ChromeDriver in WSL 1.
- Guidance on using a virtual environment for Python 3.13.1 for better consistency.
- Clear setup for Telegram bot token, admin/user token, and launching the bot in the background.

I’ll let you know when it’s ready.

# Telegram-WhatsApp Bot Setup and Usage Guide

## 1. VPS and 24/7 Operation
This bot is designed to run continuously on a **Windows VPS**. To ensure uninterrupted service:
- **Keep the VPS running 24/7:** The bot should be hosted on a server that is always online. If the VPS is shut down or restarted, the bot will stop.
- **Start once and run in background:** You only need to launch the bot one time. It will run in the background listening for Telegram commands and automating WhatsApp. After starting it, you can close your SSH or RDP session; the bot will continue running (see Section 6 on how to do this).
- **Do not log off or shut down the VPS:** Logging off your remote session is fine (if the bot is running as a background process), but shutting down or rebooting the VPS will interrupt the bot. Plan for updates/reboots accordingly.

## 2. Installing WSL 1 on Windows 10/11
The bot runs in a Linux environment provided by **Windows Subsystem for Linux (WSL)**. We specifically need **WSL version 1** (not WSL 2). Follow these steps to install WSL1:

1. **Enable WSL feature:** On your Windows 10/11 VPS, open PowerShell **as Administrator** and run:  
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```  
   This command enables the WSL feature on Windows ([Manual installation steps for older versions of WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install-manual#:~:text=We%20recommend%20now%20moving%20on,on%20to%20the%20next%20step)). If you prefer using the GUI, you can also go to *Control Panel > Programs > Turn Windows features on or off*, and check **Windows Subsystem for Linux**, then click OK.


1. **(Optional) Set WSL default version to 1:** By default, newer Windows might use WSL2. To ensure new Linux installations use WSL1, run in PowerShell:  
   ```powershell 
   wsl --set-default-version 1
   ```  
   This forces WSL to use version 1 for new Linux distros ([Basic commands for WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#:~:text=wsl%20)).

2. **Reboot Windows:** After enabling WSL, restart your VPS to apply changes.

3. **Install a Linux distribution:** For example, install **Ubuntu** from the Microsoft Store or via command line:  
   - **Via Microsoft Store:** Open the Store, search for "Ubuntu" (e.g., Ubuntu 22.04 LTS) and click **Install**.  
   - **Via PowerShell:** Run `wsl --install -d Ubuntu` (this will install the default Ubuntu distribution).  
   The first time you launch Ubuntu, it will prompt you to create a UNIX username and password – go ahead and create those.

5. **Verify and set WSL version:** After installation, check that the distro is using WSL1. In PowerShell, run:  
   ```powershell
   wsl -l -v
   ```  
   This lists all installed distros with their WSL version. Ensure your Ubuntu (or chosen distro) shows **Version 1**. If it shows Version 2, convert it to 1 by running:  
   ```powershell
   wsl --set-version <DistroName> 1
   ```  
   (Replace `<DistroName>` with the exact name shown in the `wsl -l -v` list, e.g., "Ubuntu-22.04"). This command will switch that distro to WSL1.

👉 **Official Documentation:** For more details, refer to Microsoft's guide on installing WS ([Manual installation steps for older versions of WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install-manual#:~:text=We%20recommend%20now%20moving%20on,on%20to%20the%20next%20step))】. Ensure to follow the steps for WSL1 (the guide notes that if you want only WSL1, you can skip the WSL2 update steps).

## 3. Installing Google Chrome and ChromeDriver version 131.0.6778.204 in WSL 1
Our bot uses **Selenium** with Google Chrome to automate WhatsApp Web. We need to install **Google Chrome (Linux version)** inside WSL and the matching **ChromeDriver**. It’s crucial that the ChromeDriver version matches the Chrome browser version.

### 3.1 Install Google Chrome (Linux) in WSL
1. **Update package list:** Open your WSL terminal (Ubuntu) and run:  
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```  
   This updates your packages to avoid issues.

2. **Install dependencies (if not already installed):** Ensure you have `wget` and `apt-transport-https`:  
   ```bash
   sudo apt install -y wget software-properties-common apt-transport-https
   ```

3. **Download Google Chrome 131.0.6778.204 .deb package:**  
   > You need a `.deb` installer for **Chrome 131.0.6778.204** specifically. This version might come from an official Google repo, a pinned repository, or an archived link. For example (hypothetical link—replace with the actual source if you have it):
   ```bash
   cd /tmp
   wget https://dl.google.com/linux/direct/google-chrome-stable_131.0.6778.204_amd64.deb
   ```
   This will download the Chrome 131.0.6778.204 installer to the `/tmp` directory.  

4. **Install the Chrome .deb package:**  
   ```bash
   sudo apt install -y ./google-chrome-stable_131.0.6778.204_amd64.deb
   ```  
   Using apt to install the local deb will automatically install any needed dependencies.

5. **Verify Chrome is installed:** Run:
   ```bash
   google-chrome --version
   ```
   You should see something like `Google Chrome 131.0.6778.204`. This confirms Chrome 131.0.6778.204 is installed in WSL. (We will use Chrome in headless mode via Selenium, so we don’t need a display.)

### 3.2 Install ChromeDriver (for Selenium) Version 131.0.6778.204
Now install **ChromeDriver 131.0.6778.204**, which allows Selenium to control Chrome:
1. **Check Chrome version:** Ensure it’s exactly `131.0.6778.204`.
2. **Download the matching ChromeDriver 131.0.6778.204:** Visit the official ChromeDriver download page: **<https://chromedriver.chromium.org/downloads>**. Find the version that matches **131.0.6778.204**. Download the **Linux 64-bit** ChromeDriver zip. Alternatively, from command line:
   ```bash
   wget -O /tmp/chromedriver.zip https://chromedriver.storage.googleapis.com/131.0.6778.204/chromedriver_linux64.zip
   ```
3. **Unzip the driver:**
   ```bash
   sudo apt install -y unzip  # install unzip if not already present
   unzip /tmp/chromedriver.zip -d /tmp
   ```
   This extracts a file named `chromedriver`.
4. **Install ChromeDriver system-wide:**
   ```bash
   sudo mv /tmp/chromedriver /usr/local/bin/chromedriver
   sudo chmod +x /usr/local/bin/chromedriver
   ```
   We move the driver to `/usr/local/bin` and make it executable. This places it in your PATH.
5. **Verify ChromeDriver:**
   ```bash
   chromedriver --version
   ```
   You should see `ChromeDriver 131.0.6778.204`. If the versions don’t match (or if you get an error), download the correct version and replace the binary.

**⚠ Important:** ChromeDriver’s version **must match** the installed Chrome’s version. If you update Chrome in the future, update ChromeDriver accordingly. A mismatch will cause Selenium to throw errors (e.g., `SessionNotCreatedException`).

## 4. Installing Python 3.13.1 and Setting Up the Environment
The bot is written in Python, specifically requiring **Python 3.13.1**. We will install this version in WSL and set up a Python virtual environment for the bot.

### 4.1 Install Python 3.13.1 in WSL (Ubuntu)
Ubuntu’s default Python may be older, so we’ll install Python 3.13.1 manually:
1. **Add deadsnakes PPA:** This repository provides newer Python versions on Ubuntu. In WSL Ubuntu, run:  
   ```bash
   sudo add-apt-repository ppa:deadsnakes/ppa -y
   sudo apt update
   ```  
   (If `add-apt-repository` is not found, install `software-properties-common` as done in Section 3.)

2. **Install Python 3.13:**  
   ```bash
   sudo apt install -y python3.13-full
   ```  
   This installs Python 3.13 and all standard libraries. If you prefer a minimal install, you can do `python3.13` instead of `python3.13-full`, but the "full" package ensures you have pip, venv, etc., available.

3. **Verify the installation:** Run `python3.13 --version`. It should output `Python 3.13.1`. Keep the default Python (3.x) as is; we will call `python3.13` explicitly for the bot.

4. **Install pip for Python 3.13:** Ubuntu’s package might not automatically include pip for this version. Set it up by running:  
   ```bash
   python3.13 -m ensurepip --upgrade 
   python3.13 -m pip install --upgrade pip
   ```  
   The first command bootstraps pip, and the second upgrades pip to the latest version.

### 4.2 Create a Python Virtual Environment (Recommended)
It’s best practice to run the bot in an isolated virtual environment to manage dependencies:
1. **Install venv module (if needed):** If `python3.13-full` was installed, the venv module should be included. If not, install it:  
   ```bash
   sudo apt install -y python3.13-venv
   ```

2. **Create a virtual environment:** Navigate to the directory where your bot code is (the folder containing `bot.py`). Then run:  
   ```bash
   python3.13 -m venv bot-env
   ```  
   This creates a virtual environment named `bot-env` in that directory.

3. **Activate the virtual environment:**  
   ```bash
   source bot-env/bin/activate
   ```  
   After this, your shell prompt will change (often it will prefix with `(bot-env)`), indicating the venv is active. Now `python` and `pip` will refer to the versions inside this environment (which uses Python 3.13).

4. **Install the bot’s dependencies:** Use pip to install required Python packages. Typically, the bot’s code repository may include a `requirements.txt`. If provided, use:  
   ```bash
   pip install -r requirements.txt
   ```  
   If no requirements file is present, install packages individually:  
   - **Selenium:** `pip install selenium`  
   - **Telegram bot API library:** The code uses the Python Telegram Bot library. Install it with: `pip install python-telegram-bot` (for latest version).  
   - (Any other libraries required by the bot should be installed here as well.)

   **Example `requirements.txt`:** You can create a requirements file for consistency. For instance:  
   ```text
   selenium==4.10.0
   python-telegram-bot==20.3
   ```  
   Adjust versions as needed. Then run `pip install -r requirements.txt` to install all at once.

5. **Stay in the virtual environment:** Remember to activate this `bot-env` whenever you work with or run the bot. You can add a note to yourself in the README to run `source bot-env/bin/activate` before starting the bot. (If you forget, the bot might run with the wrong Python or miss dependencies.)

## 5. Bot Configuration (Telegram Token and Authorization Setup)
Before running the bot, you need to configure a few things in the code:

### 5.1 Telegram Bot Token
- **Tokens that must stay the same:** 

  ```python
  BOT_TOKEN = "123456:ABCDEF...BotFather token provided by Telegram..."
  ```  

### 5.2 Admin and User Authorization Tokens
The bot has an **authorization system** to restrict access to certain commands:
- Open the file `authorization.py`. You will see two variables `ADMIN_TOKEN` and `USER_TOKEN` near the top, defaulting to `"1"` and `"2"` respectively.
- **Set a secret admin token:** Change `ADMIN_TOKEN = "1"` to a secure string that will serve as the "password" for admin access. For example:  
  ```python
  ADMIN_TOKEN = "MySecretAdminPass123"
  ```  
  Choose something not easily guessable. This is what you (and any trusted admins) will use to authorize yourselves as admin via Telegram.
- **Set a user token:** Similarly, change `USER_TOKEN = "2"` to another secret string for regular users. For example:  
  ```python
  USER_TOKEN = "GuestAccess456"
  ```  
  This token can be a simpler or different code that you give out to users who should have limited access to the bot (send messages only).

**Do not share these tokens publicly.** Only give them to those who should have access. Anyone who knows the tokens can potentially authorize themselves with your bot.

### 5.3 Admin vs User Roles
Understanding the difference:
- **Admin Role:** After a user sends the admin token via the `/authorize` command, they become an authorized admin. Admins have **full access** to all bot commands. This includes management commands like linking WhatsApp, adding/removing groups, approving groups, and sending messages. Essentially, admins can configure the bot and broadcast messages.
- **User Role:** After a user sends the user token with `/authorize`, they become an authorized regular user. Regular users have **limited access**. They can send broadcast messages (to allowed groups) but cannot perform management actions. For example, a user can use the `/send` or `/sendall` commands to send messages, but cannot approve new groups or link WhatsApp or manage groups.
- **Usage scenario:** You (the owner) would use the admin token on your Telegram account (making you an admin in the bot). You might give the user token to, say, some team members or friends who should be able to send out announcements via the bot, but not change settings. This way, even if the user token is shared, those users can only use the bot in a send-only capacity.

You can always change these tokens in `authorization.py` if needed (just be sure to restart the bot for changes to take effect). Changing them will not unauthorize people who already used the old tokens during that run, but on a fresh start of the bot, only those with the new tokens will be able to authorize.

## 6. Running the Bot in the Background (Daemonizing)
Once everything is installed and configured, you’re ready to start the bot. Since this is on a VPS, you’ll want to run the bot such that it **continues running after you disconnect** from the server, and ideally even after reboots (with some setup).

Navigate to your project directory (where `bot.py` is) in the WSL terminal. Then choose one of the methods below to run `bot.py` continuously:

### 6.1 Using `tmux` (Terminal Multiplexer)
`tmux` allows you to create a persistent terminal session that stays alive even if you disconnect.
1. **Install tmux:**  
   ```bash
   sudo apt install -y tmux
   ```
2. **Start a tmux session:**  
   ```bash
   tmux new -s bot_session
   ```  
   This opens a new tmux session named "bot_session". You will see a regular shell prompt (inside tmux now).
3. **Activate your virtual env:** (if you created one in section 4.2)  
   ```bash
   source bot-env/bin/activate
   ```
4. **Run the bot:**  
   ```bash
   python3 bot.py
   ```  
   Once run, the bot will start up. You should see some log output in the terminal (perhaps it will say it started polling Telegram, etc.). This means the bot is now running.
5. **Detach the tmux session:** Press the keyboard combo **Ctrl+B**, then **D**. This will detach the session and bring you back to the normal shell. The bot process continues to run inside tmux.
6. **Log out safely:** You can now close your SSH or terminal. The `bot.py` will keep running inside the tmux session on the VPS.

Later, if you reconnect and want to see the bot’s output or stop it:
- **Reattach tmux:** `tmux attach -t bot_session` will bring you back into the running session where the bot is running.
- **Stop the bot:** In the tmux session, you can press `Ctrl+C` to stop the bot (this stops the Python program).
- **Exit tmux:** Type `exit` in the tmux shell or press Ctrl+D to close that shell. If the bot process was the last thing, the session might close. You can also kill the tmux session with `tmux kill-session -t bot_session` if needed.

Using tmux is convenient because you can always reattach to see logs or manually restart the bot if needed.

### 6.2 Using `nohup` (No Hangup)
If you prefer not to use tmux, you can use `nohup` to run the bot in background:
1. **Ensure virtual env is activated** (if using one):  
   ```bash
   source bot-env/bin/activate
   ```
2. **Run with nohup:**  
   ```bash
   nohup python3 bot.py > bot.log 2>&1 &
   ```  
   - This starts `bot.py` in the background. The output (stdout/stderr) is redirected to `bot.log`. The `&` puts it in background. The `nohup` ensures it isn’t killed when you log out.
   - After running this, you can close the terminal. The bot will keep running.
3. **Check if running:** You can run `ps aux | grep bot.py` to see if the process is alive. Also check the `bot.log` for output or errors: `tail -f bot.log` to live-monitor the log.
4. **Stopping the bot:** If you need to stop it, find the process ID (from `ps aux`) and use `kill <PID>`. Or if you reboot, it will naturally stop.

### 6.3 After a Server Reboot
By default, the bot **will not automatically start on a Windows reboot** (because WSL and the Python script won’t start on their own). If your VPS restarts, you’ll need to manually start the bot again using the steps above (tmux or nohup).

If you want the bot to start on boot without manual intervention:
- **Option 1: Windows Task Scheduler:** You can create a scheduled task on Windows to run at startup. The action would be something like:  
  `wsl -d Ubuntu-22.04 -e /usr/bin/bash -c "cd /path/to/your/bot && source bot-env/bin/activate && nohup python3 bot.py > bot.log 2>&1"`  
  This instructs Windows to launch WSL, activate the env, and run the bot on boot. This requires some familiarity with Task Scheduler.
- **Option 2: `rc.local` or cron in WSL:** Because WSL doesn’t automatically initiate on boot, this is tricky. However, you could use a workaround: create a script that launches the bot and use Windows startup to call `wsl -e` with that script.
- If you are not comfortable with these, the simplest approach is to **remember to reconnect to the VPS after a reboot and start the bot** manually.

### 6.4 Keep the WhatsApp Web Session Active
When the bot runs, it will use Chrome in headless mode to connect to WhatsApp Web. The first time you run commands like `/linkwhatsapp`, you’ll scan a QR code to log in. The bot saves session info in the `User_Data` directory (in the bot folder). **Do not delete this folder** if you want to stay logged in on WhatsApp Web. If the VPS reboots or the bot restarts, as long as `User_Data` is intact, you typically won’t need to scan the QR code again. However, note that if Chrome/WSL is completely shut down for a long time or if WhatsApp logs out the session, you might need to re-link by using `/linkwhatsapp` again.

## 7. Basic Usage — Telegram Commands
Once the bot is up and running on the VPS, you will interact with it through **Telegram commands**. Below is a summary of the available commands and how to use them. All commands are initiated via a Telegram chat with your bot (either in a private chat or in a group chat as specified):

- **`/start`** – Use this in a **private chat** with your bot. The bot will introduce itself and list the main commands. This is a good way to see if the bot is responsive. It also sends you a menu of what you can do.

- **`/authorize <token>`** – Authorize yourself with the bot. Replace `<token>` with either the admin token or user token that you set in `authorization.py`.  
  - *In a private chat with the bot*: Send `/authorize YourSecretTokenHere`.  
  - If the token matches `ADMIN_TOKEN`, the bot will reply that you are now an admin. If it matches `USER_TOKEN`, you’ll be authorized as a regular user. If it doesn’t match either, you’ll get an "Invalid token" message.  
  **Note:** You need to do this **once** (each time the bot restarts, the authorization list resets). Authorized admins/users are remembered in memory until the bot stops. Make sure to authorize yourself as admin before trying other admin-only commands.

- **`/send <message>`** – **(Admin only)** Send a text message to all **approved Telegram groups** that the bot is a member of.  
  - Use this after you have added the bot to some Telegram groups and approved them (see `/approvegroup`).  
  - Example: `/send Hello everyone, meeting is at 5 PM.`  
  - The bot will iterate through all registered groups that have been approved (whitelisted) and send the message. It will skip any group not approved. After execution, it will reply in your chat indicating the message was sent.

- **`/sendall <message>`** – **(Admins and authorized users)** Broadcast a message to **all platforms**: this sends the message to all approved Telegram groups *and* all registered WhatsApp groups.  
  - This command is handy if you want to send the same announcement to both Telegram and WhatsApp recipients at once.  
  - Example (from a private chat with the bot): `/sendall The event will start in 10 minutes.`  
  - The bot will respond with a summary of how many groups on each platform were successfully sent to, and list any failures (e.g., if some group was unavailable).

- **`/listgroups`** – **(Admin)** List all Telegram group chats that the bot knows about and their status.  
  - When the bot is added to a Telegram group, it doesn’t immediately start sending messages there. Instead, it adds the group to a **pending list** for approval.  
  - `/listgroups` will show “No groups are currently registered” if none have been added, or list groups by name and ID that are approved. (For pending groups, see the next commands.)

- **`/approvegroup <group_id>`** – **(Admin)** Approve a Telegram group for message broadcasting.  
  - Use this command in a private chat with the bot to approve a group that the bot was added to. You must supply the `<group_id>` which is a numerical ID. (The bot will tell you the ID when it was added, see note below.)  
  - Example: `/approvegroup -1001234567890` (Telegram group IDs are typically large numbers, often starting with -100 for supergroups).  
  - Once approved, the group moves to the allowed list, and the bot can send messages to it when using `/send` or `/sendall`. The bot will also notify the group itself that it has been approved (and similarly if rejected).

- **`/rejectgroup <group_id>`** – **(Admin)** Reject a pending group. This removes the group from the pending list and the bot will not send messages there. Use this if an unknown or unauthorized group added your bot and you don’t want to allow it.

- **`/removegroup <group_id>`** – **(Admin)** Remove a previously approved group from the allowed list. If you no longer want the bot to send messages to a certain Telegram group, use this. You’ll have to approve it again if you change your mind later.

  > **How to get `<group_id>`:** When you add the bot to a Telegram group, the bot (if it’s running and you are an admin) will automatically send you (the admin) an alert with the group’s name and ID, indicating it’s pending approval. You can copy that ID for use with approve or reject. Additionally, when the bot is added to a group, it posts a message in the group like “This group has been added to pending approval list...”. So you’ll know a pending group by that notification as well. You can also use `/listgroups` in private to see if any pending groups are waiting (they might not show until approved, so mainly rely on the join notification).

- **`/linkwhatsapp`** – **(Admin)** Initiate linking a WhatsApp account by QR code.  
  - **Use this in a private chat with the bot**, since it will return an image (the QR code) to scan.  
  - When you run `/linkwhatsapp`, the bot will launch WhatsApp Web in Chrome (headless) and capture the login QR code. It will send you a photo of the QR code with instructions. On your phone, open WhatsApp > Linked Devices > Link a Device, and scan that QR code.  
  - The bot keeps the browser session open for a few minutes to allow you to complete the scan. Once scanned, your WhatsApp account is now linked to WhatsApp Web running on the VPS. The bot will store session cookies so you generally don’t need to scan again unless the session expires.  
  - If successful, the bot is now ready to send WhatsApp messages on your behalf. (If you see any error or it doesn't send the QR, make sure Chrome/ChromeDriver is set up correctly and try again.)

- **`/addwhatgroup <group_name>`** – **(Admin)** Register a WhatsApp group for broadcasting.  
  - Since WhatsApp Web can’t list group IDs the same way Telegram does, we use the **exact group name** as it appears in WhatsApp. After linking your WhatsApp (previous step), use `/addwhatgroup` to tell the bot which WhatsApp group chats to target.  
  - Example: `/addwhatgroup Family Chat`  
  - The bot will store "Family Chat" in its `whatsapp_groups` list (with an active status). It will reply with a confirmation. If the group name was already added, it will warn you it exists.  
  - **Ensure the name is exactly as in WhatsApp.** It’s case-sensitive and must match the group’s title. The bot uses this name to search and send messages.

- **`/deletewhatgroup <group_name>`** – **(Admin)** Remove a WhatsApp group from the bot’s list.  
  - Example: `/deletewhatgroup Family Chat` will remove that group from the list, so the bot will no longer send messages to it.

- **`/whatgrouplist`** – **(Admin)** List all WhatsApp group names that are currently registered with the bot. This helps you review which group names the bot will send to when using WhatsApp send commands.

- **`/whatsend <message>`** – **(Admin)** Send a message to all registered WhatsApp groups.  
  - Use this to broadcast a message **only to WhatsApp groups**, using the groups added via `/addwhatgroup`.  
  - Example: `/whatsend Don't forget to check the new schedule.`  
  - The bot will open WhatsApp Web (if not already open), iterate through each group in its list, and send the message. It will then reply to you with how many succeeded and if any failed.  
  - Make sure you have called `/linkwhatsapp` at least once before using this, so that the WhatsApp session is active.

- **`/help`** – Shows a help message (very similar to what `/start` shows) with a list of commands and usage. This is available in private chat. It’s a quick reference if you forget command usage.

**Note on where to use commands:** For security, do all administrative commands like `/authorize`, `/linkwhatsapp`, `/addwhatgroup`, etc., in the bot’s **private chat** with you (the admin). Regular users with only send access would also typically use the bot in a private chat to issue `/send` commands. The bot can operate in groups (for broadcasting), but you wouldn’t normally have people type commands in those groups except maybe `/start` to see the bot’s intro. Adding the bot to a group is mainly for receiving broadcasts, not for others in the group to control the bot.

**Note on WhatsApp web usage:** The bot uses a headless Chrome browser to send WhatsApp messages. This means it might take a few seconds to open WhatsApp Web and send messages for each command. The bot includes some delays between messages to avoid being rate-limited. When you run a WhatsApp send command, watch the console (if attached via tmux) or the log for info messages. Also, avoid sending too frequently to not trigger WhatsApp’s anti-automation measures. Generally, sending normal messages to a few groups should be fine.

---

By following this guide, you should have the Telegram-WhatsApp bot installed on your Windows VPS (via WSL1), properly configured, and running continuously. You can now manage your bot through Telegram commands and have it relay messages to both Telegram groups and WhatsApp groups as needed. 

If you encounter any issues:
- Re-check each step (WSL installation, Chrome/Driver versions, Python environment, tokens).
- Ensure the VPS is running and not sleeping.
- Look at the `bot.log` (if using nohup) or tmux console for error messages (for example, Selenium errors if Chrome/Driver not set up correctly, or Telegram API errors).
- Common issues might be ChromeDriver version mismatches (addressed by updating the driver) or forgetting to authorize yourself before using commands.

Good luck! If everything is done correctly, the bot will be a powerful tool to send announcements across Telegram and WhatsApp with a single command. ([Manual installation steps for older versions of WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install-manual#:~:text=We%20recommend%20now%20moving%20on,on%20to%20the%20next%20step)) ([Run Linux GUI apps with WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps#:~:text=1,stable_current_amd64.deb))】




