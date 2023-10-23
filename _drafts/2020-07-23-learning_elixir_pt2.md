---
layout:     post
title:      "Learning Elixir Pt. 1"
date:       2020-7-22 13:28:00
author:     "bobby"
tags:       programming elixir
---

Elixir is a functional programming language. If you come from an object-oriented programming language, you will have to change the way you think about programming. For example, with OOP languages, you usually create objects and call methods on those objects to operate on them. With functional programming languages, you use functions to transform the data. 

For example, lets say we have a Alchemist module. 

```elixir
  defmodule Alchemist do

  end
```

We want to be able to combine some functions to create different types of Potion.
 
```elixir
  defmodule Alchemist do
    def conjure_blank_potion do
      ""
    end

    def health_potion(potion) do
      "Gain 100 Health Points"
    end

    def mana_potion(potion) do
      "Gain 100 Mana Points"
    end

    def dragon_potion(potion) do
      "Turn into dragon, gain 1000 health Points"
    end

    def invisibility_potion(potion) do
      "Turn invisible, gain 100% evasion"
    end
  end
```

