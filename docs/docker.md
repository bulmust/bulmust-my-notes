---
layout: default
nav_order: 4
title: docker
permalink: /docker
#parent: 
#grand_parent: 
has_children: true
has_toc: True
#tags: []
#categories: []
math: true
mermaid: true
last_modified_date: 2023-11-12 +0300
---

# docker
{: .no_toc }

This is docker notes.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Commands

| Definition | Command |
|:---:|:---:|
| List all containers | `docker ps -a` |
| Copy file from container to host | `docker cp <containerId>:/file/path/within/container /host/path/target` |