# Hyper-V
MS Hyper-V Resources, References, &amp; Guides

**MS Hyper-V Documentation**  
https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/  

**Hyper-V EDR/AV Exclusions**  
https://learn.microsoft.com/en-us/troubleshoot/windows-server/virtualization/antivirus-exclusions-for-hyper-v-hosts  

**Nakivo Hyper-V Resources**
https://www.nakivo.com/blog/platform/hyper-v/

**Hyper-V Security Best Practices**  
https://www.starwindsoftware.com/blog/hyper-v-security-mistakes-dont-want-make/  

**How to Install Hyper-V**  
https://www.nakivo.com/blog/how-to-install-hyper-v-on-windows-server-2019-step-by-step/  

**Hyper-V - Core vs. GUI**  
https://www.nakivo.com/blog/hyper-v-server-core-vs-gui-installation-compare/  

**Hyper-V Networking Best Practices**  
https://www.nakivo.com/blog/hyper-v-networking-best-practices/  

**Hyper-V Virtual Switches**  
https://www.nakivo.com/blog/hyper-v-networking-virtual-switches/  

**Hyper-V Storage Best Practices**  
https://www.nakivo.com/blog/hyper-v-storage-best-practices/  

**Hyper-V Cluster Setup**  
https://www.nakivo.com/blog/hyper-v-cluster-setup/  

**Starwind Resources**  
https://www.starwindsoftware.com/technical_papers/StarWind_HA_Hyper-V_6.0.pdf  
https://www.starwindsoftware.com/datasheets/starwind-iscsi-san-for-hyperv-data-sheet.pdf  

**Configure iSCSI & MPIO**  
https://infohub.delltechnologies.com/en-us/l/dell-powerstore-microsoft-sql-server-2022-on-microsoft-hyper-v-deployment-and-best-practices/configure-iscsi-and-mpio-for-hyper-v-hosts/  

**Core Architecture Options**  
Virtual SAN (VSAN): Installed directly as a Windows application or virtual machine on Hyper-V nodes for hyper-converged HA storage.  
SAN and NAS Appliance: Dedicated VM (Linux/ZFS-based) exposing iSCSI storage targets to hypervisors.  

**Essential Setup Steps**  
Prerequisites: Install Failover Clustering, Multipath I/O (MPIO), and the Hyper-V role on target host servers.  
Network Design: Keep iSCSI/heartbeat traffic on separate physical/virtual adapters without NIC teaming for StarWind synchronization links.  
MPIO Configuration: Enable MPIO support for iSCSI devices under Windows management features.  
Target Connection: Open the Microsoft iSCSI Initiator, discover portal IPs, and connect targets with multi-path checked.  
Disk Initialization: Bring disks online via Server Manager Disk Management and format/initialize for CSV (Cluster Shared Volume) use.  

**Best Practices & Performance Tips**  
No NIC Teaming: StarWind explicitly advises against NIC teaming for synchronization/iSCSI channels; use dedicated redundant physical links instead.  
Pass-through vs VHDX: Pass entire RAID arrays or use thick-provisioned virtual disks to avoid severe performance degradation.  
VMQ Tuning: Disable Virtual Machine Queue (VMQ) if experiencing lagging disk performance under heavy loads.  

**NOTES**
Ensure at least dual 10Gbe NICs are used (ethernet or fiber)  
Jumbo Frames Enabled (MTU 9000)  
Dedicated network for storage traffic & communications  
Dedicated VLAN & IP Subnet  
STATIC IP's only for each HOST and SAN target  
Do not use a NIC team, simply enable MPIO on each adapter on the Hyper-V host  
Take note of your iSCSI Initiator configuration on each host  
