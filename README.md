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

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/eaed9178-6f1f-42b0-9bc2-255565825958" alt="image">
</div>

<p align="center">
  
  **Figure 1. Hardware diagram of TeachSpin 'Muon Physics' equipment (taken from [4]).**
  
</p>


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
It is: $` \tau^- = (2.043 \pm 0.003) \mu s `$ [5]
The ratio of fluxes R, needs to be taken for a given muon momentum. The relativistic energy - momentum relation is:
```math
E^2 = p^2 c^2 + m_0^2 c^4
```
Where: E is the energy of a particle, p is its momentum and m_0 - its mass, c is the speed of light in vacuum. In natural units:
```math
p = \sqrt{E^2 - m_0^2}
```
Where for muons: $`m_0 = (105.6583715 \pm 0.0000035) MeV `$ [6].
Muons which decay in scintillator used in this experiment, have an estimated energy of about 160 MeV. Therefore, their momentum is estimated as $` p \approx 120 MeV `$. 
For this momentum, the ratio is taken as: $` R = 1.21 \pm 0.01 `$ [7].

## Results and Analysis
Gain of the two-stage amplifier is plotted against the signal frequency. Gain is defined as ratio between output and input voltages, to obtain the real gain of the amplifier, this value is additionally multiplied by 21, due to the attenuation resistors inside the electronics box.

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/ca0f23e8-66ce-43cb-a08d-cae6f42eb2ef" alt="image">
</div>

**Figure 2. Gain of the two-stage amplifier used in TeachSpin apparatus vs frequency of the sine wave voltage input from the function generator.**

On Figure 2, it can be seen that gain depends significantly on the frequency, however there is a region in which gain appears to be stable. Based on those measurements, the stable gain frequency range was estimated to be from $` (20.92 \pm 0.01)kHz `$ to $` (396.3 \pm 0.1)kHz `$. Limits of the range of decay times with stable range are taken as the inverses of the frequency limits. This gives a range of decay times that can be measured reliebly as: $` (2.52 \pm 0.01) \mu s - (47.80 \pm 0.02) \mu s `$. The upper limit is however larger than the maximum decay time allowed by the FPGA, therefore the final range in which we can measure decay times reliably is taken as: 
```math
(2.52 \pm 0.01) \mu s - 20 \mu s
```
<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/8966dabe-dc13-4a86-9c27-49362ae9fb59" alt="image">
</div>

**Figure 3. Gain vs frequency in the stable gain range of the amplifier, red line roughly indicates which data points are within each other's uncertainties.**

In the next step, timing of FPGA timer was checked against the readings from an oscilloscope. 

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/ec78b0be-9ad5-404a-a0f3-2ec04ae3d99b" alt="image">
</div>

**Figure 4. Time interval between pulser signals measured by FPGA, vs measured by the oscilloscope. Linear fit is performed using least squares rule.**

Perfect agreement between the two methods of measurement would correspond to a line 1x+0 on the graph, the obtained fit parameters are within their uncertainty from it. This indicates that FPGA measures time between two signals reliably. It was also noticed, that as expected when time separation between two signals was larger than $` 20 \mu s `$, 'Muon Physics’ program was not showing the time between signals but instead, number of instances when the second flash did not occur within the FPGA timing window. 
The vertical flux through scintillator is estimated as flux [8] times scintillator’s base area, to be $` \approx 3 s^-1 `$.


A total of 4 data collection runs have been performed, with total duration of 68:36:14 (hh:mm:ss). Total number of muon decays recorded was 1970, the average muon flux in all runs was slightly lower than 3, between $` 2.6025 s^-2 `$ and $` 2.9004 s^-1 `$. It is better to underestimate flux, since that way noise is decreased. Data was collected and decay times were plotted as a histogram. 

