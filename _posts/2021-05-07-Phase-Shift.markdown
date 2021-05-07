---
layout: post
title:  "How Do you Correct for a Time Delay between Multiple Signals?"
date:   2021-05-07 2:06
categories: [research notes, coding, python, FFT, phase, time delay, signals, phase shift, time series]
published: True
---

## I want to compare the phase difference between two signals, but there is a time delay. How do I account for that?

When computing the cross power and phase to compare the phase difference between multiple signals, it is important to account for any time delays between the signals. Depending on the instrument, the signals might have been observed simultaneously. This induces an artifical phase offset caused by the time delay of recording the time series.  This time delay needs to be accounted for to accurately compare the signals.

Given a forward Discrete Fourier transform for a time series $$x(t)$$

$$X(\omega) = \frac{1}{N} \sum_{t=0}^{N-1} x(t) \exp(-i \omega t),$$

a time delay ($$t_d$$) in the time domain is equivalent to a phase shift in the frequency domain by multiplying each FFT value by a constant containing the phase shift: 

$$x(t - t_d) \Leftrightarrow X(\omega) \exp(-i \omega t_d).$$

The phase derived from the cross power of two signals is

$$\Delta \phi_{XY} = \arctan \left(  \frac{Im[X(\omega) \times Y(\omega)^*]}{Re[X(\omega) \times Y(\omega)^*]} \right)$$

and it is a linear process. So, you can simply add the time delay between the two signals to the calculated phases.

## Why is the phase shift a linear process?

Euler's law states that 

$$\exp(i \omega t) = \cos(\omega t) + i\sin(\omega t),$$

so the phase can also be expressed as 

$$\phi = \arctan \left( \frac{\sin(\omega t)}{\cos(\omega t)} \right).$$ 
$$=  \arctan (\tan(\omega t))$$
$$= \omega t.$$ 

Thus, the phase shift in frequency space is a linear correction with a slope of $$t = t_d$$, the time delay. So, you can simply add the time delay to the phase difference between two signals:

$$\Delta \phi = \Delta \phi_{XY} + \Delta \phi_{correction}$$

where 

$$\Delta \phi_{correction} = -\omega t_d.$$

##  What does the linear phase shift mean in terms of waves?

A linear phase difference means that all the frequencies of the signal is shifted in time by the same amount. This avoids any potential destructive interference of the waves. The phase shift is relative to the frequencies of the waves.

The larger the $$\omega$$ value, the larger the phase shift. For high frequency waves (large $$\omega$$, small period), the signal varies very slowly. They complete one cycle in a short amount of time. The time delay that needs to be added back to get the waves in phase with one another is smaller. So, they require a larger phase correction.

For low frequency waves (small $$\omega$$, large period), the signal will vary rapidly. Low frequency waves travel a fraction of the period that it takes high frequency waves to complete a cycle in the same time. So, the phase shift and thus phase correction is smaller.