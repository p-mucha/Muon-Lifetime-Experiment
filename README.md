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
D(t) = \frac{1}{\tau_{\mu}} e^{- t/ \tau_{\mu}}
```
Since negative muon has one more way of disappearing than positive muon, its effective lifetime is slightly shorter.
Knowing the positive muon lifetime constant $` \tau_{\mu} `$, the Fermi coupling constant $`G_F `$ can be calculated as [3]:

```math
G_F = \sqrt{\frac{192 \pi^3 \hbar^7}{\tau_{\mu} m_{\mu}^5 c^4}}
```

## Method

For the detection of muons, the 'Muon Physics' apparatus by TeachSpin is used. It consists of the detector module and electronics module. Active part of the detector module is single right circulat cylinder, polyvinyl toluene (PVT) - based scintillator with 15 cm diameter and 12.5 cm height. It is optically coupled to a photomultiplier tube (PMT). The entire hardware setup is shown on Figure 1.

When muon enters scintillator, it causes excitation of scintillator’s molecules, this leads to light emission, which is then converted to an electric signal by the PMT. If muon stops inside the scintillator, it eventually decays and produces a second light signal, which is also converted to an electric signal by the PMT. Signals from the PMT are then amplified by a two-stage amplifier. The output is fed to the discriminator, and after that to the FPGA timer. Discriminator works as an adjustable voltage threshold, signals below this threshold are cut and not measured. This is done to limit the amount of noise, as muons are not the only particles that could produce light signal in scintillator. Since expected flux of muons entering the detector can be estimated, discriminator threshold can be adequately adjusted, until such muon rate is achieved, which allows to limit the noise. FPGA timer is responsible for distinguishing pairs of signals which occur close in time,  from all the other signals. A signal above the discriminator threshold starts the 50 MHz FPGA timer, if second signal appears within 20 $`\mu s `$, the time between them is recorded. This corresponds to muon entering scintillator, producing first signal, stopping and decaying inside scintillator, thus producing second signal. If second signal does not occur within this timing window, timer clock resets. This scenario corresponds to muon passing through scintillator, without decaying. All the data, is then processed to a Laptop via USB port, decay times are plotted as histogram using ‘Muon Physics’ program. 

In the first part of calibration of the experimental setup, gain of the two stage amplifier located inside the electronics box was measured for a range of signal frequencies using sine wave signal from function generator. Gain is defined as ratio between voltage output and voltage input. In this experiment, TG315 function generator was used. GDS-1102A oscilloscope 

was used to measure both the signal input and amplifier output. Frequency of the signal given by the function generator was also checked against value measured by the oscilloscope. It is important to know, over what range of frequencies the gain is constant.
Muon that stops and decays produces two signals with some time period between them. Strength of those signals is related to the energy of muon, only signals strong enough to not be cut by the discriminator threshold can be detected. Inverse of the period between two signals is interpreted as signal frequency. If signals at different frequencies are amplified by different gains, then muons with different decay times will have different ranges of energies in which they can be detected. For reliable measurement of muon lifetime, it is crucial, that muons with different decay times have the same probability of detection. 

In the second step of calibration of the instruments, it is verified experimentally, whether FPGA timer measures time intervals accurately. This is done using build in LED pulser (see Figure 1) which emits light to the scintillator, imitating muon decays. Then time between two pulses is measured using oscilloscope and compared to the results from the FPGA which are shown on a ‘Muon Physics’ program window on a computer.

After the calibration, muon decays can be detected. Muon flux through the scintillator is estimated, and the discriminator threshold is set to such value to achieve muon rate slightly lower than the estimation. The collected decay times are then plotted as a histogram and analyzed.  
Muon decays follow exponential distribution, therefore a fit function to the histogram is chosen as:
```math
f(t) = A exp(- \frac{1}{\tau} t) + B
```
Where: A is a fit constant without a physical meaning, B is a fit constant corresponding to noise, $` \tau `$ is muon lifetime.
A fit to the histogram is performed according to the least squares rule, using curve_fit in Python. Thus, muon lifetime \tau is obtained as one of the fit parameters. 
This fitted muon lifetime observed in the experiment, has contribution from both negative and positive muons:
```math
\frac{1}{\tau_{obs}} = \frac{N^+ \frac{1}{\tau^+} + N^- \frac{1}{\tau^-}}{N^+ + N^-}
```
Where: $`\tau_{obs}`$ - fitted muon lifetime, $`\tau^+`$ and $` \tau^- `$ - positive and negative muon lifetimes respectively, $`N^+ `$ and $` N^- `$ - numbers of positive and negative muons detected respectively. 

Using ratio of positive to negative muon fluxes $` R(\frac{\mu^+}{\mu^-}) = \frac{N^+}{N^-} `$, positive muon lifetime can be obtained as:
```math
\tau^+ = \frac{R \tau_{obs} \tau^-}{\tau^- + R \tau^- - \tau_{obs}}
```
Negative muon lifetime $` \tau^- `$ is taken as negative muon lifetime on carbon, since scintillator used in this experiment is carbon based. 
It is: $` \tau^- = (2.043 \pm 0.003) \mu s $` [5]
The ratio of fluxes R, needs to be taken for a given muon momentum. The relativistic energy - momentum relation is:
```math
E^2 = p^2 c^2 + m_0^2 c^4
```
Where: E is the energy of a particle, p is its momentum and m_0 - its mass, c is the speed of light in vacuum. In natural units:
```math
p = \sqrt{E^2 - m_0^2}
```
Where for muons: $`m_0 = (105.6583715 \pm 0.0000035) MeV `$ [6].
Muons which decay in scintillator used in this experiment, have an estimated energy of about 160 MeV. Therefore, their momentum is estimated as $` p \approx 120 MeV. 
For this momentum, the ratio is taken as: $` R = 1.21 \pm 0.01 `$ [7].

## Results and Analysis

## References
[1]	J.M. Cassels, ‘Pion and Muon Decay [and Discussion]’, the Royal Society publishing, Series A, Mathematical and Physical Sciences, p.463, (Aug 1958) \
[2]	T. P. Gorringe, D. W. Hertzog, ‘Precision Muon Physics’, Progress in Particle and Nuclear Physics, p.4, 2015 
[3]	D.M. Webber et al, ‘Measurement of the Positive Muon Lifetime and Determination of the Fermi Constant to Parts-per-Million Precision’, Phys. Rev. Lett. Vol 106, p.1, (2011)
