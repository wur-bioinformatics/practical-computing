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

### File systems

### Software

### Performance and Capacity



## Exercises

### Command Line Strategies for Using Remote Computers

### Data Transfer – Data Integrity (checksums)