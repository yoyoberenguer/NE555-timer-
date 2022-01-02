# NE555 explain 

## NE555 History 
`source history here (https://www.circuitstoday.com/the-history-555-timer-ic)`

The 555 Timer IC is one of the renowned ICs, in the electronic circles. However, its history of invention is not known to many. 
This article takes you on a journey of 555 timer IC from the time of its creation to the present day time.
Hans R. Camenzind, designed the first 555 timer IC in 1971, under an American company Signetics Corporation. 

It is this design work of his, that is most prominent in Hans’s distinguished career in the field of Integrated Circuit technology.
In the summer of 1971,  first design was reviewed, that used a constant current source and had 9 pins. 
After the review was passed, Hans thought of a new idea of replacing the constant current source by a direct resistance.
This reduced the number of pins from 9 to 8, and enabled the chip to be fit in an 8 pin package instead of a 14 pin package.
This new design was passed in the review in October 1971. 

The IC consists of 25 transistors, 2 diodes and 15 resistors.
In order to define the timings, provision to attach R and C externally is provided.
In 1972, Signetics Corp. then released its first 555 timer IC in 8 pin DIP and 8 pin TO5 metal can packages, as SE/NE555 
timer and was the only commercially available timer IC at that time. Its low cost and versatility, made it an instant hit
in the market. It was later on manufactured by 12 other companies and became the best selling product.

`Although, there is a belief that this IC got its name from the three 5k resistors in its internal circuit`, Hans R Camenzind revealed
in his book, “Designing Analogue Chips”,  that it was Signetics manager, ArtFury’s, love for the number “555”,
that led to the naming of the circuit.


What is a 555 timer IC?
A 555 timer IC, is a multipurpose integrated circuit chip, that finds its application in timer, oscillation and pulse generation circuits. It is one of the prominent and popular inventions of the electronic world. A monolithic timing circuit, the 555 timer, is equally reliable and cheap like op-amps working in the same areas. It is capable of producing stabilized square waveforms of 50% to 100% duty ratio.

## NE555 description

`Pin diagram`

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/NE555_top_view.PNG)


These devices are `precision timing` circuits capable of producing accurate time delays or oscillation. In the
time-delay or `monostable` mode of operation, the timed interval is controlled by a single external resistor and
capacitor network. In the `astable` mode of operation, the frequency and duty cycle can be controlled
independently with two external resistors and a single external capacitor.

The `threshold` and `trigger` levels normally are `two-thirds` and `one-third`, respectively, of VCC.
These levels can be altered by use of the control-voltage terminal. When the trigger input falls below the trigger level,
the `flip-flop` is set, and the output goes high. If the trigger input is above the trigger level and the threshold input is above the
threshold level, the flip-flop is reset and the output is low. The reset (RESET) input can override all other inputs
and can be used to initiate a new timing cycle. When RESET goes low, the flip-flop is reset, and the output goes
low. When the output is low, a low-impedance path is provided between discharge (DISCH) and ground.
The output circuit is capable of sinking or sourcing current up to 200 mA. Operation is specified for supplies of
5 V to 15 V. With a 5-V supply, output levels are compatible with TTL inputs.

Simplified schematic of an NE555 

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/simplified%20schematic.PNG)

## Study of the NE555 from the Kicad Simplified schematic
- The RESET function has been removed from the RS flip-flop and will not be a part of this experiment

We can study the schematic from 4 different stages
* 1 The voltage bridge divider 
* 2 The comparators stage
* 3 The RS flip-flop 
* 4 Frequency analysis with C charge and discharge

`Kicad NE555 Simplified schematic version with additional leds`

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/schema.png)

### Voltage divider
The voltage divider is made of 3 identical resistors R1, R2, R3 (value 5k) supply with a 5V DC power supply voltage.
The input current going through the AOP AS358 is negligeable (maximun few 100 nA, typical 20nA) via U1A (pin 2) & U1B (pin 5)

Consequently, the current passing through R1, R2, R3 is identical. 
The voltage applied on the pin 5 is the determine as follow (v+ voltage on pin 5 and v- voltage on pin 2) with VCC = 5V
```
v+ = (R3 / (R3 + R2 + R1)) * VCC 
v+ = 1/3 * Vcc
v+ = 1.667

The voltage on pin 2 is : 
v- = (R2 + R3) / (R1 + (R2 + R3)) 
v- = 2/3 * Vcc
v- = 3.334V
```
These two voltages will be used to control the charge and discharge of the external capacitor C. 
1/3 Vcc and 2/3 vcc will be the voltage minimum and maximum during the charge and discharge of the capacitor C 
through the resistors (RA & RB).

### Comparators U1A & U1B
We are using the IC AS358 in open loop to behave like a comparator. The AS358 is a (low power dual operational
amplifuers that can operates with a wide ranges of power supply voltages (in single supply mode 3v - 36V). 
It as also a low input bias current of 20nA and low input offset voltages of 2mv, for those reasons a single 
AS358 is used in the diagram for U1A & U1B. 
The voltage supplied to the comparator is 0 - 5V and the output state will remain within the same range. 
- Output is high (+5V) when V+ > V-  
- Output is low (0v) when v+ < V- 




