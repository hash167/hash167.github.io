---
layout: posts
title:  "Python decorator common use cases"
date:   2020-04-04 15:54:35 -0700
categories: python decorator
---

- Timing functions. Almost always the first example on StackOverflow. (You can always use a Context Manager for these too, writing them is a good way to learn those and their `__enter__` and `__exit__` dunders.)
- Retrying functions. Bonus points for having longer times between tries per try.
- Setting a maximum time for a function to finish executing, if the function is amenable to it (e.g. it runs in a loop)
- Logging functions. There are tons of different types of these (and some PyPI packages that are based on this), because there are tons of different use cases for logging. They generally require a decorator factory or class, because they require parameters (such as the logger instance).
- Simple debugging, sending a function’s inputs and outputs to a log or just stdout
Validating function inputs. Python is EAFP rather than LBYL, but it’s still useful to validate inputs sometimes depending on use case. I’ve written classes that use the same decorator with a bunch of different methods. It’s also handy to CHANGE inputs if they’re in the wrong format, e.g. if the user forgets to start a url with `http://`, you can add it.
- Validating function outputs, for example setting a max/min.
- Waiting/rate-limiting. Don’t want that web service to ban you for pinging them too frequently!
- Caching/memoization. If you’ve got an pure/idempotent (i.e. a functional programming pagradigm functions) that’s also expensive (big O/long running time) that you run several times, sometimes with the same inputs, why not cache the results so you don’t have to recalculate from scratch? Eg: `functools.lru_cache`.
- Gracefully handling database transactions, e.g. rolling back if there’s an Exception (although many DB-API packages come with their own ways to set this up)
- Synchronization, i.e. acquiring and releasing locks in multithreading/multiprocessing applications
- Authentication (this is what some web framework decorators do, i.e. make sure a user is logged in before they are allowed to do some task/access some resource)
