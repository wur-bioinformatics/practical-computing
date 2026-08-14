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
Almost all computer clusters and many servers run Linux. Copying the files that are required for your analyses (data, scripts, and anything else) from one machine to the machine you will use to perform the analysis is an important step. Connections are made using ssh-based protocols ([](#table_connection_protocols)). SSH is a general communication protocol between Linux and Unix (e.g. Mac) machines that is always available. Sometimes when a remote machine refuses a connection, it is possible that it is not properly configured to be a ssh-server. But your local machine will usually have the 'client' ssh software to connect to any remote machine.

Two methods that are often used to copy files over the ssh-protocol to a remote (Linux/Unix) machine, are: secure copy (`scp`) and `rsync`. The difference between them (in behavior) is that `scp` will just copy everything, and `rsync` will only copy the things that are not yet present. If no files were previously copied, `rsync` will just behave as `scp`. For copying files to other computers, `rsync` is generally the preferred option.


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

When using a remote computer, you will have at least a terminal and in most cases you will not have anything else. Apart from that, there are other restrictions. Not everything is possible on a remote computer that you can do on your own desktop due to system permissions. This is to ensure stability and security of system. Therefore, you need to know how to deal with that by understanding the limitations and the work-arounds. 


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
In these exercises, we will work on the High Performance Computing Cluster from Wageningen University (called Anunna).

``````{exercise} Connect to Anunna
We will access the anunna server which is part of the HPC system here in Wageningen:
```{code-block} bash
ssh yourwurname@login.anunna.wur.nl
```
``````

### Looking Around an HPC System
``````{exercise} Check the current node
You might believe you now logged into a magical supercomputer and you can start doing the heaviest jobs. However, this is not completely true.

**What computer are we logged into?** Use:
```{code-block} bash
hostname
```
**Do you think this is one of the "worker" nodes? Or the "headnode"?**
``````

``````{exercise} Check the specifications of the HPC system
**How much RAM does the "anunna" node have?** Use
```{code-block} bash
free -h
```
**How large are the `/lustre` and `/archive` filesystems (ignore the tmpfs)?** Use:
```{code-block} bash
df -h
```
**How many processors does the node have? **Use:
```{code-block} bash
cat /proc/cpuinfo | grep processor
```
``````

``````{exercise} Look around the file system
**Where is your home directory located (relative to the root directory)?**

**What does your home directory contain? **Include the 'hidden' directories! If a name of a file or directory starts with '`.`', it is hidden in your filebrowser, but also if you do [`ls`](#ls_section). 
```{code-block} bash
ls
```
Use the relevant {term}`option` for the [`ls`](#ls_section) command to make all files visible.
``````

``````{exercise} Check who is active on the HPC system
**Anybody you know around?** See who else is logged into this machine:
```{code-block} bash
who
```
``````

### Nodes on an HPC system
``````{exercise} Amount of nodes on the HPC system
How many nodes does the HPC system have? Use:
```{code-block} bash
sinfo -N
```
**What kind of distinct nodes do you recognize?**
``````

``````{exercise} Inspect a specific node on the HPC system
We typically do not interact directly with the worker nodes but they will perform the tasks that are assigned to them by SLURM. All nodes are generally connected to a shared filesystem (e.g. the `/lustre` filesystem on the HPC sytem).

Now let's explore one of the worker nodes:
```{code-block} bash
sinfo -n node200 -o "%n %c %m"
```
**What is the number of CPUs and memory available?**

Do the same for one of the "fat" nodes. **What do you notice?**
``````

### Working with a Job Scheduler
Here, we will build up to submit a job to slurm to perform a small task on the HPC system. For the task we will write a small script that calculates the GC content of chromosome 3 from yeast (*Saccharomyces cerevisiae*). We will just use one CPU on one node.

``````{exercise} Download the FASTA file
First download the fasta file using following command:
```{code-block} bash
wget http://ftp.ensembl.org/pub/release-104/fasta/saccharomyces_cerevisiae/dna/Saccharomyces_cerevisiae.R64-1-1.dna.chromosome.III.fa.gz -O Sc_chr3.fa.gz
```
Decompress it using:
```{code-block} bash
gunzip Sc_chr3.fa.gz
```
``````

``````{exercise} Create the job script
Next, make a new file called `calc_gc.sh` using the `nano` editor:

```{code-block} bash
:filename: calc_gc.sh
#!/bin/bash
#SBATCH --job-name=calc_GC
#SBATCH --time=0:30:0
#SBATCH --ntasks=1
#SBATCH --mem=2000
#SBATCH --output=output_GC.txt
#SBATCH --error=error_output_GC.txt

time python calc_GC.py Sc_chr3.fa
```
``````

``````{exercise} Create the Python script to calcualate the GC percentage
Now we need to write a python script that takes the chr3 file as input and reports the GC percentage.
```{code-block} bash
nano calc_GC.py
```

Copy the Python script into the `calc_GC.py` file:
```{code-block} python
:filename: calc_GC.py
import sys
def gc_content(dna):
    ...

input_filename = sys.argv[1]
input_file = open(input_filename, 'r') # open the file for reading
line=input_file.readline()[1:-1] # read first header line
sequence = '' ## Empty sequence string

for line in input_file:
    if line[0] != '>':
        sequence += line[:-1]

print(gc_content(sequence))
```
The python script read the `Sc_chr3.fa` file and calculates the GC percentage. 

**Finish the `gc_content()` function in the python script.**

:::{tip}
To finish `gc_content()` function, look at the W2D4 Exercise [GC content](#exc_wf_gc_content_function)
:::


``````

``````{exercise} Submit and monitor a job
We can now submit the `calc_gc.sh` script to calculate the GC percentage using our own python script:
```{code-block} bash
sbatch calc_gc.sh
```
To monitor your job type:
```{code-block} bash
sacct
```
This will show if your job is pending, running, or has completed. To get a real time view of your job you can run `watch`:
```{code-block} bash
watch -n 15 squeue -u username
```
To cancel a job you can use `scancel` together with the job-id, the job-id is shown when you submit the job and also in the first column of the `squeue` output
```{code-block} bash
scancel <job-id>
```

Once your job is finished, **what is the GC content of chr3 of yeast (look in the `output_GC.txt` file)? **

**How much time did it take to calculate this (look in the `error_output_GC.txt`)?**
``````

:::{note} Working responsibly on a shared cluster
Note that working on a shared cluster also means you need to work responsibly, taking into account the other users' needs. Hence, if you need to perform a lot of heavy calculations you might want to divide that over a longer time or you should consult your fellow users of the HPC system.
:::

### Using Software via Modules
``````{exercise} Check what software is available on the HPC system
Many users use similar software to perform computations on their datasets. Therefore, a large collection of software is readily available on the HPC. Run the following command to get a list of the software that is available:
```{code-block} bash
module load 2023
module avail
```
``````

:::{note} Many of the standard bioinformatics utilities (i.e. calculating GC content of a fasta file) are also available in existing software utilities. 
:::


``````{exercise} Use an existing module 
We will use one of the existing software packages to calculate the GC content of the `Sc_chr3.fa` file again. Load the module `seqtk`:
```{code-block} bash
module load seqtk
```
`seqtk` is a fast and lightweight tool for processing sequences in the FASTA or FASTQ format. If you want to check where a particular software is stored you can use the `which` command:
```{code-block} bash
which seqtk
```
Moreover, you can list the modules you have loaded with:
```{code-block} bash
module list
```

Now we can use the program `seqtk` to calculate the GC content of the same fasta file. 

Modify the slurm script and use `seqtk` instead of your own python script to calculate GC:
```{code-block} bash
:filename: calc_gc.sh
...
time seqtk comp Sc_chr3.fa
```
You will notice that `seqtk` does not report a GC percentage directly. Instead, it counts the number of bases for every nucleotide (you will find the header when typing: `seqtk comp` without the fasta input).


**Compare the runtime with the previous analysis, what do you notice?**
``````

### Transferring Files
Make sure that during these exercises you keep (at least) one terminal open in Anunna (your home dir), and one in your server (in the W5D3 working dir).

``````{exercise} Download data onto [[SERVER_NAME]]
First download the data for this day from Brightspace. 

Unzip the archive to [[SERVER_NAME]], and make the directory '`W5D3`' in your working directory. 

Make sure you understand which files and folders it contains, notably what is in the '`dna_files`' directory.
``````

``````{exercise} Use secure copy to copy the data to a HPC system
Secure copy `scp` works similarly to the [`cp`](#cp_section) command you encountered in the first week of the course, on the first day we started working on the command line. 

:::{caution} In the next line of code the `:` is important to include.
This means that you are copying this to your home directory. What happens when you forget this (you can try it, if you do check the home directory on Anunna *#! missing in the exc pdf assuming anunna*)?
:::

```{code-block} bash
scp -r dna_files yourname@login.anunna.wur.nl:
```
**What does the `-r` flag mean?** Remember that the behavior is very similar to [`cp`](#cp_section), with the difference that `scp` uses the SSH protocol and can copy "remotely".

Observe the change in your home directory in Anunna.

In Annuna, remove the fasta files using:
```{code-block} bash
rm -rf dna_files
```
``````

``````{exercise} Use rsync to copy the data do a HPC system
Now we will copy the `dna_file` folder and contents again, but this time using the `rsync` command:

```{code-block} bash
rsync -av dna_files yourname@login.anunna.wur.nl:
```

**What do the `-a` and `-v` flag mean?** (use `man rsync`, for instance in a third open terminal, to find out). 
```{code-block} bash
man rsync
```

Observe the changes in Anunna.

Change one of the fasta files (say `dna99.fa`) on your own machine, for instance by changing one base. 

Then use the exact same `rsync` command again (just use the {kbd}`↑` key!). 

**What happens?**
``````


### Data Integrity : `checksums`

``````{exercise} 
```{code-block} bash

```

``````