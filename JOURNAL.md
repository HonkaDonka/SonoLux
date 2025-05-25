# Launchpad
A reactive 8x8 capacitive Launchpad
> I can't think of a better name so this will be it for now

## June 24: Research
I'm planning on using an ESP32 I have lying around for the MCU. Although it has 10 capacitive touch GPIOs, an 8x8 grid warrants 64 of them. Originally I was planning on using the MPR121 capacitve touch IC, but it only has 4 I2C addresses and each chip supports 12 channels, making it able to support a maximum of 48 touch pads (less than 64). For now, I'm planning on bypassing this by adding another I2C bus. 

Regarding lighting, I'm planning on using WS2812B LEDs because they are addressable and I have experience programming them already (Check out my HonkaCube project!)
For WAV/MP3 playback, I have an SD card module (no SD card though😔).

Next up:
Perhaps prototype a 1x1 LED + capacitive sensing (using ESP32's built-in pins)
Figure out all the electronics needed + PCB design

**Time spent this session: 1 hour**
