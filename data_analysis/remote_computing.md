---
title: Remote Computing
label: remote_computing
abbreviations:
    HPC: High Performance Computing
    CPU: Central Processing Unit
    FLOPS: Floating point operations per second
bibliography:
    remote_computing.bib
---

```{important} Learning outcomes
After completing this section you should be able to:
- learning_outcome1
- learning_outcome2
```

## Introduction
Physically remote
– Other side of planet
– Other side of door you are not allowed in
– (massively) shared
• Machines dedicated to specialized tasks
– ‘servers’
• Webserver
• Databaseserver
• etc
– High Performance Computing
• “Super computer”
• Computer cluster

## High Performance Computing
High Performance Computing (HPC) uses supercomputers and computer clusters working in parallel to process huge data sets and solve complex problems. In advance of HPC, the first computer that could successfully use multiple CPUs was the [Cray 2](wiki:Cray-2). If we compare the specifications of the Cray 2 to a modern smartphone ([](#table_supercomputers_specs)), one could see that we are currently carrying devices 2000 times faster than the first supercomputer in our pockets, running on just a few watts. Though, the current champion of modern supercomputers far exceeds both: the [LineShine](https://en.wikipedia.org/wiki/LineShine) (China) reached 2.198 ExaFLOPS performance and operates exclusively on 13.79 million CPU cores [@top500_june_2026].

(table_supercomputers_specs)=
:::{list-table} Old supercomputer vs. modern smartphone
:header-rows: 1
* - Computer
  - Year
  - Cost
  - FLOPS
  - RAM
  - Storage
  - Power use
* - Cray 2
  - 1985
  - $16,000,000
  - 800 MFLOPS
  - Up to 128 MB
  - 10GB
  - 200 kW
* - Samsung Galaxy S26
  - 2026
  - $700
  - 3.68 TFLOPS
  - 12 GB
  - 128
  - max 25W
:::

## Clusters and Servers
Computer clusters consist of many computers, or compute nodes. They have a shared file system and one or several "head nodes" that mastermind the processes ([](#figure_computer_cluster)). The head nodes ensure resource allocation to tasks and distribute jobs to the compute nodes.

(figure_computer_cluster)=
:::{figure} img/computer_clusters.svg
Diagram of a computer cluster containing one head node and three compute nodes
:::


Almost all computer clusters and many servers run Linux. Connections are made using ssh-based protocols ([](#table_connection_protocols)). In all cases, you will have at least a terminal and in most cases you will not have anything else.

(table_connection_protocols)=
:::{list-table} ssh-based protocols for connecting to computer clusters and servers
:header-rows: 1
* - Connection protocol
  - Service
* - ssh
  - Secure shell
* - scp
  - Secure copy
* - rsync
  - Syncing file, can also be done over ssh
:::

### Restrictions
Apart from the fact that you often only have a terminal available to use a remote computer, there are other restrictions. Not everything is possible on a remote computer that you can do on your own desktop due to system permissions. This is to ensure stability and security of system. Therefore, you need to know how to deal with that by understanding the limitations and the work-arounds. Additionaly, you need to know how to properly schedule your compute jobs using job schedulers or resource allocation software.

### Resource Allocation
On computer clusters jobs need to be scheduled because there are often more jobs than space or capacity on the cluster. They are scheduled based on estimated memory and {term}`CPU` cores usage. Highly specialized software designed for this task are called job schedulers. Some common ones are [slurm](https://slurm.schedmd.com/overview.html) and Gridware Cluster Scheduler. 

WUR has a HPC cluster called [Anunna](https://wiki.anunna.wur.nl/Main_Page) and it uses slurm as job scheduler *#! allowed to mention this?*
It contains 100 "normal sized" compute nodes, six "fat" nodes (64 cores each with 4 TB of memory), six {term}`GPU` nodes, and a 3.0PB parallel file system ([Lustre](https://en.wikipedia.org/wiki/Lustre_(file_system))).

To use the HPC, we would need to create a job script for slurm ([](#example_skeleton_slurm_job_script)).

(example_skeleton_slurm_job_script)=
``````{prf:example} Skeleton for a slurm job script
```{code-block} bash
:filename: skeleton.sh
#!/bin/bash

#-----------------------------Mail address-----------------------------
#SBATCH --mail-user=
#SBATCH --mail-type=ALL
#-----------------------------Output files-----------------------------
#SBATCH --output=output_%j.txt
#SBATCH --error=error_output_%j.txt
#-----------------------------Other information------------------------
#SBATCH --comment=
#SBATCH --qos=
#-----------------------------Required resources-----------------------
#SBATCH --time=0-0:0:0
#SBATCH --ntasks=
#SBATCH --cpus-per-task=
#SBATCH --mem-per-cpu=

#-----------------------------Environment, Operations and Job steps----
# load modules

# export variables

# your job
```
``````


### File systems
All nodes on the HPC cluster have the same network file system mounted. A network file system (NFS) is one physical filesystem served by one machine to many others. It behaves a bit like the 'M:' drive in Windows. Alternatively, a HPC cluster can have a parallel filesystem, which has a much higher read/write speed than an NFS. Lustre on Anunna is a parallel filesystem.

*#! is this correct?*

### Software
On a HPC cluster, it might be necessary to have dozens of different versions of the same software to be available. Software may need to be compiled from source and doing that across a HPC cluster is a dependency nightmare. Thus, user do not have write permissions to system folders. Instead, one should install in `$HOME/bin` or other shared parts of the file system. 

To ensure multiple modules and dependencies are correct for your specific task, it is best to use a package manager such as [conda](https://docs.conda.io/en/latest/) or [mamba](https://mamba.readthedocs.io/en/latest/). 

### Performance and Capacity



## Exercises

### Command Line Strategies for Using Remote Computers

### Data Transfer – Data Integrity (checksums)