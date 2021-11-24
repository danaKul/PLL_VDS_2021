# PLL_VDS_2021  
## Why PLL?
PLL is used to get very precise clock signal without a frequency or phase noise. <br>
While Quartz crystals can do that, they have soem practical limitations like integrating on chip, because of which Voltage Controlled Oscillators(VCO) are instead used which are a part of PLL system. <br>

#  PLL Components

![pllc](/pll_compo.JPG "pllc")

As seen in the block diagram, PLL  has a Phase Frequency Detector(PFD), Charge Pump(CP), Low Pass FIlter(LPF), VCO, and Frequency Divider(FD) <br>

# Phase Frequency Detector

![pfdb](/pfd_block.JPG "pfdb")


A phase detector (PD) is realised with an XOR gate which genertes output if the 2 signals are out of phase. As shown above, but it doesnt tell us which signal is leading and which is lagging. FOr that an improved circuit, called Phase Frequency Detector(PFD) is used. As shown below it has 2 outputs to show which signal is leading and which is lagging.

![1](/pfd_wave.JPG "2")

Depending on the delays of the components, some minute phase diff between the 2 signals may not be detected, called dead zone.  <br>

Smaller the dead zone, better the PFD <br>


![1](/pfd_cir.JPG "2")

#  Charge Pump

Charge pump  converts the diff in phase between the two signals in to an analog control signal/voltage. When up signal is high, Capacitor is charged and when down signal is high, capacitor is discharged. <br>

![1](/cp_block.JPG "2")

The circuit shown may suffer from leakage. <br>

The fluctuations in voltage on the Capacitor are removed using a low pass filter.


![1](/loop_filter.JPG "2")

# Voltage Controlled Oscillator (VCO)
VCO is a circuit whose output signal frequency is controlleld by input voltage value. <br>
It is realised by a chain of inverters with a way to control the output current. <br>
By controlling the Vctrl shown below, current of the inverter chains is changed which affects the frequency.

![1](/vco_block.JPG "2")


# Frequency Divider

Frequecy Divider(FD) as the name suggests divides input freuency in half. <br>
It is realised as shown below. <br>

Output of a D f/f is half the frequency of its input clk. Thus a D f/f with an inverter  is a 1/2 Frequency Divider

![1](/fd_block.JPG "2")

![1](/dff_fd.JPG "2")


# VCO terminologies

Some important VCO terminologies are as below. <br>
<br>
<br>
![1](/vco_terms.JPG "2")

# Tools used in the project

1. Ngspice for prelayout simulations  <br>
2. Magic for post layout simulations and parasitic extraction  <br>

# Development Flow

1. SPICE-level Circuit Development
2. Pre-Layout Simulation
3. Layout Development
4. Parasitic Extraction
5. Post-Layout Simulation  

## PDK

PDK used is Open Source Google-Skywater 130nm


## PLL Specifications

He,re apart from the PVT corners mentioned, 
Simulatiosn will be done for VCO mode where,  a control voltage will be directly provided to VCO and thus PLL will be used as VCO. <br>
Another mode is PLL mode where whole whole PLL will be simulated. <br>
Frequency range shows the range of frequencies for which PLL must work.  <br>
Noise is specified to be less than 10nS, and jitter rms > 20nS <br>

![1](/pll_spec.JPG "2")


### PFD implentation to reduce Dead Zone

![1](/pfd_new.JPG "2")

### Replacement CP circuit to reduce leakage

![1](/cp_new.JPG "2")

###  FD Simulation

![1](/fd_sim_wave.JPG "2")


As can be seen, out frequency(red) is half the input frequency(blue)

###  CP simulation

![1](/cp_wave_1.JPG "2")

When v2=v3=0, output  is charged with leakage current and we see this small(uV) voltage output building up. <br>
Initial condition on this o/p was 0v. <br>

When v2 is a pulse input with 200nS period, we get following plot of output for 50uS, output voltage approaching 900mV  <br>

![1](/cp_wave_2.JPG "2")

### VCO Simulation

Here, control voltage is v2 in spice netlist file. For 0.6V control voltage, we get the o/p of the VCO as shown below.

![1](/vco_sim_wave_1.JPG "2")

### PFD  Simulation

As shown I the waveforms, as the phase difference of 2 inputs are fixed, 1 signal(up) is always 0 while signal down  shows the phase difference between the 2 input signals.

![1](/pfd_sim_wave_1.JPG "2")


### Simulation of Complete PLL

Shown below is teh block diagram for the PLL system.  <br>
Here, ref clock, clk_ref  is 80nS which is 12.5MHz and f/b clock is 1/8  <br>

![1](/pll_draw.JPG "2")

Below is the whole view of transient simulation waveforms.

![1](/pll_wave_1.JPG "2")

Here is the initial part of transient sim, At the bottom, we see that the blue vco output frequency is much lower than red clk_ref

![1](/pll_wave_2.JPG "2")





