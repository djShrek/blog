---
layout:     post
title:      "Learning Docker Pt. 1"
date:       2021-11-13 20:30:00
author:     "bobby"
---

 I watched a video that advocated for using Docker to develop locally so that you wouldn't have to worry about having any issues or conflicts in your local environment. Here is a list of things I learned:

After installing Docker, you need can pick a Docker image from [Docker Hub]("https://hub.docker.com/search?q=elixir&type=image") and use that as a starting point for your project. 

## But why do we need Docker?

If you pulled down an Elixir project from Github, the project has its own environment needs.
For example, maybe the project was built using Elixir 1.7 but you have Elixir 2.2 on your machine. Now you
need to install a different version of Elixir to get it to run, but a new problem arises because you now need to manage how you use these different versions of Elixir, so now you need a tool to manange different runtime versions like [asdf]("http://asdf-vm.com/"). At this point, you have to download two different things just to work get the project up and running. Lets say you are successful at getting the project to run on your machine after downloading "all the things," but you had to do a bunch of miscellaneous configuration in the system environment (symlinking things, changing environment variables, etc etc.). But lets say you have _another_ project that only can run in Elixir 1.9 but not 2.X+, so you download this project and get it running, but there are conflicts with your system environment and it is just one big mess now. The system requirements for each project come into conflict with one another and you are seeing errors in the command line and now you want to pull all your hair out. This is not good, you wish the system environments and needs could be somehow isolated from one another.

A better solution is to use a Docker image that contains all the information and dependencies you need to run your projects isolated from one another.

### What is a docker image?

### What is a docker container?

### How to create a Docker container

I want to create a development container with Elixir. To do so, I need to do:

```
docker create -it --volume `pwd`:/pomodoro -w /pomodoro --name pomodoro_container elixir
```
If I now run:

```
docker ps -a
```
I should observe my new container that I named pomodoro_container. The -i flag stands for interactive and -t flag stands for a terminal. When developing locally using Docker, you pretty much always want to use these two flags. Volumes in Docker basically represent the workspace directory that you want to attach and associate Docker with. 

One way to make this more repeatable for other developers is to capture all of this in script. 
Since I want to create and start a container and open a shell for it when I run it, it would be easier
if it was all done in a script. This can be done using the docker-compose tool and will be the topic of my next blog post