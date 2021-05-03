---
layout: post
title:  "Array Dimensions: IDL versus Python"
date:   2021-05-01 4:15
categories: [research notes, coding, python, IDL]
published: False
---

# Difference between arrays in Python and IDL

This is evident when I display a HMI image, and the image is transposed when comparing it on IDL and Python.

## Python:

- arrays are 0 index based
- access columns using axis = 0
- access rows using axis = 1

A fits file read into Python follows this format: 

(z-dimension, rows, columns) or (t, y, x)

## IDL

- arrays are 0 index based

A fits file created and read into IDL follows this format:

(column, row, z-dimension) or (x, y, t)

## Solution

When reading in a fits file to Python, use

```python
array = array.transpose(1,2,0)
```

to match IDL notation and get (x,y,t) ordering. 