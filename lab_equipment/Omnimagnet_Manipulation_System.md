[Home](../Home)
# Omnimagnet Manipulation System

>:warning: **This page is incomplete! Please add any information that may be missing or useful!**

DAQ card in omnicomputer: PCI-1724U
This DAQ card has 62 pins, AO0-AO31, the rest are ground. The comedi driver software uses the analog pin number. The mapping between analog pin number and wire pin is found in the [DAQ datasheet repo](https://bitbucket.org/utahtelerobotics/docs-pci-1724u/src/master/).


18x Amplifiers model: 30A8


The DAQ analog output pin 25 is used to enable all the Amplifiers. Testing with 15 amplifiers plugged in pulls roughly 80mA, the DAQ analog output pin is rated for 10mA. To supply the needed current to the enable pins a relay is used with a wall mounted 5V power supply using the DAQ analog output to trigger the relay instead. 

January 2023 the wall mounted 5V power supply is broken, unclear why. Purchased equivalent
https://www.amazon.com/dp/B09W96X88K




On the computer the omnimagnets are plugged into the following analog out pins on the DAQ card. Ordering is in theory, inner coil, middle coil, outer coil.

1. Omni0: 2,0,18
2. Omni1: 3,11,19
3. Omni2: 4,12,20
4. Omni3: 5,13,21
5. Omni4: 6,14,22


3 of the amplifiers are currently not currently in use.