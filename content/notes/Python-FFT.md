---
title: "Python's FFT" 
date: 2021-03-15
tags: ["Note",]
author: ["Oana Vesa"]
description: "Clarifies how Python’s FFT implementation defines the forward and inverse discrete Fourier transforms and how these definitions relate to standard mathematical expressions for frequency and angular frequency."
summary: "The note presents the exact DFT conventions used by NumPy and SciPy, explicitly defining the normalization, sign conventions, and index roles in the forward and inverse transforms. It connects the discrete formulation to the continuous exponential form, interprets the meaning of each index and parameter, and clarifies how discrete frequency, cycles per sample, and angular frequency are related. The goal is to make Python’s FFT conventions transparent and avoid common sources of confusion when interpreting spectral results."
editPost:
    URL: "https://ovesa.github.io/"
    Text: "GitHub repository"
showToc: true
disableAnchoredHeadings: false

---

## Research Note ~ Deciphering Python's FFT


In Python, the [forward Discrete Fourier Transform (DFT)](https://numpy.org/doc/stable/reference/routines.fft.html) for a time signal $a(m)$ using both numpy and scipy is represented as 

$$A(k) = \sum_{m=0}^{n-1} a(m) \exp \left(-2\pi i \frac{mk}{n}\right)$$

and the inverse DFT is

$$a(m) = \frac{1}{n} \sum_{k=0}^{n-1} A(k) \exp \left( 2\pi i \frac{mk}{n}\right).$$

The forward DFT is analagous to

$$A(k) = \sum_{m=0}^{n-1} a(m) \exp (-i \omega n).$$

- $$a(m)$$ corresponds to the input sequence
- $$n$$ is the number of samples in the time domain
- $$k$$ is the number of cycles
- $$m$$ is the current index/sample
- $$\frac{k}{n}$$ corresponds to the frequency of the signal ($$k$$ cycles per $$n$$ samples)
- Relationship between angular frequency and temporal frequency: $$\omega = 2 \pi f$$

