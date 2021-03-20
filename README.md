{{template>:template:project
 | name=portable-led-bar
 | status=active
 | founder=[[user>lepi]]
 | repo=[[github>lepi00/portable-led-bar]]
}}

### Adapting a mains AC led bar to work with a battery of 18650s
by [[people:lepi:start|lepi]](lepi at-a hackerspace.pl)

# Intro
The purpose of this project is to adapt a 220AC UV LED-Bar to work with 18650 cells.

I have just started learning electronics, and my knowledge is very basic.

# Specifications

The LED Bar - Light4Me LED UV 8
^Characteristic                 ^Value                              ^Notes
|Voltage:                       |AC110-240V, 50/60Hz                | |
|Power:                         |30W                                | |
|Light source:                  |8x3W UV LED                        | |
|Light angle:                   |65°                                | |
|Light wavelength:              |390-410 nm                         | |
|Dimensions:                    |450 x 50 x 40 mm + 55 mm pins      | |
|Weight:                        |0,6 kg                             | |
|                               |                                   | |
|LED driver inside (IP65):      |                                   | |
|Model:                         |ZW0820                             | |
|Power:                         |27 W                               | |
|Input:                         |AC85V-265V 50/60Hz                 | |
|Output Voltage:                |27-36V DC                          | |
|Output Current:                |600 mA ±5%                         | |
|TA:                            |60 °C                              | |
|TC:                            |80 °C                              | |

Cells
^Characteristic                 ^Value                            ^Notes
|Datasheet:                     |(https://www.tme.eu/Document/e06617d885c58dfb3fecaf4abbe330c4/ICR18650-26H.pdf)["datasheet"]     | |
|TME Symbol:                    |Samsung ACCU-ICR18650-26H          | |
|Rated voltage:                 |3.63 V                             | |
|Capacity:                      |2.6 Ah                             | |
|Maximum current:               |5.2 A                              | |
|Charging Method:               |constant voltage, limited current  | |
|Charging Voltage:              |4.2 V ±0.05 V                      | |
|Charging Current (standard):   |1300 mA                            | |
|Charging Current (max):        |2600 mA                            | |
|Diameter:                      |18.4 mm                            | |
|Length:                        |65 mm                              | |

Battery charger - Tangspower TP-L8S20 Li-ion charger
^Characteristic                 ^Value                              ^Notes
|Maximum Voltage:               |8 * 4.20 V = 33,6 V                | |
|Charging Current:              |2 A                                |Passive, PFC filter|

### The Story

# Revision 0.1

A friend of mine performs POI with POI-tails that are neon-yellow. The thing is made to shine in UV light.  
Some AC mains LED bars I have, revealed a lot of space inside the casing profile - more than enough to house 8 18650 cells.  
The LEDs have a "PowerLed" package soldered in-series upon a pcb with no other elements, but most likely have some resistor inside the package, as multimeter LED tester does not show anything when testing a single LED.  
  
Remembering next-to-nothing about Electrical Circuits, I started designing a circuit, that would:
 - Power the LEDs from cells
 - Allow charging the cells without taking them out
 - If possible leave the original charger with mains connection


First I considered two solutions:
 - LEDs and cells in parallel
   - Operating current would be         0.6 A * 8 =  4.8 A
   - Charging  current would be         1.3 A * 8 = 10.4 A
 - LEDs and cells in-series
   - Operating voltage would have to be             26.9 V (3.36 V / LED)
   - Charging  voltage would have to be 8 * 4.2 V = 33.6 V

Parallel...
 - I have a TP4056 03962A Lithium Battery Charger with protection module
   - [[03962A description]](https://www.epal.pk/product/tp4056-lithium-battery-charger-with-protection-module/)
   - [[TP4056Datasheet]](http://www.haoyuelectronics.com/Attachment/TP4056-modules/TP4056.pdf)
 - Initially I thought that would be crazy to put 8 of these inside
 - Also wiring LEDs in parallel would if I understand correctly require to put at least 40 cm * 8 = 3.2 m of thick wire - that might be difficult.
  
In-series...
 - A friend informed me to the fact, that I could use an external 33.6V charger which seemed to be easier.
 - And also that I could use LM317 to regulate current out of the cells to LED's
 - I decided to use a I/0/II switch and an IEC cord socket with the original LED driver if possible.

Emeryth suggested:
 - to learn more about li-ion cells before I use un-protected or multiple cells
 - to put some protection between cells and the cell charger
 - to use a DC-DC converter instead of LM317 that produces too much heat
 - to rethink if I need all LEDs in-series

Next Steps:
 - Research Emeryth's suggestions
 - Find a solution to connecting the cells
   - decide whether to solder the cells (dangerous, potentially capacity hindering)
   - contact weld the cells (I don't have access to a contact welder)
   - design a 3d-printed casing for the cells with springs, that would slide into the LED bar casing
   - remember to discharge cells before in case of soldering
 