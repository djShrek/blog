---
layout:     post
title:      "Monitoring and Alerting Pt. 1"
date:       2020-07-24 2:35:00
author:     "bearcat"
---

Determining causality when your application is experiencing emergent system events requires you to do 3 things:

1. Find a correlation - Look at timeseries metrics to see if there is a correlation among them. Find anything abnormal and try to correlate them to system events
2. Establish a direction - 
3. Rule out confounding errors - turn on and off certain parts of the system to see if there is an issue