---
layout:     post
title:      "Project based learning to learn Elixir: Part 2"
date:       2020-4-3 13:28:00
author:     "bobby"
---

## Phoenix

Phoenix is an Elixir web framework. You can think of it as the Elixir equivalent to Ruby on Rails. For our pointing poker application, instead of having our game logic and web logic all in one application, we decided to separate these two concerns which the Phoenix portion of our application to act as the client of the Pointing Poker application. So our Phoenix application well route and serve assets whereas the Pointing Poker application will execute the logic.

First, we create a new Phoenix application. Directions of how to create a new Phoenix application can be found here: TODO. Then we open our mix.exs file and find a list of dependences under the deps function. The line contain {:bingo, path: "../bingo"} sets the Pointing Poker application as a dependency of the Phoenix app. What is great about using this as a dependency is that any change that occurs in the Pointing Poker app will be automatically recompiled by the Phoenix application. Alternatively, we could put the Pointing Poker app as a dependency in the hex package manager, or if its in a public Git repository, we can use the git link and set that as a dependency, and finally, we can set Pointing Poker as a depedency as part of an "umbrella project."

By making PointPoker a depedency on the Phoenix app, all of the modules are available inside the Phoenix application and the Phoenix app automatically starts the Pointing Poker application.