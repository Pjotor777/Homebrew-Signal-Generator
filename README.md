# Homebrew Signal Generator

Update 2026-05-23: project in progress, currently revising readme, and working on the final version 1 PCB.
I also plan on beginning version 2, using more sophisticated components and improving performance over v1.

## Abstract
A basic analog signal generator circuit that generates the 4 fundamental waveforms (Square, Sine, Triangular and Sawtooth). The generator was built using only passive components (resistors, capacitors and diodes) and operational amplifiers. The generator has a fixed frequency (phase locked), oscillating at 1 kHz.

The project has 3 phases (no pun intended!): 
1. Theoretical learning and design via LTspice (Current phase, 99% complete).
2. Prototyping in a laboratory environment.
3. Developing the hardware as a PCB via KiCad.

### Contents
There are 2 files containing the circut. The first one: 'multi-wave-osc' is the basic 'default' circuit built with LTspice's Universal Opamp 2 components. The second one 'multi-wave-sc-lt1364' is the 'main' circuit for testing and prototyping. Fundamentally, they are the same circuit but with some minor differences to account for the behavior of the op-amps used.

All relevant images can be found in the 'images' folder. The folder contains images of the 2 circuits, the waveform outputs of each oscillator (outputs based off the 'main circuit') and the spectrum analysis (FFT plots) of all waveforms together.

I also added a second file, (noted with the number 2) where I will experiment (in the meantime) on some basic optimizations, such as using better filtering methods in the sine wave generator, and attempting to cut out the anti-clipping voltage divider. Work in progress.

Work in progress: more info will be added shortly along with the project updates.

## Functionality
### Square Wave Generator
The square wave generator functions as the main core of the circuit, providing both for itself, the sine and the triangle wave generator, and serves as a synchronization source for the sawtooth wave generator.

The square wave generator is based off a typical RC (resistor-capacitor) relaxation oscillator. As the oscillator is powered on, the output of the op-amp goes into saturation (generally, positive but it can go into negative saturation as well). As the capacitor charges to Vcc (in our case, 5V), the output remains the same. With time constant RC, the capacitor begins charging towards 5V. When the capacitor voltage reaches one half of the supply voltage, the op-amp switches into the negative (or positive) saturation. In general, the op-amp functions as a Schmitt trigger. Then, the capacitor begins discharging in the same way, repeating the process. 

This particular oscillator has a period of 2.2RC, independent of the supply voltage, and is able to cycle indefinitely provided it has a stable supply voltage. This can be seen clearly in the 'default-circuit' as it uses ideal universal op-amps. The same functionality is seen in the main circuit using actual commercial op-amps, with a smaller amplitude due to actual constraints from real environment variables such as manufacture error, temperature, etc.

### Sine Wave Generator
Work in progress
### Triangle Wave Generator
Work in progress
### Sawtooth Wave Generator
Work in progress

## Images
Images will be posted here. For now, they can be found in the images folder as mentioned earlier

## Future Work
Once the project is (at least, mostly) complete, I plan on possibly making a 'version 2' of the signal generator, including more robust methods of waveform generation, using potentiometers to allow for lower and higher frequencies (and amplitudes? if that is even possible) and more advanced waveforms found in modern signal generators.