# Home Lab Foundation
## Overview
Base installation reference for home lab projects. Future lab projects should link to this repository for VMware and ISO setup rather than duplicating these instructions.

## VMware Workstation Pro Installation
1. Navigate to Broadcom Support Portal
2. Select [VMware Workstation Pro](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Workstation+Pro) > Version 17.x
3. Download the installer for your host OS
4. Run installer with default settings
5. Obtain licence key from Broadcom portal (free for personal/educational use)

**Note:** Requires free Broadcom account for access to downloads.

## Operating System ISOs
- [Windows 11 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
- [Windows Server 2022 Standard](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
- [Ubuntu 22.04 LTS Desktop](https://ubuntu.com/download/desktop)
- [Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)

*Adjust VM specifications based on your host resources and project requirements.*

## Configuring NAT Network
To connect VMs to the same network whilst maintaining internet access:

1. Open VMware Workstation Pro
2. Navigate to Edit > Virtual Network Editor
3. Verify VMnet8 (NAT) exists with desired subnet (default: 192.168.10.0/24)
4. For each VM:
- Right-click VM > Settings
- Select Network Adapter
- Choose NAT: Used to share the host's IP address
- Click OK
5. Power on VMs - they'll receive DHCP addresses in the same subnet
6. Verify connectivity with ping between VMs

**Note:** For static IP assignments, configure network settings within each guest OS rather than relying on DHCP.

## Troubleshooting
### Ping Windows → Ubuntu Failed
- Resolved by disabling Ubuntu's firewall temporarily (`sudo ufw disable`) to confirm connectivity, then re-enabled with ICMP allowed (`sudo ufw allow from 192.168.10.0/24`).

### Ping Ubuntu → Windows Failed
- Resolved by disabling Windows Defender's (Start > Settings > Update & Security > Windows Security > Virus & threat protection) as ICMP is blocked by default. Tested to confirm connectivity.

## Additional Resources
- [VMware Workstation Pro Documentation](https://docs.vmware.com/en/VMware-Workstation-Pro/)
- [VMware NAT Networking Guide](https://docs.vmware.com/en/VMware-Workstation-Pro/17/com.vmware.ws.using.doc/GUID-89311E3D-CCA9-4ECC-AF5C-C52BE6A89A95.html)