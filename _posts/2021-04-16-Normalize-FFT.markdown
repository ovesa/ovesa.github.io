---
layout: post
title:  "FFT Normalization"
date:   2021-04-16 2:06
categories: [FFT, research note, FFT normalization]
published: True
---

## Research Note ~ Normalizing a Fourier Transform

In Python, the [forward Discrete Fourier Transform (DFT)](https://numpy.org/doc/stable/reference/routines.fft.html) for a time signal has no normalization factor while the inverse DFT has a normalization factor of $$\frac{1}{N}$$, where $$N$$ represents the total number of samples.

One way to normalize the forward FT for a time series $$x(t)$$ is this form:

$$X(\omega) = \frac{1}{N} \sum_{t=0}^{N-1} x(t) \exp(-i \omega t),$$

where $$\frac{1}{N}$$ represents the normalization constant.

Note: $$N$$ represents the total number of samples, but this number is different depending on the dimensionality of the FT:
- 1-D FFTs: $$N$$ represets the total number of samples in the time domain
- N-D FFTs: $$N = N_x \times N_y \times N_t$$ (or the size of the array)

Normalization of various FT products:


| Product | Normalization | Description|
|------------ | ------------- | --------|
|Fourier Transform | $$X(\omega)$$ | -Complex Valued
                                    -Amplitude & phase information |
|Amplitude/Magnitude | $$\frac{\mid X(\omega) \mid}{N}$$ | -The peaks value(s) of the signal in the time domain 
                                                          -Units: Unit of the signal, say V |
|Power Spectrum | $$\frac{\mid X(\omega) \mid^{2}}{N^2}$$ |  -Power as a function of frequency
                                                            -Units: $$V^2$$ |
|Power Spectral Density | $$\frac{N}{f_s}\frac{\mid X(\omega)\mid^2}{N^2} = \frac{\mid X(\omega)\mid^2}{f_S N}$$ | -Power as a function of frequency per unit frequency 
                                      -Units: $$\frac{V^2}{Hz}$$. 
                                      -$$f_s$$ is the sampling frequency |


When a window is used $w(i)$, the normalization constant for all of these quantities becomes

$$\frac{1}{N} = \frac{1}{\sum_{i=0}^{N} w(i)}$$

and

$$\frac{1}{N^2} = \frac{1}{\left( \sum_{i=0}^{N} w(i) \right)^2}.$$

