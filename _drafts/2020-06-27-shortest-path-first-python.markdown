---
layout: post
title:  "Shortest path first in python"
date:   2020-06-20 16:00:00 -0700
categories: python
---

## Find the shortest path to destination in a 2-D map

- Algorithm is a variant of [ Dijkstra’s algorithm]( Dijkstra’s algorithm)

3 data structures

- tentative: map of a tentative path from a origin to a position. The path is called tentative because it is a shortest known path but it could be improved upon

- certain: it is a set of points which tentative map is certain to be the shortest possible path

- candidate: is a heap of position that have a path. The sorting key of the heap is the length of the path

Algorithm

1. 