[< previous](otp-project-overview.md)  |  [home](README.md)  |  [next >](project-folder-structure.md)

# Eils-HPC

- The eils-hpc is not the BIH-HPC
- Governance is determined by The Centre for Digital Health
    - Roland Eils
    - Naveed Ishaque
    - Christian Conrad
    - Juergen Eils
    - Harald Wagener
- Access is based on your Charite user name and password (no additional user credential required!)

## Hardware overview

The cluster consists of the following systems:

- Login Nodes
    - 2 nodes@ `eils-login1.bihealth.org` and `eils-login2.bihealth.org`
    - PowerEdge R740XD Server (batch 2018/1)
        - 2x Intel Xeon 6130 @2.1 GHz (16 cores/32 threads)
        - 384 GB RAM
        - 2x 800 GB SSD (mirror)
        - 2x 25 GbE NIC QLogic FastLinQ 41262
- Compute Nodes
    - 32 standard compute node node: `eils-compute{001..032}`
    - PowerEdge C6420 Server (batch 2018/1)
        - 2x Intel Xeon 6130 @2.1 GHz (16 cores/32 threads)
        - 512 GB RAM
        - 2x 120 GB SSD (mirror)
        - 2x 25 GbE NIC QLogic FastLinQ 41262
- 2 GPU nodes
    - eils-gpu{1,2}
    - NVIDA DGX-1 Server (batch 2018/1)
        - 2x Intel Xeon E5-2689 v4 @2.2 Ghz (20 cores/40 threads)
        - 512 GB RAM
        - 8x NVIDIA Tesla GP100
        - 4x 1.92 TB SSD RAID-0
        - **OS: Ubuntu Server Linux OS**
- 2 FPGA Nodes
    - eils-fpga{1,2}
    - PowerEdge R740 Server (batch 2018/1)
        - 2x Intel Xeon 8180 @2.5 GHz (28 cores/56 threads)
        - 256 GB RAM
        - 4x Intel 10 GX FPGA
        - 2x 240 GB SSD (mirror)
        - 2x 25 GbE NIC Intel XXV710
- Isilon Storage System
    - 12 A200 nodes (HPC)
    - 4 F800 nodes (HPC)

## Operating System and software
- The cluster runs CentOS 7 (RHEL derivative).
- Only core software is managemed by the system admin
- All scientific software is managed by the users
   - we encourag the use of conda!

[< previous](otp-project-overview.md)  |  [home](README.md)  |  [next >](project-folder-structure.md) 
