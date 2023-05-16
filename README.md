# Muon-Lifetime-Experiment

## Summary
A single cylindrical scintillator, together with a PMT were used to detect decays of muons produced in atmosphere. Times between muon entering the detector and decaying were plotted as a histogram and an exponential fit was performed to find the muon lifetime. From this, the positive muon lifetime was found to be $` \tau^+ = (2.2 \pm 0.3) \mu s `$. The Fermi coupling constant was obtained as $` \frac{G_F}{(\hbar c)^3} = (1.16 \pm 0.08) 10^{-5}  GeV^{-2} `$. Various properties of fit were investigated, such as its dependance on number of bins chosen for the histogram.

## Introduction

A muon is one of the elementary particles, it often can be treated as an unstable, much heavier electron. Muons have an electric charge of -1e and spin 1/2, their antiparticle - antimuons, have +1e electric charge. According to the sign of their charge, muons and antimuona are also referred to as negative and positive muons respectively, and are denoted as $` \mu^- `$ and $`\mu^+ `$. Muons are produced in Earth's atmosphere, as a result of cosmic radiation colliding with air molecules. Muons are unstable, they decay, and negative muons can also disappear through a process called muon capture. Muon decay and processes are [1], [2]: 
```math 
\mu^- \rightarrow e^- + \bar{v_e} + v_{\mu}
```

```math 
\mu^+ \rightarrow e^+ + v_{e} + \bar{v_{\mu}}
```

```math 
\mu^- + p \rightarrow n + v_{\mu}
```
The decay rate of muons is characterised with a constant called the muon lifetime. If at moment t, there are given N(t) muons and the decay rate is $` \lambda `$, then change in muon population in short time interval dt can be written as:
```math 
\frac{dN}{N(t)} = - \lambda dt
```

Parameter $` \lambda `$ is inverse of the muon lifetime:

```math
\tau_{\mu} = \frac{1}{\lambda}
```
This leads to probability density of decay at time t for a single muon:

```math
D(t) = \frac{1}{\tau_{\mu}} e^{- \frac{1}{\tau_{\mu}} t}
```
Since negative muon has one more way of disappearing than positive muon, its effective lifetime is slightly shorter.
Knowing the positive muon lifetime constant $` \tau_{\mu} `$, the Fermi coupling constant $`G_F `$ can be calculated as:

```math
G_F = \sqrt{\frac{192 \pi^3 \hbar^7}{\tau_{\mu} m_{\mu}^5 c^4}}
```



## References
[1]	J.M. Cassels, ‘Pion and Muon Decay [and Discussion]’, the Royal Society publishing, Series A, Mathematical and Physical Sciences, p.463, (Aug 1958) \
[2]	T. P. Gorringe, D. W. Hertzog, ‘Precision Muon Physics’, Progress in Particle and Nuclear Physics, p.4, 2015 
