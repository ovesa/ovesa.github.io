---
layout: post
title:  "How Do You Correct For a Time Delay?"
date:   2021-04-12 2:06
categories: [research notes, coding, python, FFT, phase, time delay, signals, phase shift]
published: False

output: 
  pdf_document:
    extra_dependencies: ["amssymb"]
---


# If I have a time delay between two signals, how do I correct for that?

The forward Discrete Fourier transform for a time series, $x(t)$, can be expressed as
$$X(\omega) = \frac{1}{N} \sum_{t=0}^{N-1} x(t) \exp(-i \omega t).$$

The time shifting property of Fourier transforms states that a time delay ($t_d$) in the signal is equivalent to a phase shift in the frequency domain by multiplying each FFT value by a constant: 
$$x(t - t_d) \Leftrightarrow X(\omega) \exp(-i \omega t_d).$$

Thus, the phase shift is a linear process. Euler's law shows that $\exp(-i \omega t) = \cos(\omega t) + i\sin(\omega t)$. Each value in the Fourier transform is complex. The phase of the Fourier transform can be expressed as
$$\Phi = \arctan \left(  \frac{Im[X(\omega)]}{Re[X(\omega)]} \right).$$

This is similar to stating 
$$\Phi = \arctan \left( \frac{\sin(-\omega t)}{\cos(-\omega t)} \right).$$ 

Using the fact that cosine is an even function $\cos(-x) = \cos(x)$ and sine is an odd function $\sin(-x) = -\sin(x)$,

$$\Phi = \arctan \left( \frac{\sin(-\omega t)}{\cos( -\omega t)} \right)$$
$$= \arctan \left( \frac{-\sin(\omega t)}{\cos(\omega t)} \right)$$
$$= - \arctan (\tan(\omega t))$$
$$= - \omega t$$ 

Thus, the phase shift in frequency space is a linear process with a slope of $t_d$. This can be added to the phase of the Fourier Transform: $\Phi_{corrected} = \Phi_{X(\omega)} + \Delta \Phi$

#  What does the linear phase shift mean for waves?

The bigger the $\omega$ value, the larger the phase shift. For high frequency waves (large $\omega$, small period), the signal varies very slowly. For low frequency waves (small $\omega$, large period), the signal will vary rapidly. Low frequency waves travel a fraction of the period of high frequency waves before the high frequency wave completes its cycle.


rate of oscillation increases as omega increases


Fourier transform produces two components: phase and magnitude. Magnitude shows how much each frequency component is contributing to the signal

phase shifts the signal along the tmime axis. at any given frequnecy, there will be a time delay for that frequency

a fixed time delay causes a linear phase shift

linear phase -> constant group delayso the group of all frequencies ina  waveform will be delayed by the same amount in time and not cause destructive interference between the different frequences in the group.

FT in rectangular coordinates ~ A e^j phi = A cos() + j sin() = I + jQ


rectangular coordinates give real and imaginary components
polar coordinates give magnitude and phase components