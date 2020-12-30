---
layout: post
title:  "Abstract classes using Metaclasses"
date:   2020-12-28 17:00:00 -0700
categories: python
---

### Type and Class

In python3 all classes are new style classes, thus it is reasonable to refer to an objects type and its class interchangably

```python

class Foo:
    pass

>>> type(Foo)
<class 'type'>

```

Type is a metaclass of which classes are instances

* `Foo` is an instance of metaclass `type`
* `type` is an instance of `type` as well

### Type Metaclass

A `type` metaclass is initialized with 3 arguments

* `name`: name of the class (__name__ attribute)
* `bases`: a tuple of classnames that the class inherits from
* `namespace`: a dictionary contianing definitions of the class body (__dict__ attribute of the class)

### Creating an abstract class manually with Metaclasses

To understand metaclasses, we create an interface or abstract class implementation. Use `from abc import ABC, abstractmethod` when implementing something at work. 

```python

# test.py

# Decorator to add attribute to function
def abstract_func(func):
    func.__isabstract__ = True
    return func


# This is the metaclass inheriting from `type`
class Interface(type):
    def __init__(self, name, bases, namespace):
        print(f"Init method initialized from {self}")
        class_methods = getattr(self, 'all_methods')
        for base in bases:
            required_methods = getattr(base, 'abstract_methods')
            for method in required_methods:
                if method not in class_methods:
                    msg = f"""Can't create abstract class {name}!
{name} must implement abstract method {method} of class {base}!"""
                    raise TypeError(msg)

    def __new__(cls, name, bases, namespace):
        namespace['abstract_methods'] = Interface._get_abstract_methods(namespace)
        namespace['all_methods'] = Interface._get_all_methods(namespace)
        cls = super().__new__(cls, name, bases, namespace)
        return cls
    
    def _get_abstract_methods(namespace):
        ret = []
        for name, val in namespace.items():
            if callable(val) and getattr(val, '__isabstract__', False):
                ret.append(name)
        return ret


    def _get_all_methods(namespace):
        ret = []
        for name, val in namespace.items():
            if callable(val):
                ret.append(name)
        return ret
    

# the __calls__() function calls the __new__() and __init__() methods of the metaclass
class NetworkInterface(metaclass=Interface):

    @abstract_func
    def connect(self):
        pass

    @abstract_func
    def transfer(self):
        pass

# The object of this class will not be created 
# because of missing abstract method
class TestNetwork(NetworkInterface):
    def __init__(self):
        print(f"Init method initialized from {self}")

    def connect(self):
        pass
    
    # def transfer(self):
    #     pass


c = TestNetwork()
>>> TypeError: Can't create abstract class TestNetwork!
TestNetwork must implement abstract method transfer of class <class '__main__.NetworkInterface'>!

After uncommenting the method

>>> python3 test.py
Init method initialized from <class '__main__.NetworkInterface'>
Init method initialized from <class '__main__.TestNetwork'>
Init method called from <__main__.TestNetwork object at 0x7fc5e7659350>

```

When we initialize `TestNetwork`, the following happens

* The interface init method is called twice. Once when creating the `NetworkInterface` and  `TestNetwork` class from the metaclass blueprint.
* In the `Interface` init method, we iterate over the list of abstract methods in the parent class and make sure each one is present in the current class.
* If we don't find a method in the class with the same name, we raise an exception
