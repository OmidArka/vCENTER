Installing VMware vCenter on ESXi

This guide provides step-by-step instructions for deploying VMware vCenter Server Appliance (VCSA) on an ESXi host.
📌 Prerequisites

Before proceeding with the installation, ensure you have:
✔ A running ESXi host (7.x or later)
✔ vCenter Server Appliance (VCSA) ISO (Download from VMware)
✔ Minimum system requirements:

    CPU: 2 vCPUs
    RAM: 12GB+
    Storage: 150GB+ (SSD recommended)
    ✔ A system with network access to the ESXi host

🛠 Step 1: Download & Extract vCenter ISO

1️⃣ Download the latest VCSA ISO from the VMware portal.
2️⃣ Mount or extract the ISO:

    Windows: Use built-in File Explorer to mount the ISO.
    Linux/Mac:

    mount -o loop vcsa.iso /mnt

🚀 Step 2: Deploy vCenter on ESXi
🔹 Option 1: Using GUI (vCenter Installer)

1️⃣ Navigate to the extracted ISO and run the vCenter Installer:

    Windows: vcsa-ui-installer\win32\installer.exe
    Mac: vcsa-ui-installer/mac/Installer.app
    Linux: vcsa-ui-installer/lin64/installer

2️⃣ Click Install and accept the EULA.
3️⃣ Provide the ESXi host details (IP, username, password).
4️⃣ Select a datastore and configure network settings.
5️⃣ Proceed with the installation and wait (~15-30 min).
🔹 Option 2: Using CLI (Automated Deployment)

For automated deployment, modify the JSON configuration file:
1️⃣ Edit the deployment template:

nano vcsa-cli-installer/templates/install/embedded_vCSA_on_ESXi.json

2️⃣ Update ESXi details, network settings, and credentials.
3️⃣ Run the installer:

vcsa-deploy install --accept-eula --acknowledge-ceip vcsa-cli-installer/templates/install/embedded_vCSA_on_ESXi.json

⚙ Step 3: Initial vCenter Configuration

1️⃣ Once deployed, open vCenter Appliance Management:

https://<vcenter-ip>:5480

2️⃣ Log in with root credentials.
3️⃣ Complete the Setup Wizard:

    Configure SSO domain (default: vsphere.local)
    Apply licensing (or use evaluation mode)
    Set NTP & network settings
    4️⃣ Access the vCenter Web UI:

https://<vcenter-ip>/ui

✅ Post-Installation Checklist

✔ Connect an ESXi host to vCenter
✔ Verify vCenter services (https://<vcenter-ip>:5480)
✔ Configure backups & monitoring
