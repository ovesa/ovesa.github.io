---
title: "Difference between arrays in Python and IDL" 
date: 2021-05-01
tags: ["Note",]
author: ["Oana Vesa"]
description: "This note explains why images and data arrays can appear transposed when comparing FITS files between Python and IDL, and how to reconcile the differing array conventions."
summary: "Python and IDL store and interpret multi-dimensional arrays using different axis orderings, which leads to apparent transposition when visualizing the same FITS data. In Python, FITS files are typically read as (t, y, x), whereas IDL uses (x, y, t). Although both languages use zero-based indexing, their axis conventions differ. The note shows how to use a simple transpose operation in Python to reorder the array dimensions and recover IDL-style (x, y, t) ordering for consistent comparison and analysis."
editPost:
    URL: "https://ovesa.github.io/"
    Text: "GitHub repository"
showToc: true
disableAnchoredHeadings: false

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
array = array.transpose(2,1,0)
```

to match IDL notation and get (x,y,t) ordering. 
