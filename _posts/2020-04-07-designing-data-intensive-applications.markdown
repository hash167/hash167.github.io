---
layout: post
title:  "Designing Data Intensive Applications"
date:   2020-04-07 18:54:00 -0700
categories: book
---

Updating as I read the book

## Chapter 1 - Reliable, Scalable and Maintaiable applications

### Latency and Response time

The `response time` is what the client sees which includes service time, network delays and queueing delays

`Latency` is how long the request is waiting to be serviced.

### p95, p99 and p999 percentile of requests

Customers with slow latency are the ones most likely to have more data to compute. Thus its important to look at these outliers and not just the average customer. In Amazon's case, an outlier could mean that a customer has more orders in his shopping cart.

High percentiles of response times are also known as tail latencies

An apm like New Relic can give you these metrics.
