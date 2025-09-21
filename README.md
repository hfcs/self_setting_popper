# Self Setting Popper

## Problem Statement
Airsoft competitive shooting use small poppers seating low the the ground, resetting such targets competitors and range officers kneeing or bending down. We intend to eliminate such toil automating the process. 

There is a known commercial product in the market, yet the product does not support "gravity drop on hit" and cost around 100 USD. We are seeking to build a cost down version that support gravity drop like the usual airsoft poppers.

## Principles

* Hardware design:
  * Durable design that can survive abuse.
  * Commericial off the shelf parts, minimal parts fabrication.
  * Sustainable sourcing:
    * Commodity part with long usage history.
    * Widely available from Taobao/Aliexpress.
* Software design:
  * Simple deployment by end user, simple maintainence by hobbyist.

## Solution Scope

## Functional Requirements
* Gravity drop target
* Setting without bending down

## Non Functional Requirements
* Drop from 1 meter on hard surface
* Software maintainable and deployable by hobbyist and student type of skills

## Design decisions and rationales
* Use MG996R servo, MG90 micro servo are too weak to drive a light titanium mini-popper
  * Each target needs to have it's own 3-5v power supply, MG966R can take up to 2.5A stall current when peaking out
* Use adjustable servo driver, a simpler way in production and operation to drive and adjust each servo mechanically than micro controller, the part just cost 1.5 USD.
* Interface each adjustable servo driver with a 2 pins interface, ground, in signal (low level trigger)
  * Use RJ45 socket, taking a TBD pair for the ground/input trigger for a locking connection easily sourcing off-the-shelf cable


## Parts

### Each popper
| Part                               | Count | Remark                               | Reference Price (RMB yen, Taobao) |
|----------------------------------- |-------|--------------------------------------|-----------------------------------|
| Servo mount                        | 1     |                                      | 2.3                               |
| M4x10 screw                        | 2     |                                      | N/A                               |
| M4 nut                             | 2     |                                      | N/A                               |
| MG996R Servo                       | 1     | Come with servo horns                | 12.8                              |
| Servo steel cable pul rod          | 1     | Elastic rod acts as servo saver      | 0.44                              |
| Adjustable servo driver board      | 1     | Preferable with header pins          | 9.79                              |
| RJ45 socket -> jumper socket cord  | 1     | 10 pin version                       | 6.5                               |
| 2pin male -> female jumper capble  | 1     |                                      | 0.44                              |
| 18650 battery box                  | 1     | Single battery box with header pins  | 5                                 |
| 18650 battery                      | 1     |                                      | 15                                |
| Cat 5 cable (15m)                  | 1     |                                      | 15                                |
| PLC case (125x90x40mm)             | 1     |                                      | 5                                 |

### Central switch
| Part                               | Count | Remark                               | Reference Price (RMB yen, Taobao) |
|------------------------------------|-------|--------------------------------------|-----------------------------------|
| Foot activated guitar switch       | 1     | press to connect                     | 7.5                               |
| 9 way RJ45 interface board         | 1     | HL-RJ45-09                           | 53                                |
| Trigger delayed relay module       | 1     | QF1025F 3V version                   | 7.9                               |
| 4.3 inch display case              | 1     | Window opening 107*70mm              | 8                                 |
| 10k ohm pull up resistor           | 1     |                                      | N/A                               |
| 18650 battery box                  | 1     | Single battery box with header pins  | 5                                 |
| 18650 battery                      | 1     |                                      | 15                                |

### Test harness
| Part                               | Count | Remark                               | Reference Price (RMB yen, Taobao) |
|------------------------------------|-------|--------------------------------------|-----------------------------------|
| RJ45 socket -> jumper socket cord  | 1     | 10 pin version                       | 6.5                               |
| Switch                             | 1     | press to connect                     | 7.5                               |

## How the system works
  * All sockets on the RJ45 switch box are tied together, pressing the switch (shorting) will trigger the relay.
  * The relay will drive input signal of each servo driver boards to low and drive the servo to "up" position.
  * After preset time the relay will disconnect and return the servo to "down" position.

## How to build 

### RJ45 pin assignment
  * Only use Brown, Brown-white pair.
  * Brown-white pair assign to ground, Brown assign to popper input.

### Popper
  * Assemble servo driver board:
    * Input signal -> RJ45 Brown pin 8: Solder directly on board, or solider a jumper wire and plug into jumper socker on the RJ45 wire.
    * Ground/- -> RJ45 Brown-White pin 7: Solder directly on board, or solider a jumper wire and plug into jumper socker on the RJ45 wire.
    * Output Signal -> Servo Signal (Yellow) : plug in pin on the board into header socket.
    * Output + -> Servo + : plug in pin on the board into header socket.
    * Output - -> Servo - : plug in pin on the board into header socket.
    * Since we have a stable battery supplied power we can skip the capacitor across the input power.
  * Mount servo steel cable pull rod on servo horn and secure it (e.g. with steel wire and tighten).
  * Adjust each servo controllers such that servo horn press gently on popper, flexing the steel cable pull rod a little bit and act as servo saver.

### Central switch
  * Assemble trigger delayed relay module:
    * Input:
      * DC in + -> a) Battery box + b) one end of 10k ohm resistor.
      * DC in - -> a) Battery box - b) Switch connector 1 c) CON from output.
      * IN -> Switch connector 2.
    * Output:
      * COM -> a) Brown-white wire on RJ45 switch box (pin 7) b) DC in - from input.
      * NO -> a) Brown wire on RJ45 switch box (pin 8) b) one end of 10k ohm resistor.
  * Adjust relay delay for 1-3 seconds just enough for poppers to settle.
  * Note on pull-up resistor:
    * Central switch now use 18650 to align the voltage of high input of the poppers, which are driven by pull-up resistor.
    * Since we use central switch and pull-up, we need to tie the ground of central switch and output to poppers.

## Lesson Learnt
  * Switching from JST SM cable to RJ45 is a buy vs build decision, we can get more reliable outcome for cheap buying or sourcing RJ45 cables.
  * We should apply pull up resistor on relay output, servo controllers may power down or have bad connection that cause their input going low, which will drive all connected poppers to "up" position and stuck there.

## Reference
* https://core-electronics.com.au/guides/getting-started-with-servos-examples-with-raspberry-pi-pico/
* https://randomnerdtutorials.com/raspberry-pi-pico-servo-motor-micropython
* https://github.com/hobbyquaker/awesome-mqtt 
