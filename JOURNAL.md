# Launchpad
A reactive 8x8 capacitive Launchpad
> I can't think of a better name so this will be it for now

## May 24: Research
I'm planning on using an ESP32 I have lying around for the MCU. Although it has 10 capacitive touch GPIOs, an 8x8 grid warrants 64 of them. Originally I was planning on using the MPR121 capacitve touch IC, but it only has 4 I2C addresses and each chip supports 12 channels, making it able to support a maximum of 48 touch pads (less than 64). For now, I'm planning on bypassing this by adding another I2C bus. 

Regarding lighting, I'm planning on using WS2812B LEDs because they are addressable and I have experience programming them already (Check out my HonkaCube project!)
For WAV/MP3 playback, I have an SD card module (no SD card though😔).

Next up:
Perhaps prototype a 1x1 LED + capacitive sensing (using ESP32's built-in pins)
Figure out all the electronics needed + PCB design

**Time spent this session: 1 hour**
## May 25: More Research + KiCad
I'm thinking of using a PCB with copper rings connected to the MPR121s.

Problem: I want to have everything on a single PCB, including the LEDs. This means that I'd have to somehow mount the LEDs so that they're flush with the copper rings. 

Solution: After doing a bit of research, instead of using WS2812B LEDs I'm switching to SK6812-Mini-E becuase they have the ability to be reverse-mounted. ]

Also did a bunch of digging for KiCad footprints and other components. At first, I was thinking of buying a 8x8 matrix and having a separate PCB for the capacitive touch, but I think that's unnecessarily complicated. 

### KiCad Time

I took a look at the MPR121 datasheet and found a good reference on how to hook it up. 

![image](https://github.com/user-attachments/assets/a212b5b4-bc4f-4c60-9bec-c13e326b2a37)

According to the datasheet, attaching ADDR to other pins changes the I2C address. Apparently it can also control LEDs???

I also created a footprint and a symbol for each tile on the launchpad. 

Front: ![image](https://github.com/user-attachments/assets/f06692d3-755e-468c-af6a-615e38025c1c)

Back: ![image](https://github.com/user-attachments/assets/90a9a7d0-5a40-4417-be01-c917d1f1fa5c)

3D Render: 
![image](https://github.com/user-attachments/assets/edf108cc-81fa-417e-91d0-6722bc5b50cd)
![image](https://github.com/user-attachments/assets/0ee0a6be-7f5b-467b-b24d-1bc2a60a074b)

I'm also in the process of learning KiCad (I've only used EasyEDA) and creating the actual schematic for the single PCB. 

**Time spent this session: 3 hours**

## May 26: A LOT of KiCad

I did a LOT of digging to find footprints for specific breakout boards I was using. Additionally I had to made sure I had mapped out the pins correctly on the ESP32. One thing I was thinking of was leaving extra pin headers in case I want to add a rotary encoder or something. 

In KiCad, I spent a lot of time creating the schematic and laying out the PCB.

<img width="1090" alt="image" src="https://github.com/user-attachments/assets/1a2dd47a-1c1b-45ae-bcb6-4d78cb08acfd" />

Inside the heirarchical sheets: 

<img width="993" alt="image" src="https://github.com/user-attachments/assets/bdc7f562-1df6-461e-9acb-d270c1b5b686" />

What the current PCB looks like:

<img width="878" alt="image" src="https://github.com/user-attachments/assets/51f7e6a9-9714-4082-9efa-723405ba0f8d" />

I'm trying to keep the PCB at two layers, but its a little difficult routing the connections becase of the big capacitive touch pads I made on the front layer. 

**Time spent this session: 4 hours**

