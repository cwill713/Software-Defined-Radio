# Software-Defined-Radio-Reciever
This is the design of Software Defined Radio built in collaboration with Joshua Mularczyk for my Engineering Electronics II class

## Design Specifications
When perfroming research for this project, Joshua and I began to figure out what specifations our SDR would follow. Origianlly, we wanted to build a commercial FM radio, but after discusstion with Dr. Frohne, our professor, we reconsidered. The final specifications we decided on are as follows.
- Frequency Range: 8MHZ - 18Mhz
- Radio Type: Showrtwave
- One Butterworth Bandpass Filter
- One Tayloe Mixer
- One Bessel Lowpass Filter
- One Power Supply Noise Filter

## Schematics
The following are the initial schematics that Joshua and I have designed for the SDR.
### BandPass Filter
![image](https://user-images.githubusercontent.com/103695977/163806479-3e5f9cdf-7e73-47da-89b3-40038dfab9f3.png)
We built this filter using the LC Filter Design Tool found at https://rf-tools.com/lc-filter/. This is a Butterworth Filter that will on allow frequencies between 8MHz and 18MHz through it.

### Mixer
![image](https://user-images.githubusercontent.com/103695977/163806984-39671f89-a80e-467b-b468-739948fc7889.png)
The mixer that Joshua and I decided to use was  Tayloe Mixer. The Tayloe mixer uses switches to combined the signals that are 180 degrees out of phase with differential amplifiers so that signals above and below the oscilator frequecy can be detected.

### Lowpass Filter
![image](https://user-images.githubusercontent.com/103695977/163808794-6a4be6bf-b5aa-4a15-bba8-eb2360f31603.png)
Our Lowpass filter will block all frequencies greater that 100kHz.

### Voltage Smoother
![image](https://user-images.githubusercontent.com/103695977/163809129-1609780f-fa72-482c-b42a-1404d5a31d9e.png)
Our Voltage Smoother with take the the 5V coming in from the USB and remove all the noise the comes in from the computer and outputs a smoother 5V for the SDR to use.

### Arduino and Si5351
![image](https://user-images.githubusercontent.com/103695977/163809601-5b499e8b-3c42-4b21-aab6-d112a2c7a813.png)
Our Si5351 programmable oscillator will allow us to input two clock signals that are 90 degrees apart into S0 and S1 of the SN74CBT3253. The Arduino Nano will controll the frequency the is put out by the Si5351 for tuning.

## Simulations
The Following are the simulations of our filters as we have not yet fully simulated the SDR as a whole.

### Bandpass Filter
![image](https://user-images.githubusercontent.com/103695977/163806294-b24794c1-b576-47e0-a262-90af70f5b265.png)
![image](https://user-images.githubusercontent.com/103695977/163810045-d9e52c8f-7157-414a-8c3d-9e4d7e16fb39.png)

### Lowpass Filter
![image](https://user-images.githubusercontent.com/103695977/163810193-a9069945-3c7c-4594-b9f1-aa382b970d71.png)
![image](https://user-images.githubusercontent.com/103695977/163810300-0baa7ec9-fe0b-4580-a687-907685373d8e.png)


