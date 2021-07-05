### As of 2021/07/02:  
**This project has a working implementation of an (FFT-powered) audio spectrum analyzer with direct input from a 3.5mm jack.  Currently assembling amplifier and speaker components to begin the audible part of the project.**

# FFT-Audio-Speaker-MCU
A custom bluetooth speaker project conceived from an FFT mini-project.  This MCU version serves as a test bed for the FPGA version.

![Audio Spectrum Display Closeup](https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/video/IMG_1387.gif)

## Table of Contents
1. Overview
2. Feature List
3. Future Changes
4. Issues
5. List of Components and Tools
   - Hardware
   - Software
6. Derived Sources
   - shajeebtm's 32-Band Audio Visualizer Arduino Project
   - ForceTronics: Advanced Configuration of the SAMD21 ADC
7. Schematic Diagram
8. References
   - Source Code/Hardware Inspiration
   - Documentation
   - Technical Guides
   - Theory
   - Other


<a href="MKR Zero and Nano Version Comparison"><img src="https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/video/IMG_1230.gif" align="center" width="500"></a>

## 1. Overview

<a href="Board Overall View"><img src="https://github.com/Gunmetal-61/FFT-Audio-Speaker-MCU/blob/gh-pages/images/IMG_1381.jpeg" align="center" width="500"></a>

## 2. Feature List

## 3. Future Changes

## 4. Issues

## 5. List of Components and Tools

### Hardware

### Software

## Derived Sources

### shajeebtm's 32-Band Audio Visualizer Arduino Project

### ForceTronics: Advanced Configuration of the SAMD21 ADC

## Schematic Diagram

## References

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

<br />

_Last Updated: 2021.07.04 19:32 PST_