Collected muon decays data is cut to account for the stable region: all decay times below $` 2.52 \mu s `$ are disregarded. For the histogram, number of bins is chosen as square root of number of remaining data points, rounded up to integer [9]. 
In this experiment, muons are detected with constant average rate $` \approx 3 s^-1 `$, it can be expected that rate of occurances in a given bin is also constant. Therefore, the number of occurances measured in each bin, is described by Poisson distribution, with average of the distribution taken as the observed number of counts in a gvien bin. This indicates that uncertainty of number of counts in a bin is equal to square root of number of counts in that bin: $` \delta N  = \sqrt{N} `$ [10].
This description works however only for larger numbers of occurances, therefore in a histogram, neighbouring bins are combined in such a way that each bin contains at least 5 counts. Fitting is then performed. 

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/0d361020-996a-412c-9a7d-d73dfbe25981" alt="image">
</div>

**Figure 5. Histogram of the muon decay data together with fitted function.**

A muon lifetime is obtained as:
```math
\tau = (2.1 \pm 0.2) \mu s
```

Therefore positive muon lifetime is obtained as:

```math
\tau^+ = (2.2 \pm 0.3) \mu s
```
This value is in agreement with the reported $` (2.1969803 \pm 0.00000022) \mu s `$ [11]. 

And the Fermi coupling constant (in natural units):

```math
\frac{G_F}{(\hbar c)^3} = \sqrt{\frac{192 \pi^3 \hbar}{(m_{\mu} c^2)^5 \tau_{\mu}}} = (1.16 \pm 0.08) 10^{-5} GeV^{-2}
```
Which agrees with $` \left(1.1663787\pm0.0000006\right)\ {10}^{-5}{\ GeV}^{-2} `$ Codata recommendation [12]. 

Impact of the number of bins and how low decay times are disregarded (the cut threshold) on the fitted lifetime was investigated. 

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/8ad8262f-48a1-4e32-a524-38f63d4f3594" alt="image">
</div>

**Figure 6. Fitted lifetime value relation to how low decay times are disregarded (cut threshold).**


<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/11e1da44-a0dd-473f-8c45-db5a9eda2da7" alt="image">
</div>

**Figure 7. Fitted lifetime value relation to the chosen initial number of bins (before combining bins together for at least 5 counts in each).**

Figure 7 reveals a negative correlation between fitted lifetime and how many bins are initially chosen. This lowers confidence in fit result, since the method of rounding up square root of number of data points for choosing number of bins is a rule of thumb. The reason for this correlation is the fact that for bigger numbers of bins, each bin contains less counts, because the constant total number of counts is being distributed into more bins. Since decay times are exponentially distributed, for large decay times there is generally less occurrences. However after combining the bins, each bin for larger decay times has at least 5 counts, therefore choosing bigger number of bins decreases counts in bins at lower decay times, but does not change them at larger decay times, due to the method of combining the bins together. This tends to make the distribution less ‘steep’ which corresponds to lower lifetime values. This can be observed, by comparing fitted functions and histograms for different numbers of bins. 

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/80a4a5ae-1f3d-47ac-add6-866c39398155" alt="image">
</div>

**Figure 8. Numbers of occurrences in bins together with fitted function, for 25 bins (before combining them).**

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/1a197122-f4bb-408b-aaa3-6351f1496bef" alt="image">
</div>

**Figure 9. Numbers of occurrences in bins together with fitted function, for 60 bins (before combining them).**

Graphs 8 and 9 show how numbers of occurrences decrease at small decay times when number of bins is chosen as bigger, but they stay almost unchanged for large decay times. This results in the trend of decreasing fitted lifetime for increasing number of bins. 

The same relations of fitted lifetime to number of bins and cut threshold are also investigated for fitting without combining the bins together. 

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/5831fa95-230e-43a4-bab8-113d903a5642" alt="image">
</div>

**Figure 10. Fitted lifetime value for unchanged bins relation to how low decay times are disregarded (cut threshold).**

Figures 6 and 10 show similar trend between the fitted lifetime and cut threshold.

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/cb2eafba-4a71-4a38-a9b7-57bdff736671" alt="image">
</div>

**Figure 11. Fitted lifetime value for unchanged bins relation to the chosen number of bins.**

Figure 11 reveals, that the negative correlation between lifetime and number of bins disappears when the bins are not changed. 

The goodness of fit is additionally tested by investigating how the reduced $` \chi^2 `$ depends on number of bins for a fit to a histogram with combined bins such that each bin contains at least 5 occurrences.

