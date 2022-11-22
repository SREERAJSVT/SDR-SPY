# SDR-SPY
ESP32A1S Based Stantalone SDR 

The article is being published in collaboration with JLCPCB. They supply high quality PCBs at a very reasonable price. They also can provide SMT circuit assembly.

We thanks to our sponsor JLCPCB https://jlcpcb.com/RTA for sponsoring us PCBs for this project circuit.

Thanks To JLCPCB.

$2 for 1-4 Layer PCBs.

Get SMT Coupons: https://jlcpcb.com/RTA



ESP32A1S AMATER RADIO & AUDIO DEV TOOL

![alt text]( https://github.com/SREERAJSVT/SDR-SPY/blob/main/EasyEDA(Standard)%206.5.22%20-%20Team%20Work%20mode%2022-11-2022%2012_01_53.png)
![alt text](https://github.com/SREERAJSVT/SDR-SPY/blob/main/EasyEDA(Standard)%206.5.22%20-%20Team%20Work%20mode%2022-11-2022%2013_51_07.png)



Amateur Radio in the world until now is still growing even with various organizational platforms even though along with other technological developments, Amateur Radio fans also do not subside with its various innovations. One of them is Amateur radio which uses a High Frequency path of 3 to 30 Mhz called the SSB line.



The modern version of two contain expansion header pins used to developing all projects
The VU3UCK design contain Air spy SDR software can control.
I&Q Input, Output inbuilt.
Users on the High Frequency 3 - 30 Mhz line use several modes both for receivers and transmitters, namely AM, LSB, USB, CW and so on. The types of radios or devices used also vary, both digital and analog. The development of user innovations that have been organized independently has shown very remarkable results utilized by other users.

I myself also carry out experiments on the development of radio techniques when there is an opportunity to carry them out in addition to daily work. The experiment I am working on is to develop a radio unit that can be used at a low cost and according to my own wishes.

This stand alone Radio SDR SSB Tranceiver was inspired by when it was in a crowded circle among amateur radios, namely a radio called uSDX stand alone 5 watts using an atmega328 processor by squeezing out its capabilities, usdx using the Front End Tayloe detector and the signal processing was done by the DSP method, processing the mode by flipping the input phase quadrature oscillator 0 and 90 degrees, uSDX itself continues to upgrade its versions when there are improvements.



Similar to uSDX, Stand alone SDR SSB Radio HF Tranceiver is upgradable, which can be adjusted again in terms of software with reviews and things that can improve capabilities and also fix bugs found later.

My attention glanced at an ESP32 processor from espressif which at the time of writing this article the market price was still below 100 rebu. ESP32 has an integrated dual Core, which is like having 2 processors, the clock can be set up to 250Mhz, usdx atmega328 itself is only 20Mhz clock, so in my opinion if the ESP32 is right for a replacement atmega328 it will be very capable. This time the control function I use is to take advantage of the Touch Screen TFT LCD ili9341 feature so that it does not use a rotary encoder or other button buttons. With the exception of PTT by utilizing only one input from the ESP32.



The method I used at the time of receiving was to extract phase I Q from one side of the FST3253 Tayloe Detector IC with the ESP32 wroom algorithm as the processor DSP, then by shifting the audio phase by 90° by (-45° and 45°) respectively using the FIR filter coeff hilbert transform, Freg Center 1.8khz Bandwith 5khz, this time the sample 48.0 khz 24 bit ADC this time using the I2S Codec PCM1802 module, DAC output with I2S CS4344 Codec, (the use of other types of I2S Codec is also very possible) after which the result is filtered using the Biquad IIR filter coeff to determine the bandwidth, When in the process of shifting the following phase and extracting the audio stream to be processed into FFT which will be displayed on the TFTLCD Graphic. Selection of USB (Upper Side Band) and LSB (Lower Side Band) modes by flipping the audio input of the Hilbert transform FIR filter.



Tranceiver.

     The method I used at the time of transmitter was to extract audio from the condenser mic, the ESP32 wroom algorithm as the DSP processor processed by shifting the audio phase by 90° by (-45° and 45°) respectively using a FIR filter coeff hilbert transform sample 48.0 khz 24 bit ADC using the PCM1802 module, output a DAC with the I2S CS4344 module, then divide it into 4 signals that have 4 signals that have 4 Different phases using the TL084 IC produce a quadrature I Q shape that is processed on one side of the IC FST3253 Tayloe Detector which will be strengthened by a power amplifier rf buffer/driver.  



Quadrature Oscillator.

    Ic FST3253 requires two Local Oscilator inputs that have phases 0 and 90 degrees to be able to produce In Phase and Quadrature or I and Q outputs. therefore, the one that gets the task as a local oscillator is the SI5351 by utilizing its two outputs. One of the outputs must have a phase of 0 degrees and the output of one has a phase of 90 degrees. This can be done by programming si5351 through its coding, as can the methods used by uSDX. The experience that I have practiced using esp32 sometimes occurs phase error when in the tuning process switch frequency so that the determination of LSB and USB modes will be not optimal.

Another alternative is to use a flip flop divisor IC which with 1 input produces 2 different inputs of 90 degrees phase. This time I used the SN74F74 flip flop IC type with the frequency input used is 4 times the desired frequency. Why do I use type F, this is because type F is an IC type DIP not SMD for ease of soldering and can handle input frequencies up to 125 Mhz, be careful with this because the example type SN74LS74 is the same as 74 but type LS can only handle up to 20Mhz only, to be able to operate in the range of 1 - 30 Mhz must use type SN74F74 or SN74AC74

L1 is an RF Phase Splitter by rolling a 0.7 mm email wire on the T50-6 or T50-2 toroid for 8 rounds, two of which are used as center tops. During the experiment I used a makeshift used email wire and sometimes didn't know the size but all of them managed to split the rf phase according to the measurement results in the Instructor brand USB Oscilloscopes.

Example implementation with all controls and settings using touchscreen LCD except PTT.

This time the AGC (Automatic Gain Controller) system was due to moment so I eliminated it and I replaced the DRC (Dynamic Range Compression) system with On and Off options so that the reception of large and small modulated radio stations became almost flat, considering that the average HF radio fan was old including me so as not to be surprised if suddenly there was a surprising modulation.

If you want to experiment with the following Bin, Schematic and PCB files

FT8. The addition of FT 8 features by adopting Cat Control with the Icom746 Protocol is inserted in the Possessor coding. USB Serial TTL as Cat Controller, Pins used are GND, data RX and data TX. It is planned to adopt Cat Command from Kenwood TS-2000 to make it more flexible to use with Power SDR software and others.



The article is being published in collaboration with JLCPCB. They supply high quality PCBs at a very reasonable price. They also can provide SMT circuit assembly.

We thanks to our sponsor JLCPCB https://jlcpcb.com/RTA for sponsoring us PCBs for this project circuit.

Thanks To JLCPCB.

$2 for 1-4 Layer PCBs.

Get SMT Coupons: https://jlcpcb.com/RTA





Special Thanks NA5Y,YD1GSE,VU3ZOF,JLCPCB.



MORE DETAILS AND PROGRAM COMINSOON

 
