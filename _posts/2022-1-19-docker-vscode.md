---
layout:     post
title:      "Using Docker with vscode as IDE"
date:       2021-11-13 20:30:00
author:     "bearcat"
---

How to open a file directory in a remote container with vscode:

1. Press F1 in vscode and select Remote Container: Open Folder in container
2. Then choose the directory in which you want mount to Docker
3. Once this is done, vscode will ask you to select a predefined container definition. These containers will contain any tools or libraries you need to get started on your project. If any are missing, you can always add more later.
4. Once step 3 is done, you will remote access to the docker container with the environment setup.

## Developing inside a Container

The Visual Studio code Remote - Containers extention lets you use a Docker container as a full-featured development environment.

## What is a docker container?