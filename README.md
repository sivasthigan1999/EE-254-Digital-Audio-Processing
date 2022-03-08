# EE-254-Digital-Audio-Processing

## 1.  Quantization and sampling

For computers to process the continuous signals, however, they must be converted to digital representations via a Analog-to-Digital Converter (ADC). A digital signal is different from its continous counterpart in two primary ways:

It is sampled at specific time steps. For example, sound is often sampled at 44.1 kHz (or once every 0.023 milliseconds).
It is quantized at specific voltage levels. For example, on the Arduino Uno, the microcontroller has a 10-bit ADC, so an incoming, continuous voltage input can be discretized at  5V210=4.88mV  steps.
In this Project, we will use audio data is our primary signal. We'll plot these waveforms, manipulate them, and then play them.

## 1.1  Dependencies
This requires LibROSA—a python package for music and audio analysis. To install this package, you have two options.

**First, from within Notebook, you can execute the following two lines within a cell** 

import sys
!{sys.executable} -m pip install librosa

**Second, from within your Anaconda shell**

> conda install -c conda-forge librosa