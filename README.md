# SonoLux

A visual and audio-reactive 8x8 LED matrix. 

<img alt="3D View" src="https://github.com/user-attachments/assets/810fa50a-3a1c-4b61-9aa4-d4f07f300fa1" width="500" />
<img alt="Exploded View" src="https://github.com/user-attachments/assets/e4e754ae-0532-40ec-8921-d338fa5cc8dc" width="500" />

I made this project becuase I love the thought of having my own launchpad, but one that is unique and hackable. 

## PCB & Schematic

The PCB and schematic for this project are designed in KiCad.

<img width="500" alt="PCB" src="https://github.com/user-attachments/assets/8cd105cd-9c98-44d1-a1f8-9dadbbe85084" />

<img width="1000" alt="Schematic" src="https://github.com/user-attachments/assets/22426926-7756-47e1-b3db-70aece154b50" />
<img width="1000" alt="HSheet" src="https://github.com/user-attachments/assets/2cb58e94-19b1-4ad0-8f28-ae497677cfdd" />

## Enclosure

The enclosure is designed in Onshape. It consists of a bottom, a side, and a top, all of which can be 3D printed.

<img alt="Exploded View" src="https://github.com/user-attachments/assets/e4e754ae-0532-40ec-8921-d338fa5cc8dc" width="500" />

## Bill of Materials (BOM)
Keep in mind JLCPCB requires at least 2 PCBA boards, so some component quantities are doubled. 

| ITEM               | DESCRIPTION                                   | QTY | TOTAL COST (USD) | SOURCE / LINK |
|--------------------|-----------------------------------------------|:---:|:----------------:|---------------|
| Acrylic            | Matte acrylic to go over PCB                  | 1   | 19.52            | Ponoko quote  |
| PCB Fabrication    | PCB                                           | 1   | 50.90            | JLCPCB quote  |
| SK6812-Mini-E      | Addressable RGB LED, reverse-mounted          | 130 | 7.52             | LCSC          |
| MPR121-QFN         | 12-channel capacitive-touch controller        | 12  | 25.76            | LCSC          |
| Bulk Capacitor     | 1000uF bulk capacitor for power entry point   | 5   | 0.39             | LCSC          |
| Decouple Capacitor | 0.1uF decoupling capacitor for LEDs           | 170 | 0.19             | LCSC          |
| Screw Terminal     | Connects to battery circuit                   | 3   | 0.26             | LCSC          |
| Resistor           | 330 For LED data line                         | 30  | 0.02             | LCSC          |
| Resistor           | 4.7k Pull-up for I2C communication line       | 20  | 0.01             | LCSC          |
| Resistor           | 75k For MPR121 REXT pin                       | 22  | 0.02             | LCSC          |
| ESP32-WROOM-32     | MCU module w/ Wi-Fi                           | 1   | 3.80             | Owned         |
| MAX98357A          | I2S Class-D mono amp                          | 1   | 5.99             | [Owned](https://www.amazon.com/WWZMDiB-MAX98357-Amplifier-Unfiltered-Raspberry/dp/B0BTBS5NW2)         |
| MicroSD Module     | Used for MP3/WAV                              | 1   | 6.99             | [Owned](https://www.amazon.com/HiLetgo-Adater-Interface-Conversion-Arduino/dp/B07BJ2P6X6/)         |
| 3 W 4 Ohm Speaker  | Audio output                                  | 1   | 4.50             | [Link](https://www.amazon.com/CQRobot-JST-PH2-0-Interface-Electronic-Projects/dp/B0822XCPT8?th=1)          |
| SPH0645LM4H        | I2S MEMS microphone                           | 1   | 3.85             | [Link](https://www.aliexpress.us/item/3256808728616834.html?spm=a2g0o.productlist.main.1.29ab7c5bHO29jL&algo_pvid=97362f52-2e0e-49ec-938c-838b55019d29&algo_exp_id=97362f52-2e0e-49ec-938c-838b55019d29-0&pdp_ext_f=%7B%22order%22%3A%2245%22%2C%22eval%22%3A%221%22%7D&pdp_npi=4%40dis%21USD%2110.36%213.85%21%21%2174.01%2127.48%21%40210318ec17504804923494537efebb%2112000047187812245%21sea%21US%212723986122%21X&curPageLogUid=U1hAD3rimfnh&utparam-url=scene%3Asearch%7Cquery_from%3A)          |
| IP5310 Module      | Boost converter/charge module for battery     | 1   | 1.59             | [Link](https://www.aliexpress.us/item/3256804838377410.html?spm=a2g0o.productlist.main.1.3d04477eWeiTQz&algo_pvid=a95f2a12-afe3-415d-b705-1b85ca116083&algo_exp_id=a95f2a12-afe3-415d-b705-1b85ca116083-0&pdp_ext_f=%7B%22order%22%3A%2212%22%2C%22eval%22%3A%221%22%7D&pdp_npi=4%40dis%21USD%211.61%211.61%21%21%211.61%211.61%21%402101ea8c17505276223774332efa67%2112000031375133543%21sea%21US%212723986122%21X&curPageLogUid=97xb7VYnlfOs&utparam-url=scene%3Asearch%7Cquery_from%3A)          |
| Battery            | Battery                                       | 1   | 1.59             | [Link](https://www.amazon.com/FITHOOD-Rechargeable-Connector-Household-Appliances/dp/B0DGCZ9YSX/)          |
| **Subtotal**       |                                               |     | **116.12**        |               |
