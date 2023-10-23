---
layout:     post
title:      "Learning Elixir Pt. 1"
date:       2020-7-22 13:28:00
author:     "bobby"
tags:       programming elixir
---

# Hello world! in Elixir? Nah, gimme the health and mana points!

---

Elixir is a functional, concurrent programming language. Unlike Ruby, which is object-oriented, the state of Elixir _things_ are immutable. 

In Elixir, there are things called modules. The general structure of the module is as follows:

```elixir
  defmodule Potion do

  end
```

The name of Elixir modules are camel-cased while the functions are snake-cased (lower cased with underscores).

```elixir
  defmodule Potion do
    def health_points do
      100
    end
  end
```

Here I want to run the function ```health_points```, so I would do something like this in my file:

```elixir
  defmodule Potion do
    def health_points do
      "100 HP left"
    end

    def mana_points do
      "200 MP left"
    end
  end

  IO.puts Potion.health_points
  IO.puts Potion.mana_points
```
The IO module is a part of the Elixir standard library and the #puts function prints whatever string is returned from the function.

I can run the code in the terminal doing ```elixir potion.ex```. This will compile the file to byte code and run it in the Erlang virtual machine.

After running the code, I will see the response of "100 HP left" and "200 MP left" respectively. 

Elixir also comes built in with an Elixir interactive shell called IEX. If you are familiar with Ruby, it is similar to IRB. In IEX, you can run commands that will be interpreted and executed at runtime. You can also run IEX along with compiling your file into memory and loading it in the current IEX session. 

Running ```IEX potion.ex``` will immediately return "100 HP left" and "200 MP left." The file gets immediately loaded and any code outside of the module is interpreted. If I call the health_points function on my potion module again, the function will run and return "100 HP left" as the potion.ex file is still loaded in memory. 

A short cut to all of this is to simply load the entire context of the directory to iex. You can do this by running this command in the terminal: ```iex -S mix``` , which will load your all of the files in the current directory into the interactive shell. From here, I can run any functions from the potion.ex file without having to explicitly load it.

Becoming 1% better every day!