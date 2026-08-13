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
Computer clusters consist of many computers, or compute nodes. Compute nodes are the workhorses of a cluster. Many HPC clusters have several nodes optimized for particular jobs. Some nodes may have larger amounts of memory, or specialized resources such as Graphical Processing Units (GPUs). Clusters also have a shared file system and one or several "head nodes" that mastermind the processes ([](#figure_computer_cluster)). The head nodes ensure resource allocation to tasks and distribute jobs to the compute nodes.

(figure_computer_cluster)=
:::{figure} img/computer_clusters.svg
Diagram of a computer cluster containing one head node and three compute nodes
:::


WUR has a HPC system called [Anunna](https://wiki.anunna.wur.nl/Main_Page). An HPC system is comprised of a multitude of integrated processing and storage elements, designed to handle high volumes of data and/or large numbers of floating-point operations (FLOPS) with the highest possible performance. Be aware that the HPC systems are among the most powerful computers in the world. Most machines on the Top-500 list are HPC systems. The HPC systems are often maintained in centers specifically designed to support heavy computing and with large bandwidths (i.e. the maximum rate of data transfer).

Anunna contains 100 "normal sized" compute nodes, six "fat" nodes (64 cores each with 4 TB of memory), six {term}`GPU` nodes, and a 3.0PB parallel file system ([Lustre](https://en.wikipedia.org/wiki/Lustre_(file_system))).


## Using a HPC system
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

Apart from the fact that you often only have a terminal available to use a remote computer, there are other restrictions. Not everything is possible on a remote computer that you can do on your own desktop due to system permissions. This is to ensure stability and security of system. Therefore, you need to know how to deal with that by understanding the limitations and the work-arounds. 

### Resource Allocation
On computer clusters, jobs need to be scheduled because there are often more jobs than space or capacity on the cluster. If everybody just starts their jobs at random nodes it will soon get quite messy and the system might be overloaded with tasks. Hence, HPC systems work with a workload manager or job scheduler. The jobs are are scheduled based on estimated memory and {term}`CPU` cores usage. 

Anunna uses [slurm](https://slurm.schedmd.com/overview.html) as job scheduler. slurm is a free and open-source job scheduler for Linux and Unix-like kernels, used by many of the world's supercomputers and computer clusters. SLURM is therefore the "manager" between the headnode
and the compute nodes.


To perform tasks on the HPC cluster you need to write a "batch" script that you can submit to the job scheduler ([](#example_skeleton_slurm_job_script)). SLURM will take care of the job and will assign it to a free node.

When running jobs on a HPC system you need to specify the resources required for the job up front. This means that you need to think about the number of CPUs and amount of memory your job requires. These requirements help the scheduler to find the right time and place to execute the job. Some important requirements are listed in [](#table_job_script_directives)

(table_job_script_directives)=
:::{list-table} Some directives to include in a job script
:header-rows: 1
* - Directive
  - Syntax
  - Short syntax
  - Description
* - Number of tasks
  - `--ntasks=<ntasks>`
  - `-n <ntasks>`
  - How many CPU cores does your job need
* - Time limit
  - `--time <days-hours:minutes:seconds>` 
  - `-t <days-hours:minutes:seconds>`
  - How much real-world time will your job take to run? The `<days>` part can be omitted.
* - Memory
  - `--mem=<megabytes>`
  - 
  - How much memory on a node does your job need in megabytes? You can also specify gigabytes using by adding a little "`g`" afterwards (for example: `--mem=5g`)
* - Nodes
  - `--nodes=<nnodes>`
  -  `-N <nnodes>`
  - How many separate machines does your job need to run on?
:::


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
The Anunna cluster may be big, but it is finite in size. In addition, using resources may come at a monetary cost. It is, therefore, important to monitor and benchmark behavior by time (walltime and total time) and RAM. Parallel computing is used to accelerate processing certain tasks. Next, it is important to be aware of file sizes and file system use. Preferably, we keep data in a compressed format, and read and write from and to compressed files. We should also aim to reduce redundancy by not having multiple copies of the same file stored on the system. Last, we should be aware that moving around data has a limit called the network bandwidth.


## Exercises

### Command Line Strategies for Using Remote Computers

### Data Transfer – Data Integrity (checksums)