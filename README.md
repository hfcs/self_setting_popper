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
* Use adjustable servo driver, a simpler way in production and operation to drive and adjust each servo mechanically than micro controller, the part just cost 1.5 USD.
* Interface each adjustable servo driver with a 3 pin interface, ground, 5v, in signal
  * We can use a centralized 5V USB 2.0 power supply @500mA to drive all servos in parallel, each servo driver peaks at 5.5mA, that is more than 50 poppers we can drive
  * Use JST SM 3 Pin connector for a locking connection easily sourced


# Parts
* Each popper
  * Servo mount: two (m4x10 screw + m4 nuts): 2.3 RMB
  * MG996R Servo 12.8 RMB
  * Z shaped Servo steel cable pull rod 8.8RMB per 20 = 0.44 RMB
  * Adjustable Servo driver board (preferrable with header pins) 9.79 RMB 
  * SM socket cord x 1 (servo controller), 2pin Dupont socket + 2 female connectors
  * SM pin x 2 (connector cord), 6x female connectors
* Central switch
  * Foot activated guitar switch (press to connect) 7.5 RMB
  * Switch box
  * USB type C socket cord (preferable with power indicator)
  * 12 x SM socket cord
* Test harness
  * USB type C socket cord (preferrable with indicator light)
  * SM pin cord
  * Switch

## Reference
* https://core-electronics.com.au/guides/getting-started-with-servos-examples-with-raspberry-pi-pico/
* https://randomnerdtutorials.com/raspberry-pi-pico-servo-motor-micropython
* https://github.com/hobbyquaker/awesome-mqtt 
