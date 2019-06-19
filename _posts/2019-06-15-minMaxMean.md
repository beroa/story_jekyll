---
layout: post
title: "Min Max and Mean with Python's Reduce"
image: "/images/image_2"
date: 2019-06-15
categories: code
---

Here is how min max and mean functions look in python using loops:

```python
def myMin(inp):
    if (len(inp) == 0):
        return
    cur = inp[0]
    for i in inp:
        if i < cur:
            cur = i
    return cur

def myMax(inp):
    if (len(inp) == 0):
        return
    cur = inp[0]
    for i in inp:
        if i > cur:
            cur = i
    return cur

def myMean(inp):
    if (len(inp) == 0):
        return
    accum = 0
    for i in inp:
        accum += i
    return accum / len(inp)
````

These are perfect opportunities to show how the **reduce** function in python functools.

Here is how to get the min using reduce:

```python
import functools

def myMin(inp):
    if (len(inp) == 0):
        return
    return functools.reduce((lambda x, y: x if (x < y) else y ), inp)
```

The reduce function will reduce the list into one value, following the logic given in the specified function, in this case a oneline lambda function.
The x and y arguments are the current and next items in the list as the reduce function iterates over it.

*i am confused why we use the same arguments that are passed in as our return. it's nice that the above code isn't modifying the list, in my mind it should.*

It is kind of interesting that the reduce function will cause an error when given an empty list, but will run fine if it is given a list of length one even though the lambda function references two items.

anyway, the max function looks almost, but not entirely like that.

the mean function is kind of interesting because i have to now go figure out what it will look like, brb

here it is

```python
def mySum(inp):
    if (len(inp) == 0):
        return
    return functools.reduce((lambda x, y : x + y), inp)

def myMean(inp):
    if (len(inp) == 0):
        return
    return mySum(inp) / len(inp)
```

i think the best way to do that is with a **sum** helper function.

ok thats how you do it.

thanks for reading. am i a blogger now ?