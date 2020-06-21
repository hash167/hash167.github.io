---
layout: post
title:  "Designing Data Intensive Applications"
date:   2020-04-07 18:54:00 -0700
categories: book
---

Updating as I read the book

## Chapter 1 - Reliable, Scalable and Maintainable applications

### Latency and Response time

The `response time` is what the client sees which includes service time, network delays and queueing delays

`Latency` is how long the request is waiting to be serviced.

### p95, p99 and p999 percentile of requests

Customers with slow latency are the ones most likely to have more data to compute. Thus its important to look at these outliers and not just the average customer. In Amazon's case, an outlier could mean that a customer has more orders in his shopping cart.

High percentiles of response times are also known as tail latencies

An apm like New Relic can give you these metrics.


### Chapter 2

The need for NoSQL

- A need for greater scalability than relational databases for large data sets and high write throughput
- Preference for free and open source software
- Specialized query operations - schema flexibility and data locality
- https://blog.couchbase.com/nosql-adoption-survey-surprises/

Document stores follow the hierarchal model storing nested records within their parent record whereas relational stores follow the relational model where a table is represented as a list of tuples. You can select rows by setting one of the columns as index and matching on it.

However, when it comes to representing many-to-one and many-to-many relationships, relational and document databases are not fundamentally different: in both cases, the related item is referenced by a unique identifier, which is called a foreign key in the relational model and a document reference in the document model. That identifier is resolved at read time by using a join or follow-up queries.

Three main models

- Document: One to one, One to many. Flexible schema, high data locality. General purpose, High write throughput
- Relational: One to one, one to many, many to many. Non flexible, relational schema, General purpose
- Graph: Many to many. Flexible graph schema with declarative syntax. Can be general purpose with query speeds faster than Relational databases but lesser industry knowledge
