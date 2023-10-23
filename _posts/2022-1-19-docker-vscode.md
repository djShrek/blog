---
layout:     post
title:      "Using Docker with vscode as IDE"
date:       2021-11-13 20:30:00
author:     "bearcat"
---

## INTRO

Historically I've always programmed on a Mac due to the fact that the start-ups I worked for preferred using tools
that were more "friendly" to a Unix-ish system. But after I built my new gaming PC, I decided that I also wanted to use the comp
for developing my side projects. In the past, using Ruby on windows required installing additional software like Cygwin and configuring
it was a hassle. Because of this, I thought this would be a good opportunity to use Docker so that I could run Ruby (or any programming language)
apps on my new Windows PC.

## USING VSCODE AS AN IDE WITH DOCKER

There is an extension called Visual Studio Code Remote - Containers that lets you use a Docker container as a full-featured development environment. Per the docs

```
It allows you to open any folder inside (or mounted into) a container and take advantage of VS Code's full feature set.
```

All you need is a devcontainer.json file in your project which tells VS Code how to create the development container with a well-defined tool and runtime stack. 

You can also use a pre-defined devcontainer configuration file (eithe created by Docker or by the Docker community) to help you get started. For example, you can use the pre-defined configuration file for a new Ruby/Rails/Postgres project and the configuration file will install Ruby, Rails, necessary Gems, and Postgres to the Docker container. From there, you can do something like 

```
rails new blog
```

and Rails will generate a new project. The files created in the container will also exist on your local machine, so you can edit them locally while working in the container.

Once that is setup, you can quickly start working on your projects regardless of original OS
