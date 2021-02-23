---
layout:     post
title:      "Monitoring and Alerting Notes Pt. 1"
date:       2020-7-29 10:00:00
author:     "bearcat"
tags:       monitoring
---

# Determining Causality 

When monitoring an application using an APM, there will be times where you will
observe abberant events in the system. In these times, there are three ways to 
determine causality:

1. Find a correlation - First, identify the undesired symptoms. Using timeseries data, look at what metrics or events stray away from the baseline and determine if these factors are related. Gather and juxtapose timeseries from other system metrics that display similar abnormality. Pay attention to whether they are on the same stack (low level vs application level components etc.)
2. Establish a direction - Correlation does not imply causation. Which way are the abberant events coming from? Knowing that the problem comes either downstream or upstream, which anomalous timeseries recorded abnormal data first? This is where granular timeseries data helps as temporal precedence is in a matter of seconds. If you observe slow response times from your server, is it because your server is getting hit with a large number of requests coming from external sources or is it because your CPU can't handle that many requests? 
3. Rule out confounding factors - Sometimes you will observe that many if not all your metrics are going off the walls at once. Certain confounding factors can be coincidental and unrelated. In times like these, try to switch off or restart the suspected faulty components separately in order to test your hypothesis with all other things being equal.

# Capturing Daily Cycle, Trends, and Seasonal Changes

When capturing resource utilization metrics on a daily basis, you won't need more than 4 weeks worth of data to maintain a baseline. This is because baselines always change. Your system may get more users or you may upgrade your hardware for more resources. Four weeks of daily metrics should give you a good idea of what your baseline is and what your system can handle.

However, what is more important is to record metrics that represent usage patterns that encapsulate a more universal type of information that can be retained for analysis on trends and seasonality. You need to track and measure demand progression in order to properly capacity plan. If you don't properly plan for capacity, you won't be able to know when you need to scale out your resources until it is too late. The demand for the service of your system is dictated by its overall effectiveness and to a lesser extent by specific technical conditions.

Identify metrics that objectively reflect usage. A metric that can identify usage is "traffic." Being able to observe if your system is encountering more traffic will give you awareness around how much your system is being utilized. This can help you to identify trends in usage in your system as well as seasonal factors.

Trends are changes in your baseline that affected by seasonal or cyclic factors. There can be many reasons why trends occur, but they are considered trends if they are not seasonal. One way to spot trends is to gather analyze your traffic metrics on a weekly basis. Any changes in demand will give you insight to any trends that may be occuring.

Seasonal changes are self-explanatory. If you own an e-commerce website, traffic may be slower during the first quarter of the year vs the holiday season. 
