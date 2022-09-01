![](../../workflows/wokwi/badge.svg)

Go to https://tinytapeout.com for instructions!

# MicroASIC

There are 2 oscillators (3-stage and 5-stage). Oscillator are XOR-based, with second input tied to DFF chain to ensure it is not optimized away. 
Does not work in wokwi simulation - it just hangs. But it's totally ok to tapeout without simulation. 

DFF chain is set in a way that oscillators does not run without initialization. We need to push one "1" to enable both oscillators.
After each oscillator there are 4-stage counters to ensure the rest of circuit is slow enough to work. 

Then 2 MUXes allow to select ether external clock or 2 oscillators/16. 

Finally, there are 24-stage counter, with taps every 4 bit. 

All this will allow to measure frequency of internal oscillator despite slow IO.
