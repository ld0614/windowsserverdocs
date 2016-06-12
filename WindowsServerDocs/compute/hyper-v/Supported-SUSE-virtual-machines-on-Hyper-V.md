---
title: Supported SUSE virtual machines on Hyper-V
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - hyper-v
  - techgroup-compute
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
author: cwatsonmsft
---
# Supported SUSE virtual machines on Hyper-V
The following is a feature distribution map that indicates the features in each version. The known issues and workarounds for each distribution are listed after the table.  
  
The built-in SUSE Linux Enterprise Service drivers for Hyper-V are certified by SUSE. An example configuration can be viewed in this bulletin: [SUSE YES Certification Bulletin](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176).  
  
**Table legend**  
  
-   **Built in** – LIS are included as part of this Linux distribution.  The Microsoft\-provided LIS download package does not work for this distribution, so do not install it.  The kernel module version numbers for the built in LIS \(as shown by **lsmod**, for example\) are different from the version number on the Microsoft\-provided LIS download package. A mismatch doesn't indicate that the built in LIS is out of date.  
  
-   **√** \- Feature available  
  
-   \(*blank*\) \- Feature not available  
  
|**Feature**|**Windows Server operating system version**|**SLES 12 SP1**|**SLES 12**|**SLES 11 SP4**|**SLES 11 SP3**|**SLES 11 SP2**|**Open SUSE 12.3**|  
|-|-|-|-|-|-|-|-|  
|**Availability**||Built\-in|Built\-in|Built\-in|Built\-in|Built\-in|Built\-in|  
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|**[Networking](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**||  
|Jumbo frames|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|VLAN tagging and trunking|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|Live migration|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|Static IP Injection|2016, 2012 R2, 2012|**√**  Note 1|**√**  Note 1|**√**  Note 1|**√**  Note 1|**√**  Note 1|**√**  Note 1|  
|vRSS|2016, 2012 R2|**√**|**√**|||||  
|TCP Segmentation and Checksum Offloads|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**||||  
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**||  
|VHDX resize|2016, 2012 R2|**√**|**√**|**√**|**√**|||  
|Virtual Fibre Channel|2016, 2012 R2|**√**|**√**|**√**|**√**|||  
|Live virtual machine backup|2016, 2012 R2|**√** Note 2, 3, 8|**√** Note 2, 3, 8|**√** Note 2, 3, 8|**√** Note 2, 3, 8|||  
|TRIM support|2016, 2012 R2|||||||  
|SCSI WWN|2016, 2012 R2|||||||  
|**[Memory](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**||  
|Configuration of MMIO gap|2016, 2012 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|Dynamic Memory – Hot Add|2016, 2012 R2, 2012|**√** Note 5, 6|**√** Note 5, 6|**√** Note 4, 5, 6|**√** Note 4, 5, 6|||  
|Dynamic Memory – Ballooning|2016, 2012 R2, 2012|**√** Note 5, 6|**√** Note 5, 6|**√** Note 4, 5, 6|**√** Note 4, 5, 6||**√** Note 4, 5, 6|  
|Manual Memory Hot Add|2016|||||||  
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**||  
|Hyper\-V\-specific video device|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|||  
|**[Miscellaneous](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**||  
|Key\/value pair|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√** Note 7|**√** Note 7|**√** Note 7|**√** Note 7|  
|Non\-Maskable Interrupt|2016, 2012 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|PAE Kernel Support|2016, 2012 R2, 2012, 2008 R2|**√**|**√**|**√**|**√**|**√**|**√**|  
|File copy from host to guest|2016, 2012 R2|**√**|**√**|**√**||||  
|lsvmbus command|2016, 2012 R2, 2012, 2008 R2|||||||  
|Hyper-V Sockets|2016|||||||  
|**[Generation 2 virtual machines](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**||  
|Boot using UEFI|2016, 2012 R2|**√** Note 9|**√** Note 9|**√** Note 9||||  
|Secure boot|2016, 2012 R2|√|√|||||  
  
## <a name="BKMK_notes"></a>Notes  
  
1.  Static IP injection may not work if **Network Manager** has been configured for a given Hyper\-V\-specific network adapter on the virtual machine. To ensure smooth functioning of static IP injection please ensure that Network Manager is turned off completely or has been turned off for a specific network adapter through its **ifcfg\-ethX** file.  
  
2.  If there are open file handles during a live virtual machine backup operation, then in some corner cases, the backed\-up VHDs might have to undergo a file system consistency check \(fsck\) on restore.  
  
3.  Live backup operations can fail silently if the virtual machine has an attached iSCSI device or direct\-attached storage \(also known as a pass\-through disk\).  
  
4.  Dynamic memory operations can fail if the guest operating system is running too low on memory. The following are some best practices:  
   
     -   Startup memory and minimal memory should be equal to or greater than the amount of memory that the distribution vendor recommends.  
     -   Applications that tend to consume the entire available memory on a system are limited to consuming up to 80 percent of available RAM.  
  
5.  Dynamic memory support is only available on 64\-bit virtual machines.  
  
6.  If you are using Dynamic Memory on Windows Server 2016 Technical Preview or  Windows Server 2012  operating systems, specify **Startup memory**, **Minimum memory**, and **Maximum memory** parameters in multiples of 128 megabytes \(MB\). Failure to do so can lead to Hot\-Add failures, and you may not see any memory increase in a guest operating system.  
  
7.  In Windows Server 2016 Technical Preview or  Windows Server 2012 R2 , the key\/value pair infrastructure might not function correctly without a Linux software update. Contact your distribution vendor to obtain the software update in case you see problems with this feature.  
  
8.  VSS backup will fail if a single partition is mounted multiple times.  
  
9. On  Windows Server 2012 R2  Generation 2 virtual machines have secure boot enabled by default and Generation 2 Linux virtual machines will not boot unless the secure boot option is disabled. You can disable secure boot in the **Firmware** section of the settings for the virtual machine in Hyper\-V Manager or you can disable it using Powershell:  
  
    ```  
    Set-VMFirmware –VMName "VMname" -EnableSecureBoot Off  
  
    ```  
  
See Also  
  
-   [Set-VMFirmware](http://technet.microsoft.com/library/dn464287.aspx)  
  
-   [Supported CentOS and Red Hat Enterprise Linux virtual machines on Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)  
  
-   [Supported Debian virtual machines on Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)  
  
-   [Supported Oracle Linux virtual machines on Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)  
  
-   [Supported Ubuntu virtual machines on Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)  
  
-   [Supported FreeBSD virtual machines on Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)  
  
-   [Feature Descriptions for Linux and FreeBSD virtual machines on Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)  
  
-   [Best Practices for running Linux on Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)  
