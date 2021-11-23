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
VCO is a circuit whose output signal frequency is controoeld by input voltage value. <br>
It is realised by a chain of inverters with a way to control teh output current. <br>
By controlling the Vctrl shown below, current of the inverter chains is changed which affects the frequency.

![1](/vco_block.JPG "2")


# Frequency Divider





