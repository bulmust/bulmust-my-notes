---
layout: default
nav_order: 3
title: python
permalink: /coding/python
parent: coding
#grand_parent: 
#has_children: true
has_toc: True
#tags: []
#categories: []
math: true
mermaid: true
last_modified_date: 2023-11-12 +0300
---

# python
{: .no_toc }

This is python notes.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Matplotlib

### Make scientific notation the default

Following command makes scientific notation the default.

```python
plt.ticklabel_format(axis="y", style="sci", scilimits=(0,0), useMathText=True)
```

### One graph with two y-axis

Following command draws two plots in one graph with two y-axis.

```python
fig, ax1 = plt.subplots()

ax2 = ax1.twinx()
ax1.plot(x, y1, 'g-')
ax2.plot(x, y2, 'b-')

ax1.set_xlabel('X data')
ax1.set_ylabel('Y1 data', color='g')
ax2.set_ylabel('Y2 data', color='b')
```

### Horizontal line

Following command draws a horizontal line in a plot.

```python
plt.axhline(y=0, color='r', linestyle='-')
```

### Removing white space around a saved image

Following command removes the white space around a saved image [[1]].

```python
import matplotlib.pyplot as plt
plt.savefig('foo.png', bbox_inches='tight')
```

## Numpy

### Set Numpy print precision

If we want to set the precision of numpy print, we can use the following command:

```python
np.set_printoptions(precision=3)
```

### Find the index of closest value to a given value

Suppose that we have an array, and we would like to finde the index of the closest value to a given value. We can use the following command:

```python
a = np.array([1, 3, 5, 7, 9])
value = 3.5
index_min = (np.abs(a - value)).argmin()
```

## Built-in Functions and Methods

### Strings

#### Find a character (Method)

Following command find "." in the string and return the index of the **first** occurrence.

```python
x = "he.llo."
x.find(".")
```

#### Delete a character (.replace)

Following command find "." in the string and delete it.

```python
x = "he.llo."
x = x.replace(".","")
```

### Check If condition  (assert)

Assert is used to check if a condition is true. If the condition is false, it raises an AssertionError.

```python
x = "hello"
# if condition returns True, then nothing happens:
assert x == "hello"
#if condition returns False, AssertionError is raised:
assert x == "goodbye"
```

[1]: https://stackoverflow.com/questions/11837979/