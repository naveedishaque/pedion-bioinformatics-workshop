[< previous](data-management.md)  |  [home](README.md)  |  [next >](otp-project-overview.md)

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
   
## Running tools and scripts on the cluster
- The login nodes provide access to the cluster
- Loging nodes should only be used for computational light tasks
- Heavy computation (e.g. alignment, variant calling) should be performed on a compute node:
    - submitting a non-interactive "job"
    - interactive sesion on a compute node
    
## Submitting "jobs"
- Scheduling is managed by IBM LSF
    - [Official Guide](https://www.ibm.com/support/knowledgecenter/en/SSWRJV_10.1.0/lsf_welcome/lsf_welcome.html)
    - ["Rossetta stone" for translating commands between schedulers](https://slurm.schedmd.com/rosetta.pdf)
    - [Reference manual](https://www.tu-ilmenau.de/fileadmin/media/unirz/Services/Struktureinheiten/Advanced_Computing/lsf101_command_ref.pdf)
- Submitting jobs:
    - submitting a script: `bsub`
    - interactive session: `bsub -Is sh`
- Submitting jobs.. extended!
    - Jobs are allocated resources like time, memory and CPU:
        - STDERR log: `-e <error_log.txt>`
        - STDOUT log: `-o <out_log.txt>`
        - Queue: `-q <QUEUE>`
        - Process count: `-R “span[ptile=<M>]”`
        - Process count: `-n <P> -R “span[ptile=<M>]”`	
        - Wall clock limit: `-W <HH:MM>	`
        - Memory limit: `-R “rusage[mem=<N>]”`
        - Interactive job: `-Is sh`
        - Interactive/X11 job: `-Is -XF sh`
        - Job Name: `-J <NAME>`
        - Environment Variables: `-env “all, VAR=value

# Tasks

0. Log onto the cluster: `ssh eils-login1@bihealth.org`
1. Submit a simple job listing files:
```
bsub -J my_first_job -o out_report.txt -e err_report.txt ls -lah
cat err_report.txt
cat out_report.txt
```
2. ... one more time, now pay attention to what happens to the output/error log files:
```
bsub -J my_first_job -o out_report.txt -e err_report.txt ls -lah
cat err_report.txt
cat out_report.txt
```
3. ... one more time, now combine the logs:
```
bsub -J my_first_job -eo errout_report.txt ls -lah
cat errout_report.txt
```
3. Monitor a job. For this we will submit a job that does nothing:
```
bsub sleep 200
bjobs
bjobs -l
```
4. Monitor output from a job. For this we will submit a job that does nothing:
```
echo "echo start && sleep 50 && echo middle && sleep 50 && echo end" | bsub
bpeek
bpeek
bpeek
bpeek
bpeek
bpeek
bpeek
bpeek
```
5. Submit a job script that counts from 1 to 100
 - create a script which contains the following using vim, nano, emacs, or yout favourite editor
```
#!/bin/bash
seq 1 100
```
 - submit that job: `bsub lsf_script.sh`
6. There is much more that can be done with LSF, but that isnt the purpose of this session... moving on!

[< previous](data-management.md)  |  [home](README.md)  |  [next >](otp-project-overview.md)
