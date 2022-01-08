# NE555 explain 

`astable configuration`

![astablec](https://github.com/yoyoberenguer/NE555-timer-/blob/main/NE555.png)

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

![PIN Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/NE555_top_view.PNG)


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

![NE555 Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/simplified%20schematic.PNG)

## Study of the NE555 from the Kicad Simplified schematic
- The RESET function has been removed from the RS flip-flop and will not be a part of this experiment

We can study the NE555 into 4 different steps:
1) The voltage bridge divider 
2) The comparators stage
3) The RS flip-flop 
4) Frequency analysis with C charge and discharge

`Kicad NE555 Simplified schematic version with additional leds`

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/schema.png)

### Voltage divider
The voltage divider is made of 3 identical resistors R1, R2, R3 (value 5k) supply with a 5V DC power supply voltage.
The input current going through the AOP AS358 is negligeable (maximun few 100 nA, typical 20nA) via U1A (pin 2) & U1B (pin 5)

Consequently, the current passing through R1, R2, R3 is the same. 
The voltage applied on the pin 5 and to pin 2 can be calculated as follow: 
```
v+ = (R3 / (R3 + R2 + R1)) * VCC 
v+ = 1/3 * Vcc
v+ = 1.667

The voltage on pin 2 is : 
v- = (R2 + R3) / (R1 + (R2 + R3)) 
v- = 2/3 * Vcc
v- = 3.334V
```
* (v+ voltage on pin 5 and v- voltage on pin 2) and VCC = 5V

These two voltages are used for controling the external capacitor C and determine the operating voltage range
(within `1/3 Vcc` and `2/3 Vcc`) during the charge and discharge of the capacitor C through the resistors (RA & RB).
When 1/3 Vcc and 2/3 Vcc values are reach during the charging process, the comparators will sequentially trigger two 
signals: `RESET` and `SET` to the flip-flop in order to control the Transistor T1 (NPN 2n222) status (open/close).

### Comparators U1A & U1B

For this experimentation, the signals `TRIG` and `THRES` are wired together and will be used to simulate the 
external C capacitance charge & disharge process with a triangular signal of amplitude 0 - 5v from a signal 
generator connected to these two pins.
The pair TRIG & THRES will be adjusted with an offset of 2.5V to make sure the entire signal vary above the
ground level. The signal can also be a sine with the same settings (0-5v) with a DC offset of 2.5 V 

For the comaparators, we are using the IC AS358 `in open loop` to behave like a comparator. The AS358 is a 
(low power dual operational amplifier that can operates with a wide ranges of power supply voltages 
(in single supply mode 3v - 36V). It as also a low input bias current of 20nA and low input offset voltages
of 2mv, for those reasons a single AS358 is used in the diagram for U1A & U1B. 

The voltage supplied to the comparator is 0 - 5V and the output will vary from 0V to 5V. 
- Output is high (+5v) when V+ > V-  
- Output is low (0v) when v+ < V- 

#### Comparator U1B
As stated above, a triangular signal is used for the negative input (pin 6, labeled TRIG) and will represent 
the external C voltage variation values (see figure 1A).

The yellow square signal represent the comparator output on pin 7 and in blue the voltage reference on pin 6.
You can also observe two horizontal light blue lines representing the constant voltages 1/3 & 2/3 Vcc for reference.
```
When TRIG voltage (pin 6) is > 1.66v the comparator output goes low (V- > V+) and when 
TRIG is below 1.66 the output goes high (V+ > V-) and the RS flip-flop is `reset`
```

`Figure 1A comparator U1B`

![Comparator 1UA](https://github.com/yoyoberenguer/NE555-timer-/blob/main/figure1a.png)
```
When THRES voltage (pin 3) is > 3.33v the comparator output goes high (V+ > V-) and the 
RS flip-flop is `set`. When THRES is below 3.33 the output goes low (V+ < V-)
```
`Figure 1B comparator U1A`

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/figure1b.png)

### RS flip-flop

For the RS flip-flop we are using the IC 74HCT02 (NOR gates). 
The transistor T1 base is connected to the Q bar output (inversed Q) while the collector is 
connected to the external C capacitor (flag DISH)
The Thruth table is defined below (R = 1 & S = 1) is an invalid condition

![Comparator 1UBc](https://github.com/yoyoberenguer/NE555-timer-/blob/main/SR.png)

* When input R is high `reset` the RS output Q is low (Q bar is high).
  A current is going through the transistor base (T1 is saturated) 
  The flag DISH is connected to the ground and the external capacitor is disharging through 
  the resistor RB connected to ground via (DISH flag)
  
* When the input S is high `set` the RS output Q goes high (Q bar is low)
  and the transistor T1 is open, the flag DISH is disconnected. 
  The external capacitor is charging  through the resistors  RA & RB connected to vcc (+5v)
  
As shown in the figures 1A & 1B the comparator outputs are never set to +5v at the same time avoiding the flip-flop 
to be in an invalid state (output Q and Q bar undetermined).

### Frequency analysis (time Period and Frequency)

At t=0 the external capacitor C is disharge and Uc=0v. 
The potential TRIG is equivalent to the voltage difference across the Capacitor (TRIG = 0v) 
The comparator U1B output is high (see figure 1A) and the RS flip-flop output Q bar is low, the transitor T1 is open and 
the capacitor is now charging from ov to 2/3 Vcc through R1 and R2 resistors. 

When the voltage Uc goes over 2/3 Vcc, the comparator U1A ouput is set to high (+5v) and the RS output Q bar is high forcing a current
to flow through the transistor base which is now in saturation mode and THRES is at the same potential than the ground.

As TRESH is connected to the ground the capacitor is now disharging its energy through the resistor R2 and Uc voltage is 
exponentially decreasing until reaching the potential 1/3 Vcc. 

When Uc pass below 1/3 Vcc the Comparator U1B is triggering the RS flip-flop with the output voltage Q bar set to low and 
the transistor is now open forcing the capacitor to charge again through R1 & R2 and so on. 

```
C is charging through R1 & R2 and τ = C(R1 + R2) 

2/3 * Vcc = Vcc * (1 - exp(-t0/τ)) 
t0 = -τ * ln(1/2)

C is disharging through R2 and τ = R2.C
1/3 * Vcc = 2/3 * Vcc * exp(-t1/τ) 
t1 = -τ * ln(1/2)

T = t0 + t1  with ln(1.0/2.0) ≃ -0.7
T = 0.7 * C * (R1+R2) + 0.7 * R2C 
T = 0.7 * (R1 + 2 * R2)* C

frequency = 1 / T 
frequency = 1.0 / (0.7 * (R1 + 2 * R2) * C ) 
or 
frequenct = 1.44 / ((R1 + 2 * R2) * C)


Output driver duty cycle = t0 / ( t1 + t0)  = RB / (RA + 2 * RB)
Output waveform duty cycle = t1 / (t0 + t1) 
```

figure 2 showing the charge and discharge of the external capacitor C between 1/3Vcc cursor a and 2/3Vccc cursor b

`figure 2`

![External C charge and discharge](https://github.com/yoyoberenguer/NE555-timer-/blob/main/External_C.bmp)



