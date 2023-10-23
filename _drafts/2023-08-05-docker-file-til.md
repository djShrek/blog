---
layout:     post
title:      "Docker File TIL"
date:       2023-08-05 22:00:00
author:     "bearcat"
tags:       "til docker dockerfile"
---

## WHY DOCKER IS GREAT

Docker is great because all you need is a single configured DockerFile with params filled out to your needs and with the execution of one command
have it generate all the dependencies you need for your next project.

I just take an example DockerFile that is setup for me by the VSCode docker extension and swap the Elixir/Phoenix versions to the most recent
stable releases. Then to get a brand new Phoenix project rolling, I just do "mix phx.new new_project" and bam, everything is setup in its own
dev container in matter of minutes (if not seconds).