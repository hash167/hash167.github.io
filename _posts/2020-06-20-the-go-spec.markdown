---
layout: posts
title:  "The Go Spec"
date:   2020-06-20 16:00:00 -0700
categories: go
---

## Go Spec

The Go compiler can compile the Go source go with different go specs. Fo example, if you have installed go 1.14, you can compile your source with `Go spec 1.13`.

### The rules for which version of the Go spec used during compilation appear to be

1. If your source code is stored within the `GOPATH` (or you have disabled modules with `GO111MODULE=off`) then the version of the Go spec used to compile matches the version of the compiler you are using. ie if you have go 1.13 installed then the go spec used will be 1.13
1. If your source code is outside the `GOPATH`(or `GO111MODULE=on`), then the go tool will take the version from the `go.mod` file
1. If no `go.mod` file is provided, then same as point 1
1. If you are in module mode(see point 2) and no version is specified in the `go.mod` file, then `go 1.13` is used by default

The last point is interesting.