<div align="center">
  <img src="https://github.com/p-mucha/Muon-Lifetime-Experiment/assets/126366877/568a7068-1d3a-4313-8e6b-b5d8e2d11c75" alt="image">
</div>

**Figure 12. Reduced $` \chi^2 `$ relation to the initial number of bins when combining the bins together such that each bin contains at least 5 occurrences.**

The general trend in the reduced $` \chi^2 `$ is that it is large for small numbers of bins, above 1, and it decreases with growing number of bins, until after about 40 bins, where it oscillates between about 0.4 and 0.95, without any clear positive or negative correlation. 
For the histogram on Figure 5, the initial number of bins is 25, for which the reduced $` \chi^2 `$ is equal to 0.850, this indicates a good fit.  

## Conclusion

The positive muon lifetime was obtained as:
```math
\tau^+ = (2.2 \pm 0.3) \mu s
```
And the Fermi coupling constant:
```math
\frac{G_F}{(\hbar c)^3} = (1.16 \pm 0.08) 10^{-5} GeV^{-2}
```
Both values are within their uncertainties from the results reported in [11] and [12]. The main source of error to the Fermi constant is measured muon lifetime. 

The precision of this experiment could be further improved by collecting more muon decays data. Another improvement would be an amplifier with stable gain in wider range of frequencies, since then more muon decays could be measured. In this experiment, a single scintillator is used, while it is beneficial to use configurations of multiple scintillators, as in [3], which allows for better noise estimation. 
In this experiment, decay times of muons produced in atmosphere were observed. This means that there is a contribution from both positive and negative muons. This introduces additional uncertainty. Alternatively different source could be used for the production of only one type of muons. 
The method of using scintillator and PMT as in this experiment, is widely used in particle physics research.



## References
[1]	J.M. Cassels, ‘Pion and Muon Decay [and Discussion]’, the Royal Society publishing, Series A, Mathematical and Physical Sciences, p.463, (Aug 1958) \
[2]	T. P. Gorringe, D. W. Hertzog, ‘Precision Muon Physics’, Progress in Particle and Nuclear Physics, p.4, 2015 \
[3]	D.M. Webber et al, ‘Measurement of the Positive Muon Lifetime and Determination of the Fermi Constant to Parts-per-Million Precision’, Phys. Rev. Lett. Vol 106, p.1, (2011) \
[4]	TeachSpin, INC, ‘Muon Physics’, [online]. [Accessed 8.11.2022]. Available from: https://www.teachspin.com/muon-physics \
[5]	R. A. Reiter et al., ‘Precise Measurement of the Mean Lives of $` \mu^+ `$ and $` \mu^- `$ Mesons in Carbon’, Phys. Rev. Lett. Vol. 5, Iss. 1, p. 23, (1960) \
[6]	J. Beringer et al., ‘Review of Particle Physics’ (Particle Data Group), Phys. Rev. D 86, 010001, p. 30, (2012) \
[7]	M. Bahmanabadi, F. Sheidaei, M. Khakian, and J. Samimi, ‘The charge ratio of the atmospheric muons at low energy’. Phys. Rev. D 74, 082006, p. 1, (2006) \
[8]	R. L. Workman et al. (Particle Data Group), ‘Progress of Theoretical and Experimental Physics’. Vol. 2022, p. 522, 2022 \
[9]	Jay D., Roxy P., ‘Statistics: The Exploration and Analysis of Data’. Fourth edition. Duxbury. 2001, p. 65  \
[10]	Hughes, Ifan, and Thomas Hase, ‘Measurements and Theis Uncertainties: A Practical Guide to Modern Error Analysis’. Oxford University Press, Incorporated, 2010, p. 64 and p. 111 \
[11]	V. Tischenko et al. (MuLan Collaboration), ‘Detailed report of the MuLan measurement of the positive muon lifetime and determination of the Fermi constant’. Phys. Rev. D 87, 052003, p. 1, (2013) \
[12]	Peter J. Mohr, David B. Newell, and Barry N. Taylor, ‘CODATA recommended values of the fundamental physical constants: 2014’. Rev. Mod. Phys. 88, 035009, p. 41, (2016) 
