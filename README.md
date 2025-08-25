# Common Emitter BJT Amplifier – Gain Response (LTSpice)

This is a small common-emitter amplifier I built and simulated in LTSpice to get a feel for its frequency response and bandwidth. I’ve included everything you’d need to open the circuit and reproduce the plots.

## Overview
The amplifier uses a 2N3904 in a classic common-emitter configuration with a resistive divider for bias, an emitter resistor for stability, and a bypass capacitor to boost midband gain. I ran an AC sweep to see where the gain starts to roll off on both ends and to estimate the bandwidth.

## Schematic and Parts
- 2 voltage sources:  
  V1 = AC input source  
  V2 = 12 V DC supply
- 3 capacitors:  
  C1 = 1 µF (input/decoupling)  
  C2 = 100 pF (output snubber/small cap for HF behavior)  
  C3 = 20 µF (emitter bypass)
- 4 resistors:  
  R1 = 10 kΩ (bias divider, upper)  
  R2 = 100 kΩ (bias divider, lower)  
  R3 = 20 kΩ (collector load)  
  R4 = 1 kΩ (emitter resistor)
- 1 transistor:  
  Q1 = 2N3904 (NPN)

Input goes through C1 into the base. R1 and R2 form the bias network. The collector connects to +12 V through R3. The emitter goes to ground through R4 in parallel with C3. Output is taken at the collector and routed through C2.

## Circuit preview
<img width="1920" height="1080" alt="BJT Amplifier" src="https://github.com/user-attachments/assets/1877daa9-1f05-4e0d-badc-9ac4f747f062" />

## Simulation setup
AC analysis with an octave sweep:
- Start frequency: 1 Hz
- Stop frequency: 10 MHz
- Points per octave: 10

I measured gain using voltage markers at the input and the AC-coupled output node.

## Results and notes
- Low-frequency corner (approx): 256.16 Hz  
- High-frequency corner (approx): 47.87 kHz  
- Bandwidth (approx): 47.6 kHz

The gain is flat across the midband and starts to drop below a few hundred hertz due to the coupling/bypass network. On the high end, the small capacitor and device parasitics pull the response down around a few-tens of kilohertz. Bypassing the emitter with C3 noticeably lifts midband gain compared to leaving it unbypassed.

## Gain plot
<img width="1920" height="1080" alt="Gain Response" src="https://github.com/user-attachments/assets/26832a1d-1b89-47d2-8b4c-5ef9a3ef9224" />

## How to reproduce
1. Open the .asc file from the Circuit Files folder in LTSpice.  
2. Run an AC Analysis with the sweep: 1 Hz → 10 MHz, 10 points/octave.  
3. Add voltage markers at the input and at the AC-coupled output node (after C2).  
4. Plot Vout/Vin (in dB) to see the frequency response and estimate the corners.

## Things to try next
- Sweep C1 and C3 to see how the low-frequency pole shifts.  
- Try different collector loads (R3) and note the gain/linear headroom trade-off.  
- Replace the 2N3904 with other small-signal BJTs and compare fH.  
- Add a proper load (e.g., 10 kΩ to ground after C2) to reflect a real stage/input.

## Files and folders
I’ve uploaded all the circuit files in the folder named Circuit Files and all the images in a folder named Images.
