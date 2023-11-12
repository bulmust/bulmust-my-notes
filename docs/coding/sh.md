---
layout: default
nav_order: 1
title: sh
permalink: coding/sh
parent: coding
#grand_parent: 
#has_children: true
has_toc: True
#date: 2023-11-12 08:44:07 +0300
#tags: []
#categories: []
math: true
mermaid: true
---

TOC
{:toc}

---



## Find a Folder and a File

Find a folder in current directory:

```sh
find . -type d -name <folder>
```

Find a file in current directory:

```sh
find . -type f -name <file>
```

## Create Linux User

Add an user and change its password:

```sh
sudo adduser -m <username>
sudo passwd <username>
```

## Change roots bashrc

Root's bashrc is located in `/root/.bashrc`.

## Run Linux Commands In Background

If you would like to run a command in the background, all you have to do is add an ampersand (&) at the end of the command. For example, if you would like to run the `top` command in the background, you would run the following:

```sh
top &
```

This command terminates when you log out from the system. If you want to keep the command running even after you log out, you can use the `nohup` command. For example, if you would like to run the `top` command in the background and keep it running even after you log out, you would run the following:

```sh
`nohup <code> &`
```