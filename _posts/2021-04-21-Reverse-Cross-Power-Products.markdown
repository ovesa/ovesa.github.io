---
layout: post
title:  "What Happens if you Reverse the Signals for the Cross Power and Phase?"
date:   2021-04-12 2:06
categories: [research notes, coding, python, FFT, cross- ower, phase]
published: True
---


# Does the order of the signals matter when computing the cross power and phase?


The cross power of the time series X and time series Y is represented as

$$C_{xy} = FFT(X) \times FFT(Y)^*$$

where $*$ denotes the complex conjugate.


The Fourier transform of the signals X and Y can be decomposed into real and imaginary parts:

$$FFT(X) = a + ib$$

and

$$FFT(Y) = c + id$$.

With some simple algebra, we can see that

$$C_{xy} = (a +ib)(c-id) = ac +ibc +bd - iad = (ac + bd) + i(bc - ad)$$

while

$$C_{yx} = (a -ib)(c+id) = ac + iad -ibc +bd = (ac + bd) + i(ad - bc)$$


As seen, reversing the order of the signals has no affect on the real part of the cross-power. However, the order affects the imaginary part. Thus,

$$C_{xy} \neq -1 \times C_{yx}$$

so the order of the signals does matter.

The order of the signals also affects the sign of the phase as seen below


$$\Delta \phi_{xy} = \arctan \left( \frac{Im(C_{xy})}{Re(C_{xy})} \right)$$

versus

$$\Delta \phi_{yx} = \arctan \left( \frac{-Im(C_{yx})}{Re(C_{yx})} \right)$$


However, it does not affect the magnitude of the phase, so

$$\Delta \phi_{xy} = -1 \times \Delta \phi_{yx}$$


In conclusion, it depends on the convention used, but if the ultimate goal is derive the phase of the cross power, then the order of the signals does not really matter. The order of the signals only affects the sign of the phase.