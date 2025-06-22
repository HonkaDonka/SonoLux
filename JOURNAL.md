---
title: "SonoLux"
author: "@High_Kid"
description: "Reactive LED matrix"
created_at: "2025-05-24"
---
## Total Time Logged: 23 hours

## May 24: Research
Here's a mini list of what I want to include in this project:
- Some sort of capacitive touch
- LEDs (preferably addressable ones)
- Sound
- Audio input
- Built-in audio playback

I based this project off of a launchpad (image below), which is a grid of buttons each assigned to a sound. However, I also wanted to add my own spin on it (hence the capacitive touch + audio input). 

![image](https://github.com/user-attachments/assets/f8401ea9-f9ae-401e-9063-c157b9924886)

I looked up some capacitive touch ICs and settled on the MPR121 becuase of the available documentation and its price. According to [its datasheet](https://lcsc.com/datasheet/lcsc_datasheet_2410010232_NXP-Semicon-MPR121QR2_C91322.pdf), each chip supports up to 12 channels and it can be configured into four different I2C addresses. This only makes 48 channels for capacitive touch, but I'm planning to work around this by adding another I2C bus for an additional two units of the IC.

For the LED lighting in the project, I'm planning on using WS2812B LEDs because they are addressable. Yes, they are more expensive than regular LEDs, but they eliminate the need for shift registers and only require one data line. Plus, I already have experience programming them (Check out my [HonkaCube](https://github.com/HonkaDonka/LEDCube) project!)

For audio playback, I have an SD card module (no SD card though 😔) and a MAX98357 amp already. The only thing I'm missing regarding this is a speaker. 

Next up:
- Perhaps prototype a 1x1 LED + capacitive sensing (using ESP32's built-in pins)
- Figure out all the electronics needed + PCB design

**Time spent this session: 2 hours**

## May 25: More Research + KiCad
I'm thinking of using a PCB with copper pads connected to the MPR121s. The copper pads would be for capacitive touch sensing and would connect directly to the MPR121 channels. To protect the copper rings, I'm planning on having a thing sheet of acrylic above the PCB. However, this means the top layer would have to be completely flat, so all electronics that stick out would have to be mounted on the bottom (including the MPR121s)

This is where I ran into a major roadblock: since I'm planning on using WS2812B LEDs, I'd have to somehow mount them in such a way that sits flush with or below the copper rings. At first, I was thinking of having two PCBs: one would be the 8x8 matrix of LEDs, and the copper rings would sit right on top, with cutouts so the light can shine through. There are plenty of 8x8 matrices available on Aliexpress as well. However, I'd have to design "around" those LED matrices, and many of them aren't as big as I want anyways. 

After doing a bit of research, I decided to use reverse-mount LEDs (SK6812-Mini-E). These are also addressable, so I can use the same [libraries](https://github.com/adafruit/Adafruit_NeoMatrix) I've been using for my previous projects.

To begin creating the PCB, I did a bunch of digging for KiCad footprints and other components. 

### KiCad Time

I took a look at the MPR121 datasheet and found a good reference on how to hook it up to VCC and configure the I2C addresses. 

![image](https://github.com/user-attachments/assets/a212b5b4-bc4f-4c60-9bec-c13e326b2a37)

According to the datasheet, attaching ADDR to other pins changes the I2C address. Apparently it can also control LEDs 😮, but that's not what I'm using them for.

I also created a footprint and a symbol for each "tile" (copper pad + SK6812). The symbol was simply an addressable LED symbol with an extra pin. 

| Image | Description |
|------|-------------|
| <img width="100" alt="image" src="https://github.com/user-attachments/assets/41a373a7-c310-4ca6-9859-004146c7a1ed" /> | Footprint Front |
| <img width="100" alt="image" src="https://github.com/user-attachments/assets/153b0687-0c3a-47e9-89bd-2ec9e3264a6f" /> | Footprint Back |
| <img width="100" alt="image" src="https://github.com/user-attachments/assets/f9428d6a-0485-4c81-bff1-7d897099abb0" /> | Symbol |

Additionally, I started creating the actual schematic for the project.

**Time spent this session: 3 hours**

## May 26: A LOT of KiCad

One thing I was thinking of was leaving extra pin headers in case I want to add extra peripherals after the PCB is made. 

In KiCad, I spent a lot of time creating the schematic and laying out the PCB. I recently found out about heirarchical sheets and they are SUCH a livesaver. 

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/1a2dd47a-1c1b-45ae-bcb6-4d78cb08acfd" />

Inside the heirarchical sheets: 

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/bdc7f562-1df6-461e-9acb-d270c1b5b686" />

What the current PCB looks like (I know it looks like a nightmare):

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/51f7e6a9-9714-4082-9efa-723405ba0f8d" />

I'm trying to keep the PCB at two layers, but its a little difficult routing the connections becase of the big capacitive touch pads I made on the front layer. I'm going to look into using an autorouter to get this done. 

**Time spent this session: 4 hours**

## May 29: Too much KiCad

I did some journal updates and added some details + fixed some errors. 

For portability, I want to add a LiPo battery into the Launchpad and that means I need to have a charging and battery protection circuit. Luckily, I found [this guide](https://www.instructables.com/DIY-LiPo-ChargeProtect5V-Boost-Circuit/) on how I can do just that!

However, that's an addition I'm going to work on later. For now I need to continue routing connections on my PCB and soon get started on the modeling of the enclosure. 

I tried to use an autorouter(freerouting) plugin for all the IC connections because they were going to be really time consuming, but it turns out autorouters aren't the smartest (it tried to delete my entire PCB).

This is what the board looks like currently. I haven't added the SDA/SCL lines just yet. 

![image](https://github.com/user-attachments/assets/d4dbbe7b-59c0-491b-8f84-14827f292c63)

**Time spent this session: 2 hours**

## June 1: I messed up

Change of plans, I'm switching to a 4 layer PCB. After rewiring everything (and modifying some existing connections), I added a ground plane and a 5V power plane on the inner two layers, making wiring so much simpler. This also has the advantage of separating the MPR121 and LED data lines further, increasing signal integrity (I think?) 

In favor of space, I decided to make the LiPo battery circuit external, so I won't be putting it on the PCB. 

Today I exported the design in JLCPCB to check for any pick and place errors. For some reason, it's showing the SK6812s as front-side components, even though they are reverse mounted. I think this is because the footprint I made for the copper ring and LED is assigned to F.Cu. I fixed this by going to KiCad's footprint editor and flipping the LED Tile footprint (and swapping the pads around). After updating all the existing footprints, it all seemed good to go! 

![image](https://github.com/user-attachments/assets/1c62bfbe-a15c-4735-9cfa-ea204f0e0fc6)

**Time spent this session: 5 hours**

## June 7: Graduation 
Yay.

<img width="314" alt="image" src="https://github.com/user-attachments/assets/b1d23793-9ac9-40cd-b8d8-1262132799b0" />

**Time spent this session: 0 hours 😁**

## June 14: I'm Back

Finalized a couple things. Changes include:
- Adding M3 mounting holes
- Adding capacitors at power entry points
- Flipping some components

<img width="617" alt="image" src="https://github.com/user-attachments/assets/64c495e1-ae72-4803-b608-d5613ac6757a" />

I chose my speaker and battery circuit: 

<img width="574" alt="image" src="https://github.com/user-attachments/assets/8c95f5fc-c3cf-4a60-b663-35a94d057efc" />

![image](https://github.com/user-attachments/assets/d0f60481-56ab-4e66-8598-5c6d6c8d824a)

Time to CAD!!!

**Time spent this session: 1 hour**

## June 18-20: CAD Madhouse

For the enclosure, I'm thinking of having a box with the acrylic making up the top surface. Sitting right below the acrylic would be the PCB. 

![image](https://github.com/user-attachments/assets/bf68d724-221b-4756-8b8a-eee298a59377)

I'm trying to figure out how to mount the top components, as the speaker I chose is quite big. I chose to make a cutout on the PCB so that the speaker would fit without hitting the PCB. 

<img width="652" alt="image" src="https://github.com/user-attachments/assets/a1b969d1-e8d4-4fac-96ee-7f316689c51e" />

I'm left with something like this. The red outline would be the acrylic and the blue outline would be the top of the enclosure, printed as a separate piece. 

![image](https://github.com/user-attachments/assets/9531d11c-2092-4983-9187-7c12f2dc1e84)

Created the final cover, spent a lot of time adjusting the length of the extrudes to match the dimensions of the PCB, acrylic, speaker, etc. The top right of the case is a bit empty right now, but I can add my own additions later.

![image](https://github.com/user-attachments/assets/9db51201-67e1-4c9d-96b5-b883a2374be1)

Final exploded view:

![image](https://github.com/user-attachments/assets/cd5284ed-cd02-4044-a1ad-f129fc292bc7)

**Time spent this session: 5 hours**

## June 21: Finalizing (hopefully)

Uploaded relevant files and wrote out the README.

**Time spent this session: 1 hour**
