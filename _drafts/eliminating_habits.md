---
layout:     post
title:      "Eli"
date:       2020-4-3 13:28:00
author:     "bearcat"
---

When using [head | tail], if you have a list that has one element, and you do tail, you
will get an empty list returned. But what if you call [head |tail] = tail on your empty list?
You will see this error: ** (MatchError) no match of right hand side value: []. So this means that the tail of the final element of a list is an empty list. But when tail is invoked on an empty list, the pattern doesn't match, which then raises an error. 

In order to address this issue, we need a function clause that matches that pattern