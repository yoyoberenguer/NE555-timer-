# NE555 explain via the simplified schematic


## NE555 description
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

## Study of the NE555 schematic revisited
We have split the schematic into N stages in order to study each steps separately. 
* 1 The voltage bridge divider 
* 2 The comparators stage
* 3 The RS flip-flop 
* 4 Frequency analysis with C charge and discharge

`Simplified schematic` with additional leds
* please note that the RESET function as been removed from the RS flip-flop and will not be a part of this testing 

![Simplified Schematic](https://github.com/yoyoberenguer/NE555-timer-/blob/main/schema.png)
