---
layout: default
nav_order: 2
title: julia
permalink: coding/julia
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

# julia
{: .no_toc }

This is julia notes.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Installing Julia

Download Julia from [here](https://julialang.org/downloads/){target="_blank"}.

After downloading, extract the file and move it to `/opt` directory.

```sh
sudo tar zxvf julia-<version>-linux-x86_64.tar.gz -C /opt/
```

Create a symbolic link to `/usr/local/bin` directory.

```sh
sudo ln -s /opt/julia-<version>/bin/julia /usr/local/bin/julia
```

## Running Julia

```sh
julia
```

## Installing Packages

### Jupyter Kernel

Run Julia and enter the following commands.

```julia
using Pkg
Pkg.add("IJulia")
```

```sh
