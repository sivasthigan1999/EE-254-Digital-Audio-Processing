# EE-254-Digital-Audio-Processing

## 1.  Quantization and sampling

For computers to process the continuous signals, however, they must be converted to digital representations via a Analog-to-Digital Converter (ADC). A digital signal is different from its continous counterpart in two primary ways:

* It is sampled at specific time steps. For example, sound is often sampled at 44.1 kHz (or once every 0.023 milliseconds).
* It is quantized at specific voltage levels. For example, on the Arduino Uno, the microcontroller has a 10-bit ADC, so an incoming, continuous voltage input can be discretized at  5V210=4.88mV  steps.
In this Project, we will use audio data is our primary signal. We'll plot these waveforms, manipulate them, and then play them.

## 1.1  Dependencies
This requires LibROSA—a python package for music and audio analysis. To install this package, you have two options.

**First, from within Notebook, you can execute the following two lines within a cell** 

import sys
!{sys.executable} -m pip install librosa

**Second, from within your Anaconda shell**

> conda install -c conda-forge librosa


## 2. Quantization

Quantization refers to the process of transforming an analog signal, which has a continuous set of values, to a digital signal, which has a discrete set.

**For example**-- The ATmega328 on the Arduino Uno, has a 10-bit analog-to-digital (ADC) converter while the ESP32 has a 12-bit ADC. Because the ATmega328 runs on 5V, the ADC "step size" is  5V210=4.88mV . This is the tiniest discriminable change you can observe on the Uno's analog input pins. In contrast, the ESP32 runs on 3.3V and has a higher bit resolution (12 bits), so the ADC has much finer discretizations:  3.3V212=0.806mV —roughly, six times more precision than the Uno!

**Characterizing quantization error**
A digitized sample can have a maximum error of one-half the discretization step size (±½ the "Least Significant Bit" (LSB)). Why? Because when we convert an analog value to a digital one, we round to the nearest integer. Consider a voltage signal of 0.2271V on an Uno's analog input pin, this is nearly halfway between steps 0.2246V and 0.2295V, which would result in an error of  4.89mV2  (and either gets converted to 47 or 48 via Arduino's analogRead).

## Effect of Quantization on Audio signals.

In this project we work with pre-digitalized audio waveforms sampled at 44.1kHz and quantized at 16-bits and we'll downsample to observe the effects of quantization levels and sampling rates.
1. **8-bit quantization** - When sample from 16 bit to 8 bit wwe can notice a small difference in audio while hearing 

2. **6-bit quantization** - At this level, we can start to hear degradations in the signal—a hissing sound (at least with headphones). And we can begin to see obvious discretized steps in the     zoomed-in waveform 

3. **4-bit quantization**- At 4 bits, the noise is more substantial. Take a look at the zoom plot on the right, the steps between quantization levels are far more noticeable. And yet, our hears can still somehow parse the word "hello"—though you should playback this signal for someone who doesn't know what's being said to determine comprehensibility.

4. **3-bit quantization** - At 3-bits, the sound is no longer intelligible

5. **2-bit quantization** - it has very very low quantization level


 ## 3. Nyquist Sampling Theorem

It is the most fundamental theorems in **signal processing**: the Nyquist Sampling Theorem, which states that a continuous signal can be reconstructed as long as there are two samples per period for the highest frequency component in the underlying signal.
for a perfect reconstruction, our digital sampling frequency  fs  must be at least twice as fast as the fastest frequency in our continuous signal:  fs=2∗max(analogfreq) .

For example, imagine we have an analog signal composed of frequencies between 0 and 2,000 Hz. To properly digitize this signal, we must sample at  2∗2,000Hz . So,  fs  needs to be 4,000Hz.

Now imagine that the fastest our digitizer can sample is 6,000 Hz: what frequency range can we properly capture? Since we need a minimum of two samples per period for proper reconstruction, we can only signals that change with a frequency of 0 to a maximum of 3,000Hz. This 3,000Hz limit is called the **Nyquist limit**  it is  12  the sampling rate  fs .

For many applications related to Human-Computer Interaction and Ubiquitous Computing, sampling at 4kHz is more than sufficient. This enables analysis of any signal between 0-2kHz. Human motion ambulatory movement, limb motion, finger gestures are simply does not change that fast. Even electroencephalograms (EEG), which measure electrical activity in the brain, are often sampled at 500-1000Hz. However, for recording sound (humans can hear between 0-20kHz), faster sampling rates are necessary.

 ## 4. Aliasing
When we sample a signal with frequency components greater than the Nyquist limit. We get aliasing problem where the higher frequency components of a signal (those greater than the Nyquist limit) appear as lower frequency components

### Experimenting with the Nyquist limit

Now we experiment with the Nyquist limit and aliasing but this time with sound data. Sound is a bit harder to visualize than our synthetic signals above because it's very high frequency  but in the note book I  provide zoomed insets to help.

We will also be using spectrogram visualizations to help us investigate the effect of lower sampling rates on the signal. A spectrogram plots the frequency components of our signal over time.

1. **Sweep with sampling rate of 44,100 Hz**

2. ** Same sweep but with a 11,025 Hz sampling rat**

3. ** Same sweep but with a 882 Hz sampling rate** 