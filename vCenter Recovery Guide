# 🚀 vCenter Recovery Guide (After Deletion)

This guide provides step-by-step instructions to remove an old vCenter cluster from ESXi and install a new vCenter Server.

---

## **🔍 Step 1: Check Cluster & Hosts Status**
After vCenter is deleted, the ESXi hosts remain part of the cluster but function independently. To check:
```bash
esxcli network ip interface ipv4 get
esxcli vm process list
vim-cmd vmsvc/getallvms
```
If the hosts are still connected to the old vCenter, you may need to manually remove the cluster.

---

## **🗑️ Step 2: Remove Old Cluster from ESXi Hosts**
Since the cluster is no longer managed by vCenter, you need to disband it manually:

1️⃣ **Disconnect ESXi Hosts from the Old vCenter (if accessible):**
```powershell
Disconnect-VIServer -Server <vcenter-ip> -Confirm:$false
```

2️⃣ **Remove the ESXi Hosts from the Cluster (if vCenter is down, do this manually on each host):**
```bash
esxcli system maintenanceMode set --enable true
vim-cmd hostsvc/maintenance_mode_enter
vim-cmd hostsvc/advopt/update Syslog.global.logHost string ""
```

3️⃣ **Reconfigure Management Network (if needed):**
```bash
esxcli network ip interface set -i vmk0 -e true
esxcli network ip dns server add --server=<dns-server>
```

4️⃣ **Leave the Cluster and Revert ESXi Hosts to Standalone Mode:**
```bash
vim-cmd hostsvc/enable_ssh
vim-cmd hostsvc/advopt/update "UserVars.SuppressShellWarning" long 1
vim-cmd solo/registervm <vmx-path>
```

---

## **🛠️ Step 3: Install vCenter on ESXi**
1️⃣ **Download vCenter ISO** from [VMware](https://customerconnect.vmware.com/).  
2️⃣ **Deploy vCenter Server Appliance (VCSA) on ESXi** using:
   - **GUI Installer:**
     - Run `vcsa-ui-installer` from the ISO and follow the wizard.
   - **CLI Installer:**
     ```bash
     vcsa-deploy install --accept-eula --acknowledge-ceip vcsa-cli-installer/templates/install/embedded_vCSA_on_ESXi.json
     ```
3️⃣ **Complete the Initial Setup:**
   - Access vCenter Web UI: `https://<vcenter-ip>:5480`
   - Configure SSO domain: `vsphere.local`
   - Set network & NTP settings

---

## **🔗 Step 4: Reconnect ESXi Hosts to vCenter**
Once vCenter is installed:
1️⃣ **Log into vCenter Web UI:**
   ```
   https://<vcenter-ip>/ui
   ```
2️⃣ **Add ESXi Hosts:**
   - Go to **Hosts & Clusters** > **Add Host**
   - Enter ESXi host **IP/hostname**, root credentials
3️⃣ **Reconfigure Networking & Storage (if needed)**
4️⃣ **Verify Cluster Functionality & VM Status**

---

## 🎉 **Final Steps**
✔ Ensure vCenter services are running: `https://<vcenter-ip>:5480`
✔ Set up backups for vCenter
✔ Reconfigure HA/DRS settings if required

🚀 **Congratulations! Your vCenter has been successfully recovered and reinstalled.**

