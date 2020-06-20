 # ```apitran improved```
A Linux toolkit for handling signals recieved from NOAA satellites over the automatic picture transmission (APT) protocol.


Original apitran code by github user rsj56, this version has some added features such as picture sharpening.

## Intro to Automatic Picture Transmission
Automatic picture transmission (APT) is an analog image transmission format developed for use on weather satellites in the 1960s. While only three modern satellites, NOAA 15, NOAA 18, and NOAA 19, transmit on the APT protocol, building a reception station is cheap and simple. The images can be quite high quality—they natively have a resolution of 4 km/px. It is reasonable to expect at least one good-quality satellite pass (and, thereby, opportunity for image downlink) per day. 

### Transmission
The transmitting antennae aboard the satellites are linearly polarized. However, the satellites spin as they orbit, creating an effectively right-circularly polarized signal. The signal has 256 levels, which are amplitude-modulated onto a 2.4 kHz subcarrier, which is then frequency-modulated onto a 137-MHz band RF carrier. The overall RF bandwidth is 34 kHz. The signal is broadcast at 37 dBm (~5 W) ERP. The specific center frequency depends on the satellite:

* NOAA 15 — 137.6200 MHz
* NOAA 18 — 137.9125 MHz
* NOAA 19 — 137.1000 MHz

### Reception
To recieve, it is normally okay to use a passive antenna with no tracking (especially if a circularly polarized antenna is used). Some common antenna choices:

* Quadrifilar helix (QFH)
* Double crossed dipoles

The most common choice of receiver is probably the RTL-SDR. There are multiple options on the software side. If you are using apitran, it means you are running Linux and so I recommend Gqrx. 

## Getting Started with ```apitran improved```

### Dependencies
```apitran improved``` requires the following packages as dependencies:

* ```sox```

And Python modules:

* ```PIL```
* ```sys```
* ```numpy```
* ```scipy```
* ```subprocess```
* ```argparse```
* ```imageio```

### Installation
1. Clone ```apitran improved``` to your directory of choice. 
2. Navigate to the ```./apitran-improved/``` directory and run ```pip install -r ./requirements.txt```
 

## Using ```apitran improved```
Here, we will go through all of the functions available to use with ```apitran improved```. In general, these flags can be stacked.

### ```-d --decode input_filename```
Use this flag to decode a .wav recording of an APT signal. The .wav can be any number of channels, at any samplerate—the software will do any necessary conversions. The decoded image will be displayed using your default image viewer. Unless output filename is specified using ```-o```, this output will not be saved automatically. 

### ```-o --output output_filename```
Given a flag which creates output, this flag can be used to override the default output location. 

### ```-s --sharpen```
Use this flag to add sharpening to the output. Default value is 1, values smaller than 1 will produce blurred images and values greater than 1 will produce sharpened images.

### ```-c --combine```
Use this flag to combine the 2 channels the satellites send to one

### ```-C --contrast```
Use this flag to add contrast enhancement to the output. Default valie is 1, values smaller than 1 will produce reduced contrast images and values greater than 1 will produce higher contrast images.

### ```-f --filter```
This flag will apply a bandpass filter to the signal before processing, this may improve image quality and remove artefacts in some cases.
