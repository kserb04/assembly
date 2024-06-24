# Coffee machine control in pure assembly
In the computer system there is an ARM processor,
circuit GPIO1 at address 0xFFFF0F00,
circuit GPIO2 at address 0xFFFF0B00
and the RTC circuit at address 0xFFFF0E00.

To port A of the GPIO2 circuit LEDs and a button are connected as follows:
- bit 0 - key
- bit 5 - red
- bit 6 - yellow
- bit 7 - green

An LCD display connected to port B of the GPIO1 circuit.
Using the system described above your task is to realize the functionality of a simple coffee machine.
The device can do only coffee with milk according to cycles whose states are given in table:

| # | Description                  | Red | Yellow | Green | LCD   |
| - | -                            | -   | -      | -     | -     |
| 1 | Coffee machine is ready      | 0   | 0      | 0     | READY |
| 2 | Coffee machine is warming up | 1   | 0      | 0     | PREP  |
| 3 | Pouring coffee               | 1   | 1      | 0     | PREP  |
| 4 | Pouring milk                 | 1   | 1      | 1     | PREP  |
| 5 | Coffee is done               | 1   | 1      | 1     | DONE  |
| 6 | Error                        | 1   | 0      | 0     | ERORR |

The intial state on the machine is state 1.
The cycle (state 2 to state 5) is started by pressing the button in the simulation.
When the cycle ends, it is necessary to go to state 1 and wait for the button to be pressed again.
If the button is pressed while the cycle is in progress, it is necessary to report an error with state 6 and then go to the initial state (state 1).
States 2, 3 and 4 have the same duration of exactly 30 seconds, and in them the LEDs listed in table 1 are constantly lit.
States 5 and 6 last 180 seconds, and in them it is necessary to achieve the flashing of the LEDs as shown in table for the state 5.
Blinking is performed analogously in state 6 where it is necessary to turn on/off the red LED diode.
The duration of the cycle is to be measured with the RTC circuit that works in intermittent mode and is connected to the IRQ port.

Blinking LEDs for the state 5:
| Duration | Red | Yellow | Green | LCD  |
| -        | -   | -      | -     | -    |
| 30 s     | 1   | 1      | 1     | DONE |
| 30 s     | 0   | 0      | 0     | DONE |
| 30 s     | 1   | 1      | 1     | DONE |
| 30 s     | 0   | 0      | 0     | DONE |
| 30 s     | 1   | 1      | 1     | DONE |
| 30 s     | 0   | 0      | 0     | DONE |

It is not necessary to renew the print on the LCD every time the state changes,
but only in those cases when the state changes causes the LCD printout to change.
The duration of a particular state must be realized by setting the RTC to the correct values, and it is not necessary to measure it in reality, because the given period of the state of the device in the simulator can apparently last longer or shorter, depending on the simulation settings.
