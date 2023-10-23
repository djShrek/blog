---
layout:     post
title:      "Behaviours and Protocols"
date:       2023-07-01 22:00:00
author:     "bobby"
tags:       "til behaviours protocols"
---

## INTRO

Sometimes you want different parts of your code to follow a common API. Elixir behaviours allow you to define a set of functions
that need to be implemented by a module. This "ensures" that any module that adopts that behaviour will implement all of the functions of that behaviour.

### BEHAVIOURS

Behaviours are normal modules that implement the @callback typespec.

### EXAMPLES

