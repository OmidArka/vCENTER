Installation

Follow these steps to set up your environment for using vCenter automation scripts.
1️⃣ Clone the Repository

First, clone this repository to your local machine:

git clone https://github.com/your-repo/vcenter-automation.git
cd vcenter-automation

2️⃣ Install PowerCLI (for PowerShell Users)

If you are using PowerCLI, install it via PowerShell:

Install-Module -Name VMware.PowerCLI -Scope CurrentUser -Force -SkipPublisherCheck

Ensure PowerCLI is working by running:

Get-Module -ListAvailable VMware.PowerCLI

3️⃣ Install Python Dependencies (for API-based scripts)

If you are using Python, install the required dependencies:

pip install -r requirements.txt

Verify installation:

python -c "import requests; print('Dependencies installed successfully!')"

4️⃣ Configure vCenter Connection

For PowerCLI:

Connect-VIServer -Server <vcenter-IP> -User <your-username> -Password <your-password>

For Python scripts, update config.json:

{
  "vcenter_server": "your-vcenter-ip",
  "username": "your-username",
  "password": "your-password"
}

5️⃣ Test the Setup

Run a basic script to verify connectivity:
For PowerCLI:

.\Get-VMs.ps1

For Python:

python get_vms.py

