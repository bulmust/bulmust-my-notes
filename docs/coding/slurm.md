---
layout: default
nav_order: 5
title: slurm
permalink: /coding/slurm
parent: coding
#grand_parent: 
#has_children: true
has_toc: True
#tags: []
#categories: []
math: true
mermaid: true
last_modified_date: 2023-11-12 +0300
---

# slurm
{: .no_toc }

This is slurm notes.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Commands

| Definition | Command |
|:---:|:---:|
| List all jobs | `squeue -u <username>` |
| Show available modules | `module avail` |
| Load a module | `module load <module_name>` |
| Show all jobs in the queue | `squeue` |
| Launch a job | `sbatch <job.sh>` |
| Cancel a job | `scancel <job_id>` |