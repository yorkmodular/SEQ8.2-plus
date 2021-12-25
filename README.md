# SEQ8.2-plus - 8-step CV sequencer with dual clock out

The original SEQ8 module was one of the first ones that I made with a run larger than 3 - the 8.2 
was an updated version, and now we have the 8.2+ which is yet another update.

It shares most of the features of its predecessors - 8-step, adjustable CV on each step and a reset 
input. In addition, there's now an internal, free-running clock which is multed to a pair of clock 
outputs; the external clock input is still there, and if there's a signal there it'll be routed to 
the clock outs instead of the internal clock.

Reset on power up is still there, but the free-running internal clock means that the sequence will 
often roll over to step 2 on power up; there are workarounds for this, most of which involve making 
sure that the reset input is high when the sequencer is started irrespective of whether you're using 
an external or internal clock.

Both clock and reset will trigger on the rising edge of an incoming signal - furthermore, the sequencer 
will be held at step 1 for as long as the reset signal is high. Counting will not resume until the reset 
signal goes low again.

Whether you use gate or trigger inputs is a matter of personal choice.

## Build notes

* Do **NOT** be tempted to use 74HC-series ICs - chances are they won't work well (or at all) and will
place serious constraints on the voltage output. CD40106 and CD4017 ICs are easy to get hold of and
not that much more expensive. Plus they'll tolerate up to 18V.
* The output of the voltage regulator (IC2) is a matter of choice - bearing in mind that the LEDs will
take about 1.7V (assuming you use red LEDs), plus another 0.6V for the 1N4148s, I recommend using a 
7808 or 7809 regulator; either of these will give you a comfortable range of 0-5V.
* LED resistors (R5, R8-11 and R13-16) are representative values - 1k or 2k2 is a good choice for most 
cases. However, if you're using high-brightness LEDs, larger values may be needed (as high as 10k in some
cases)
* The free-running clock is a standard Schmitt trigger oscillator (U1, R1, VR1 and C1)  - the overall 
range will be governed by the values of C1 and VR1. C1=2u2 and VR1=100k are good, reliable values - a 
linear-taper pot is highly recommended.
* If you want to minimise the diode voltage drop, replace D5-D12 with appropriate Schottky diodes.

## Files

* _SEQ8.2-plus-BOM.xlsx_ - Bill of Materials
* _SEQ8.2-plus-panel.dxf_ - front panel in AutoCAD DXF format
* _SEQ8.2-plus-panel.fpd_ - front panel in Schaeffer FPD format
* _SEQ8.2-plus-panel.kicad_pcb_ -front panel in KiCAD format
* _SEQ8.2-plus-schematic.png_ - Schematic
