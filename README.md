# Software-Defined-Radio-Reciever
This project, assigned to us by [Dr. Frohne](https://github.com/frohro), combines our professors' interest HAM radio and a practical application of gain, opamp analysis, noise, and AC/DC analysis that we learned in Electronics I. This is the design of Software Defined Radio built in collaboration with [Joshua Mularczyk](https://github.com/JoshuaMularczyk) for our Engineering Electronics II class.

## Design Specifications
When perfroming research for this project, Joshua and I began to figure out what specifations our SDR would follow. Origianlly, we wanted to build a commercial FM radio, but after discusstion with Dr. Frohne, we reconsidered. The final specifications we decided on are as follows:
- Frequency Range: 7MHZ - 18MHz
- Radio Type: Shortwave
- Inexpensive
- No Noise


The subcirucits used to create this SDR are: 
- Butterworth Bandpass Filter
- Tayloe Mixer
- Bessel Lowpass Filter
- Power Supply Noise Filter
- 2.5V Voltage Bias
- Arduino Controlled Oscillator

## Theory

<img width="634" alt="blockdia" src="https://user-images.githubusercontent.com/103919092/172436558-2e65173e-d889-476e-afc4-3da0d40f0bdf.PNG">

## Schematics
The following are the initial schematics that Joshua and I have designed for the SDR.

### BandPass Filter
![BandPass Filter and Voltage Divider](https://user-images.githubusercontent.com/103695977/172123798-0871c234-771f-46bd-9502-651a71eb86e6.jpg)
We built this bandpass filter using the [LC Filter Design Tool](https://rf-tools.com/lc-filter/). This is a Butterworth Filter that will only allow frequencies between 8MHz and 18MHz to pass through it.

The voltage divider will take our Filtered 5V and output a 2.5 DC voltage to drive the rest of the circuit. 

### Mixer and Lowpass Filter
![Tayloe Mixer](https://user-images.githubusercontent.com/103695977/171759381-e49fd43a-300a-4075-a9eb-c46a4cfd6736.jpg)
The mixer that Joshua and I decided to use was  Tayloe Mixer. The Tayloe mixer uses switches to combined the signals that are 180 degrees out of phase with differential amplifiers so that signals above and below the oscilator frequecy can be detected.

The lowpass filter will block all frequencies greater that 100kHz.

### Voltage Smoother
![Voltage Smoother](https://user-images.githubusercontent.com/103695977/171760121-b3ce913d-ab7f-4082-ad9f-a03cbcf7cb58.jpg)

The Voltage Smoother with take the 5V Vcc and remove as much noise as possible that comes in from the computer and outputs a smoother 5V for the SDR to use.

### Arduino and Si5351
![Arduino and Si5351](https://user-images.githubusercontent.com/103695977/171760493-9e65d962-7504-4b07-9917-c7026b6bcaa2.jpg)
The Si5351 programmable oscillator will allow us to input two clock signals that are 90 degrees out of phase into S0 and S1 of the SN74CBT3253. The Arduino Nano will control the frequency the is put out by the Si5351 for tuning.

## Simulations
The following are the simulations of our filters and our SDR as a whole.

### Bandpass Filter
![Bandpass Filter Simulation Graph](https://user-images.githubusercontent.com/103695977/172128945-2436fb08-f1e6-4906-a7a6-28c304c560f3.jpg)
![Bandpass Filter Simulation](https://user-images.githubusercontent.com/103695977/172128985-f59a6ec8-1b1a-4b8a-a930-dfc2ace7611d.jpg)


### Lowpass Filter
![LowPass Filter Simulation](https://user-images.githubusercontent.com/103695977/172126680-7654ed1c-1729-4d28-b0ac-22c0453f8cd5.jpg)
![LowPass Filter Schematic](https://user-images.githubusercontent.com/103695977/172126698-47ae7323-1dd5-43b3-99ac-888cf9888982.jpg)

### Complete SDR
![Complete Simulation Graph](https://user-images.githubusercontent.com/103695977/172208557-2a06cd88-0c1e-46c1-88f6-4b392ef950bf.jpg)
![Complete SDR Simulation](https://user-images.githubusercontent.com/103695977/172208710-ec5d7ed2-cf76-4863-a852-ea123d72f428.jpg)


## Project Results
My partner and I each designed our own version of our board, but my partner had the better board layout. So we used his V5 of our schematic, PCB, and drill files and sent them to our professor who sent our files to [JLPCB](https://jlcpcb.com/VGS?utm_source=gg_vgs&utm_medium=cpc&gclid=Cj0KCQjwqPGUBhDwARIsANNwjV4Y9aU908uwwHsgXCAJ3L9PZ44l-hPgCvsU4kgto-ll1H0iRJroh1UaAsKwEALw_wcB) for printing. We then ordered that parts needed then constructed and tested our board. 

### Initial Testing
During the initial testing, we found that we had a wiring issue in our mixer, we were missing our ground plane on our gerber, and we didn't have our second set of opamps between +/- Vcc. We fixed these issues by cutting and jumping traces and manually wiring our grounds together. PUT LINK TO PICTURES. We fixed these issues in [V6](https://github.com/cwill713/Software-Defined-Radio/tree/main/Schematic%20Files/SDRrecV6).

### Minimum Discenable Signal
When testing to see the minimum discernible signal we connected our board up to our signal generator, our system running quisk software, and our soundcard. We adjusted the attenuator on the signal generator to output a signal of 14MHz and adjusted the attenuator to see how small of a signal we could detect. In the image below, we see our radio discern a signal of 3.5uV!
![minDecV2](https://user-images.githubusercontent.com/103695977/171743162-00ffc03b-b354-496b-b6c2-f4261597c40c.png)

### Practical Test
Next, we decided to see if we could find any bandwidths where people were talking and try to listen in. We found two bandwidths being used for communications.

The first was being used to communicate the weather from what we are assuming to be an air traffic control tower. 

![weather](https://user-images.githubusercontent.com/103695977/171746787-f60b8dcc-d91d-4fa2-9dc1-e9d8d79bb7dc.png)
"Wind 360 degrees, light drizzle, visibility more than 6 miles".

The second bandwidth was being used by two HAM Radio operators talking about how another station send out a signal that interfered with their own.
![listeningIn](https://user-images.githubusercontent.com/103695977/171746851-dc1fa95d-337f-405f-911d-0fd728108ca7.png)
