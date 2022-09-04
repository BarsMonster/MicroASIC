![](../../workflows/wokwi/badge.svg)

Go to https://tinytapeout.com for instructions!

# MicroASIC

There are 2 oscillators (3-stage and 5-stage). Oscillators are XOR-based, with second input tied to DFF chain to ensure it is not optimized away. 
Does not work in wokwi simulation - it just hangs. But it's totally ok to tapeout without simulation. 

DFF chain is set in a way that oscillators does not run without initialization. We need to push one "1" to enable both oscillators.
After each oscillator there are 4-stage counters to ensure the rest of circuit is slow enough to work. 

Then 2 MUXes allow to select ether external clock or 2 oscillators/16. 

Finally, there is 28-stage counter, with taps every 4 bit (32 bit total). 

All this will allow to measure frequency of internal oscillator despite slow IO.

# In pinout: 
```
0: clock in (for debugging)
1: Oscillator select (0 - 3XOR divided by 16, 1 - 5XOR divided by 16)
2: Enable additional x16 divider
3: shift register data (must shift in 5x 1 to enable oscillators)
4: shift register clock
6: debug (replaces 5XOR oscillator with clkin signal)
7: unused
```

# Out pinout: 
```
0: clock divided by 2^8 (regardles of in2)
1: clock divided by 2^8(12 if in2 is on)
2: clock divided by 2^12(16)
3: clock divided by 2^16(20)
4: clock divided by 2^20(24)
5: clock divided by 2^24(28)
6: clock divided by 2^28(32)
7: Bit 5 of shift register (to ensure it's not optimized away)
```

