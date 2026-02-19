#  ModelHome Security System
This repository contains the firmware designed to implement a home security system using an STM32 microcontroller. The specific microcontroller I am using is an earlier version of the "black pill," the STM32F401RCT6.

The first layer of security is a laser tripwire paired with a buzzer. The laser tripwire consists of a laser diode pointed at a light-dependent resistor (LDR). The LDR is connected in series with another resistor to form a voltage divider, with the output fed into an SR latch. This setup allows for hardware memory, ensuring that when the laser beam is interrupted by an intruder, the alarm is triggered and remains active until it is manually reset. 

Alternatively, this functionality could be implemented in software using a Boolean variable to represent the system's state (whether the alarm has been activated). The value of this variable would change only under two conditions: 1. If the tripwire is crossed, or 2. If the system is manually reset. However, for reasons I will explain later, I chose to implement a hardware solution for memory.

Instead of using a discrete SR latch, I utilized the built-in SR latch from a 555 timer. In this setup, the SET pin is assigned to pin 2 (trigger, active LOW), and the reset pin is assigned to pin 6 (active HIGH).

To display the system status, I am using a 16x2 LCD without an integrated I2C chip. The STM32 handles the display of various system states, such as: "HOME SECURITY SYSTEM," "ALARM ACTIVATED," "SYSTEM DEACTIVATED," "ACCESS GRANTED," "SYSTEM LOCKED," and "ACCESS DENIED."
