# Installing Splunk Enterprise on Ubuntu Desktop

This guide walks you through downloading and installing Splunk Enterprise on an Ubuntu Desktop virtual machine (VM) using simple steps.

---

## Prerequisites

- An Ubuntu Desktop VM (or physical machine) with a working internet connection.  
- A user account with sudo (administrative) privileges.

---

## Step 1 — Download Splunk Enterprise

1. Open a web browser (Firefox or any browser) on the Ubuntu VM and go to the Splunk Enterprise download page.  
   Note: Splunk requires creating a free account before downloading.

2. Choose the correct file:
   - Select the "Linux" tab.
   - Choose the `.deb` package (for Ubuntu/Debian).
   - Click **Download**. The file will typically save to your `Downloads` folder.

(Include a screenshot of selecting the `.deb` package and clicking Download if desired.)

---

## Step 2 — Install Splunk Enterprise

1. Open the Terminal (shortcut: `Ctrl + Alt + T`).

2. Change to the Downloads directory:
   ```bash
   cd ~/Downloads
   ```

3. Install the downloaded `.deb` package. Replace `splunk-x.x.x-xxxxxx.deb` with the actual filename:
   ```bash
   sudo dpkg -i splunk-x.x.x-xxxxxx.deb
   ```
   - `sudo`: run with administrative privileges.  
   - `dpkg -i`: installs a `.deb` package.

(Include a screenshot of the terminal showing successful `dpkg` installation output if desired.)

---

## Step 3 — Start Splunk and Set Up Admin Credentials

1. Start Splunk for the first time (this accepts the license):
   ```bash
   sudo /opt/splunk/bin/splunk start --accept-license
   ```
   - During first start, you will be prompted to create an admin username and password for the Splunk Web interface. Record these credentials.

(Include a screenshot of the terminal during the first start showing the prompt for admin credentials.)

2. Check Splunk status:
   ```bash
   sudo /opt/splunk/bin/splunk status
   ```
   Expected result: the Splunk daemon is running and the web interface is available on port `8000`.

(Include a screenshot verifying `splunk status` if desired.)

3. Enable Splunk to start automatically on boot (recommended):
   ```bash
   sudo /opt/splunk/bin/splunk enable boot-start
   ```

---

## Step 4 — Access the Splunk Web Interface

1. Open a browser on the VM and go to:
   ```
   http://localhost:8000
   ```

2. Log in using the administrator username and password created in Step 3.

(Include a screenshot of the Splunk Web login page if desired.)

3. After logging in, you should see the main Splunk Home dashboard. Splunk is now installed and running.

---
