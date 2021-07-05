### As of 2021/07/02:  
**This project has a working implementation of an (FFT-powered) audio spectrum analyzer with direct input from a 3.5mm jack.  Currently assembling amplifier and speaker components to begin the audible part of the project.**

# FFT-Audio-Speaker-MCU
A custom bluetooth speaker project conceived from an FFT mini-project.  This MCU version serves as a test bed for the [FPGA version](https://github.com/Gunmetal-61/FFT-Audio-Speaker-FPGA).

![Audio Spectrum Display Closeup](https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/video/IMG_1387.gif)

<br />

## Table of Contents
1. [Overview](#1-Overview)
2. [Feature List](#2-Feature-List)
3. [Future Changes and Additions](#3-Future-Changes-and-Additions)
4. [Issues](#4-Issues)
5. [List of Components and Tools](#5-List-of-Components-and-Tools)
   - [Hardware](#Hardware)
   - [Software](#Software)
6. [Derived Sources](#6-Derived-Sources)
   - [shajeebtm's 32-Band Audio Visualizer Arduino Project](#shajeebtms-32-band-audio-visualizer-arduino-project)
   - [ForceTronics: Advanced Configuration of the SAMD21 ADC](#forcetronics-advanced-configuration-of-the-samd21-adc)
7. [Schematic Diagram](#7-Schematic-Diagram)
8. [References](#8-References)
   - [Source Code/Hardware Inspiration](#source-code/hardware-inspiration)
   - [Documentation](#documentation)
   - [Technical Guides](#technical-guides)
   - [Theory](#theory)
   - [Other](#other)

<br />

## 1. Overview

This project began as a side project to a side project in understanding and implementing Discrete Fast Fourier Transforms (DFFTs) in FPGAs.  I figured, why not give it a real application and plug an audio signal in to be visualized?  And here we are.  In the image below, I have an Arduino MKR Zero connected to an analog 3.5mm audio signal sampled at ~20 KHz (for a max frequency detection range of 0-10 KHz) with an adjustable sample count from 8 to 256 for 4 to 128 columns on the visualizer.

This repository contains the microcontroller version of what I hope to eventually [implement in an FPGA in this repository](https://github.com/Gunmetal-61/FFT-Audio-Speaker-FPGA).  It is faster to develop and experiment with MCUs first as the toolset is less complex, and I am already more familiar with them.  Currently, I am looking to add a user interface to this audio spectrum visualizer and turn it into a full-fledged custom wireless/wired speaker of my own design.

<br />

<a href="Board Overall View"><img src="https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/images/IMG_1381.jpeg" align="center"></a>

_The prototype board as of 07.03.2021.  The device with the larger screen cut off at the top of the frame is an [Arduino Mega 2560-based Oscilloscope](https://create.arduino.cc/projecthub/wayri/arduino-oscilloscope-84b2ac)_

<br />

## 2. Feature List

- Real-Time Audio Visualization with Adjustable Frequency Range and Number of Columns
- Dual SSD1306 Displays
- Battery-Powered, micro-USB Rechargeable
- Audio Signal Input via 3.5mm Jack

<br />

## 3. Future Changes and Additions

The wireless speaker and UI portions of the code have yet to be added.  Additionally, it is a long ways off, but I am already beginning to sketch designs and choose final hardware for a polished, custom-PCB-and-enclosure version of this project.

Please look at the [project board](https://github.com/users/Gunmetal-61/projects/1) for a more accurate day-to-day view of current issues and features being worked on.

<br />

## 4. Issues

Right now, the project contains a functioning audio spectrum visualizer, but parameters to adjust the view can only be tweaked in source code.  Additionally, the spectrum graph shows varying amounts of "noise" depending on how clean the audio signal and power source are.  This has yet to be fully resolved and may not be possible without reconfiguration and addition of more hardware (decoupling capacitors have already been added).

Please look at the [project board](https://github.com/users/Gunmetal-61/projects/1) for a more accurate day-to-day view of current issues and features being worked on.

<br />

## 5. List of Components and Tools

### Hardware

- [Arduino MKR Zero](https://store.arduino.cc/usa/arduino-mkrzero)
- 3.7v 2300 mAh LiPo Battery with 2-pin JST connector (optional if desired for project to not require USB power all the time)
- 2x [SSD1306 128x64 I2C 0.96" OLED Display](https://www.aliexpress.com/item/32957392300.html?spm=a2g0s.9042311.0.0.27424c4dz9fnHf)
- [SparkFun TRRS 3.5mm Jack Breakout](https://www.sparkfun.com/products/11570)
- Breadboard
- 3x 5.1 KOhm In-Line Resistors
- 2x 100 KOhm In-Line Resistors (for audio signal voltage divider)
- 4x 10 KOhm In-Line Resistors (for pulldown purposes with the buttons)
- 2x 100 nF Capacitors
- 4x Pushbutton Switches

### Software

- Arduino IDE
- Arduino Libraries
   - [arduinoFFT](https://github.com/kosme/arduinoFFT)
   - [Adafruit_SSD1306](https://github.com/adafruit/Adafruit_SSD1306)
   - [Adafruit_GFX](https://github.com/adafruit/Adafruit-GFX-Library)

<br />

## 6. Derived Sources

### shajeebtm's 32-Band Audio Visualizer Arduino Project

I initially started this project off with the code and hardware components/config from [this repository](https://github.com/shajeebtm/Arduino-audio-spectrum-visualizer-analyzer).  There is also an [Arduino Project Hub writeup](https://create.arduino.cc/projecthub/shajeeb/32-band-audio-spectrum-visualizer-analyzer-902f51).

I then proceeded to heavily modify the project.  I subdivided the code into logical functions and made the FFT visualizer much more parameterizable (adjusting the number of columns samples, etc.).  Instead of using a MAX7219-driven 32x8 LED matrix, I used a 128x64 SSD1306 OLED display (I2C version).  The code has also been ported over to the Arduino MKR Zero which uses an entirely different microcontroller.  This provides far more power and memory to support the higher resolution display and faster FFT calculation with more samples.

In the images on this README, four buttons and a second SSD1306 display can also be seen.  These will support a future UI to adjust parameters of the FFT visualizer and control the future Bluetooth speaker functionality of this project.

It is worth mentioning while shajeebtm's project is capable of displaying all frequency ranges up to about 18KHz, I have (temporarily) intentionally set my max frequency at roughly 10KHz as the majority of the audio signal does not go beyond this range.

<br />

<a href="MKR Zero and Nano Version Comparison"><img src="https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/video/IMG_1230.gif" align="center"></a>

_A quick-and-dirty early prototype I made my code running on both a MKR Zero (top) and Nano (bottom).  Notice the MKR Zero's display shows 64 audio columns while the Nano only has 16.  This is because the latter does not have enough dynamic memory nor speed to hold and do work any more ADC samples required for the FFT.  It was possible for shajeebtm's project to display 32 columns on a Nano, but that is because his LED matrix requires less memory to be driven than a 128x64 display._

<br />

### ForceTronics: Advanced Configuration of the SAMD21 ADC

Switching from the Arduino Nano to the MKR Zero requires a significant rewrite of the code which configures the sampling rate of the ADC.  The default Arduino ```analogRead()``` function does not sample at a rate fast enough for an appreciable frequency range to be detected by the discrete FFT algorithm.  In other words, the audio spectrum visualizer would probably only display frequency bars up to about 1KHz.  In order to fix this, the prescaler value set for the ADC must be changed.  The prescaler value divides the system clock speed by a power of 2.  

Depending on the bit resolution the ADC is set at (8, 10, or 12 bits), each analog to digital conversion will take 5-7 clock cycles.  In order to calculate the sampling rate, the formula is as follows:

**Sampling Rate = SAMD21 Clock Speed / (Prescaler Value x Conversion Clocks Needed)**

Doing this is very simple with the ATMega328P on an Nano, but is a much more involved process on a SAMD21 the MKR Zero has.  I followed the videos and code provided by a guide found [here](https://forcetronic.blogspot.com/2018/06/speeding-up-adc-on-arduino-samd21.html).

Please refer to the [Source Code/Hardware Inspiration](#source-code/hardware-inspiration), [Documentation](#documentation), and [Technical Guides](#technical-guides) section found at the bottom of this README in [8. References](#8-References).

<br />

## 7. Schematic Diagram

As the project's hardware configuration is still in flux with many components to be added, there is no diagram here.  However, it should be sufficient to follow the schematic shown on [shajeebtm's project page](https://create.arduino.cc/projecthub/shajeeb/32-band-audio-spectrum-visualizer-analyzer-902f51).  Just replace the Arduino Nano for the MKR Zero and substitute the SSD1306 for the MAX7219 on the I2C bus.  Refer to the comments in the code to figure out which pins the I/O has been likewise re-mapped to.

As the MKR Zero is all 3.3V logic, connect the wire which links 5V to the **display mode** button to the MKR Zero's 3.3V power pin instead.

<br />

## 8. References

### Source Code/Hardware Inspiration
 - Arduino 32 Band Audio Spectrum Visualizer / Analyzer - shajeebtm
   - [GitHub](https://github.com/shajeebtm/Arduino-audio-spectrum-visualizer-analyzer)
   - [Arduino Project Hub Writeup](https://create.arduino.cc/projecthub/shajeeb/32-band-audio-spectrum-visualizer-analyzer-902f51)
 - Speeding up the ADC on Arduino SAMD21 Boards (Zero, Mkr, etc) - ForceTronics
   - [Source Code](https://forcetronic.blogspot.com/2018/06/speeding-up-adc-on-arduino-samd21.html)
   - [YouTube Video with Detailed Explanation and Code Breakdown (Part 1)](https://www.youtube.com/watch?v=glulIeL2lxA)
   - [Video Part 2](https://www.youtube.com/watch?v=Yb5vpLIFWOM)

### Documentation
 - Microcontroller Data Sheets
   - [Atmel SAMD21](https://ww1.microchip.com/downloads/en/DeviceDoc/SAM_D21_DA1_Family_DataSheet_DS40001882F.pdf) - Used in the Arduino MKR Zero in this project.
     - Refer to Ch. 33 (starting at page 781) for information about the ADC.  A diagram of the registers you'll likely need to manipulate to adjust the sample rate as ForceTronics' guide suggests is on page 782.
   - [Atmel ATmega328P](https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf) - Used in the Arduino Nano in shajeebtm's project.
     - Refer to Ch. 23 (starting at page 205) for information about the ADC.  The register you'll need to change to adjust the sample rate (via the prescaler) is ADCSRA.
 - SSD1306 OLED Display
   - [Adafruit SSD1306 Arduino Library API/Class Reference](http://adafruit.github.io/Adafruit_SSD1306/html/class_adafruit___s_s_d1306.html)

### Technical Guides
- SAMD21 ADC
  - [Getting the Most out of the SAM D21's ADC - Stargirl Flowers](https://blog.thea.codes/getting-the-most-out-of-the-samd21-adc/) - Conversion Time Calculator Enclosed
  - [Reading Analog Values with the SAMD21's ADC - Stargirl Flowers](https://blog.thea.codes/reading-analog-values-with-the-samd-adc/)
- Device Communication Protocols
  - I2C
    - [Using the I2C Bus - Robot Electronics](https://www.robot-electronics.co.uk/i2c-tutorial)
    - [I2C - sparkfun](https://learn.sparkfun.com/tutorials/i2c)
    - [I2C： What's That? - I2C Bus](https://www.i2c-bus.org/)
  - SPI
    - [Serial Peripheral Interface (SPI) - sparkfun](https://learn.sparkfun.com/tutorials/serial-peripheral-interface-spi/all)
  - [SPI vs I2C Protocols - Pros and Cons](https://www.arrow.com/en/research-and-events/articles/spi-vs-i2c-protocols-pros-and-cons)

### Theory
- Understanding Fast Fourier Transforms
  - [Seeing Circles, Sines, and Signals: A Compact Primer on Digital Signal Processing - Jack Schaedler](https://jackschaedler.github.io/circles-sines-signals/index.html)
  - [An Interactive Guide To The Fourier Transform - BetterExplained](https://betterexplained.com/articles/an-interactive-guide-to-the-fourier-transform/)
  - [Four Ways to Compute an Inverse FFT Using the Forward FFT Algorithm - Rick Lyons, DSPRelated](https://www.dsprelated.com/showarticle/800.php)
- Digital Audio
  - [Digital Audio Basics: Audio Sample Rate and Bit Depth - Griffin Brown, iZotope](https://www.izotope.com/en/learn/digital-audio-basics-sample-rate-and-bit-depth.html)

### Other
- [Arduino MKR Vidor 4000](https://store.arduino.cc/usa/mkr-vidor-4000) - Another MKR-series board that looks very interesting as it also contains a Intel Cyclone 10CL016 FPGA to supplement the SAMD21 MCU, more I/O, and wireless radios.  I am considering switching to this board in the future for expansions of this project.

<br />

_Last Updated: 2021.07.04 23:13 PST_
