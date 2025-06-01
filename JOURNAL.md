---
title: "SonoLux"
author: "@High_Kid"
description: "Reactive 8x8 LED grid"
created_at: "2025-05-24"
---

## May 24: Research
I'm planning on using an extra ESP32 I have lying around for the MCU on this project. Since I want to use capacitive touch buttons instead of mechanical switches, I did a bit of digging and found that the ESP32 does have 10 capacitive touch GPIOs. However, an 8x8 grid warrants 64 of them. 

I looked up some capacitive touch ICs and settled on the MPR121 becuase of the documentation and its availability. Each chip supports up to 12 channels and it can be configured into four different I2C addresses. This only makes 48 channels for capacitive touch, but I'm planning to work around this by adding another I2C bus for an additional two units of the IC.

MPR121

![image](https://github.com/user-attachments/assets/f93f7ddc-ef85-4ea9-bc36-2e3f7855d3a4)
<img width="250" alt="image" src="https://github.com/user-attachments/assets/170340f2-59e6-4521-b342-04d74b509a96" />

For the lighting in the project, I'm planning on using WS2812B LEDs because they are addressable so wiring doesn't have to be a mess (just one data line) and I already have experience programming them (Check out my HonkaCube project!)

For WAV/MP3 playback, I have an SD card module (no SD card though 😔) and a MAX98357 amp already.

Next up:
Perhaps prototype a 1x1 LED + capacitive sensing (using ESP32's built-in pins)
Figure out all the electronics needed + PCB design

**Time spent this session: 2 hours**

## May 25: More Research + KiCad
I'm thinking of using a PCB with copper rings connected to the MPR121s. The copper rings would be for capacitive touch and would sit directly under diffused acrylic. I want to minimize the distance between the finger and the copper rings so I think all the ICs on the board would have to be mounted underneath. 

This is where I ran into a major roadblock: since I'm planning on using WS2812B LEDs, I'd have to somehow mount them in such a way that sits flush with the copper rings. I want to keep everything on a single PCB, so I decided to use reverse-mount LEDs (SK6812-Mini-E). These are also addressable, so I can use the same libraries I've been using/

To begin creating the PCB, I did a bunch of digging for KiCad footprints and other components. 

### KiCad Time

I took a look at the MPR121 datasheet and found a good reference on how to hook it up to VCC and configure the I2C addresses. 

![image](https://github.com/user-attachments/assets/a212b5b4-bc4f-4c60-9bec-c13e326b2a37)

According to the datasheet, attaching ADDR to other pins changes the I2C address. Apparently it can also control LEDs 😮

I also created a footprint and a symbol for each "tile" (copper ring + SK6812s). 

Front: 

<img width="200" alt="image" src="https://github.com/user-attachments/assets/41a373a7-c310-4ca6-9859-004146c7a1ed" />

Back: 

<img width="200" alt="image" src="https://github.com/user-attachments/assets/153b0687-0c3a-47e9-89bd-2ec9e3264a6f" />


3D Render: 

<img width="200" alt="image" src="https://github.com/user-attachments/assets/21b6fbce-a14d-4a19-9832-60517273aa58" />

<img width="200" alt="image" src="https://github.com/user-attachments/assets/a461d756-0739-40af-807a-faa1b8e5e567" />

I'm also in the process of learning KiCad (I've only used EasyEDA) and creating the actual schematic for the single PCB. 

**Time spent this session: 3 hours**

## May 26: A LOT of KiCad

I searched far and wide to find footprints for specific breakout boards I was using. Additionally I had to made sure I had mapped out the pins correctly on the ESP32, as this is easily one of the most ambitious projects I'm making. 

Idea: One thing I was thinking of was leaving extra pin headers in case I want to add a rotary encoder or something after the PCB is made. 

In KiCad, I spent a lot of time creating the schematic and laying out the PCB.

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/1a2dd47a-1c1b-45ae-bcb6-4d78cb08acfd" />

Inside the heirarchical sheets: 

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/bdc7f562-1df6-461e-9acb-d270c1b5b686" />

What the current PCB looks like:

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/51f7e6a9-9714-4082-9efa-723405ba0f8d" />

I'm trying to keep the PCB at two layers, but its a little difficult routing the connections becase of the big capacitive touch pads I made on the front layer. 

**Time spent this session: 4 hours**

## May 29: Too much KiCad

I did some journal updates and added some details + fixed some errors. 

For portability, I want to add a LiPo battery into the Launchpad and that means I need to have a charging and battery protection circuit. Luckily I found [this guide](https://www.instructables.com/DIY-LiPo-ChargeProtect5V-Boost-Circuit/) on how I can do just that!

However, that's an addition I'm going to work on later. For now I need to continue routing connections on my PCB and soon get started on the modeling of the enclosure. 

I tried to use an autorouter(freerouting) for all the IC connections because they were going to be really time consuming, but it turns out autorouters aren't the smartest (it tried to delete my entire PCB).

This is what the board looks like currently. I haven't added the SDA/SCL lines just yet. 

![image](https://github.com/user-attachments/assets/d4dbbe7b-59c0-491b-8f84-14827f292c63)

**Time spent this session: 2 hours**
