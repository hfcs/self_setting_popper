# Self Setting Popper

## Problem Statement
Airsoft competitive shooting use small poppers seating low the the ground. 
Resetting such targets competitors and range officers kneeing or bending down.
We intend to eliminate such toil automating the progress. 

There is a known commercial product in the market, yet the product does not support 
"gravity drop on hit" and cost around 100 USD. We are seeking to build a cost
down version that support gravity drop like the usual airsoft poppers.

## Principles

* Hardware design
  * Durable design that can survive abuse
  * Commericial off the shelf parts, minimal parts fabrication
  * Sustainable sourcing
    * Commodity part with long usage history
    * Widely available from Taobao/Aliexpress
* Software design
  * Simple deployment by end user, simple maintainence by hobbyist

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


# Parts
* Each popper
  * Servo mount: two (m4x10 screw + m4 nuts): 2.3 RMB
  * MG996R Servo 12.8 RMB
  * Z shaped Servo steel cable pull rod 8.8RMB per 20 = 0.44 RMB
  * Adjustable Servo driver board (preferrable with header pins) 9.79 RMB 
  * RJ45 socket -> jumper socket (10 pin version) 6.5 RMB
  * 2p male -> female jumper cable 0.44 RMB (2.2 RMB for 5)
  * 18650 battery box (2 in serial, with swtich and cover) 5.5 RMB
    * We intended using 1 compartment only shorting out the rest
  * 18650 Battery 15 RMB
  * Cat 5 cable (15m) 30 RMB
  * Controller case 1.1 RMB
* Central switch
  * Foot activated guitar switch (press to connect) 7.5 RMB
  * 2 x 9 way RJ45 interface board (HL-RJ45-09) 53 x 2 RMB
  * Trigger delayed relay module (5V version) 7.9 RMB
  * Plastic case 9 RMB
* Test harness
  * RJ45 socket -> jumper socket (10 pin version) 6.5 RMB
  * Switch

## Reference
* https://core-electronics.com.au/guides/getting-started-with-servos-examples-with-raspberry-pi-pico/
* https://randomnerdtutorials.com/raspberry-pi-pico-servo-motor-micropython
* https://github.com/hobbyquaker/awesome-mqtt 
