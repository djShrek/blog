---
layout:     post
title:      "Project based learning to learn Elixir: Part 1"
date:       2020-4-3 13:28:00
author:     "bearcat"
---

- App has a separate process for retrieving and storing data (?)

## Supervisors

In our mix.iexs file, it has meta data about the project and its dependencies. But more importantly it has information on which module to invoke to start the application when the callback is executed. By convention, the #start function will be called on the module that is passed to mod with a list of empty arguments.

In our application, we have a PointingPoke module with a #start function. Inside the function, we setup our supervision tree by calling Supervisor.start_link(children, opts). The whole point of start_link function is to start our top level supervisor which is going to grow the whole supervision tree. For options, we use the "one_for_one" strategy, which means if a child process terminates, only that process will be restarted. The name of the supervisor is PointPoker.GameSupervisor. Any child of the supervisor by convention will have its start_link function invoked when the supervisor is initialized.

Our PointingPoker.GameSupervisor module inherits from DynamicSupervisor. With it, it inherits the start_link method, which simply called DynamicSupervisor.start_link with a tuple with its name as a callback, :ok atom, and a name we are giving to the DynamicSupervisor, which is simply the module name. Start_link triggers the #init function, meaning that both the start_link and init functions are invoked when the application starts to start this one DynamicSupervisor process. When the GameSupervisor calls start_game function, it calls DynamicSupervisor with #start_child, we pass in the name of the supervisor process, in this game PointingPoker.GameSupervisor along with a map of child specifications to start the child. This will start a new PointingPoker.Game process, which can be observed in the :observer.start GUI.

Passing in the child specs with a restart option of :transient means that the child will only restart if it crashes. The default restart option is :permanent, but we don't want that to happen because it will attempt to restart processes if it timesout.

Notice we also have a stop_game function just in case if we ever need to stop a game. To do that, we just called DynamicSupervisor.terminate_child with the module name and child_pid.

