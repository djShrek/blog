---
layout:     post
title:      "Elixir Streams, ParallelStreams, Flow and GenStage"
date:       2022-02-25 20:30:00
author:     "bearcats"
---

## What are Streams and what are they used for?

Lets say you are doing some wordcmmm processing on a file and you need to iterate on every word and on
every line in the file. If you use something like File.read("big_file.txt") and then pipe the file
into something like Enum.map(&String.split(&1)) and then want to do a count of how many times each
word is found in the document by doing a Enum.reduce(), this will first process each line and word
until you have one giant list of words before anything is reduced.
With streams, the Elixir enumerable is takes each item and processes it line by line instead of all at 
once.
Streams are an Elixir enumerable that are lazily loaded. What are the benefits of something being lazy?
Instead of executing a mapping on every item of a list, the stream will take one item at a time
and process it. 