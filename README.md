nvtxpy
======

NVTX offers a way to insert markers and ranges into Nvidia's CUDA debugging information. This information can be used to:

 * Identify all the kernels launched in a loop nest
 * Identify all the kernels launched by a class
 * Segment a program into phases: setup, running, cleanup

Additionally, these can be used to start and stop Nvidia's profilers so that profiling can be focused on a particular subset of an otherwise complex program.

This Python package offers an easy way to use these features from within Python with a variety of packages, including [ArrayFire](https://github.com/arrayfire/arrayfire).



Installation
============

Install using

    python setup.py install #Global

The `--user` flag can be used to install only to the user's current directory.



Usage
============

There are several ways to use the package. Ranges can be arbitrarily entered and ended using:


Simple function calls
---------------------

```python
profile_range_push(message, color, payload, category)
#Your code
profile_range_pop()
```


Contexts
---------------------

A simple way of doing the above is with a context which automagically pushes and pops a range:

```python
with nvtxpy.profile_range(name, color, payload, category) as value:
  #Code
```

This can be useful inside of a loop:

```python
for i in range(10):
  with nvtxpy.profile_range(name, color, payload, category) as value:
    #Code
```

`nvtxpy.profile_range` collects timing statistics about the number of times each context was entered and the total time spent in the contexts. To avoidcollecting these statistics, use:

```python
with nvtxpy.profile_range_nvtx_only(name, color, payload, category) as value:
  #Code
```


Function decorators
-------------------

Sometimes you want to mark a function or method. But there's a problem: any measurement actually within the function excludes time spent on the return or building default arguments. Function decorators come to the rescue!

```python
@nvtxpy.profiled(name, color, payload, category)
def myfunc(arg1, arg2):
  #code
```



Statistics
----------

You can get run counts and total runtime for eaceh profiled range using:

    nvtxpy.getstats()



Arguments
---------

What are those arguments about?

 * **name**: A string that shows up in your profiler to let you know what the range is about
 * **color**: A hex number starting with `0xff`. Green, for instance, is `00xff00ff00`. There are several predefined colors accessible with, e.g., `nvtxpy.colors.green`. They are: `red`, `green`, `blue`, `yellow`, `magenta`, `cyan`, `white`, `black`.
 * **payload**: TODO
 * **category**: TODO



TODO
----

    profile_mark(message, color=None, payload=None, category=None):
