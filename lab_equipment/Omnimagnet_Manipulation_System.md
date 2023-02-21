[Home](../Home)
# Omnimagnet Manipulation System

>:warning: **This page is incomplete! Please add any information that may be missing or useful!**

The system driver source code is found in the [omnimagnet_system_driver][source] repository.

The system is driven by an [Advantech PCI-1724U Analog Output PCI card][pci-1724u-docs].
This PCI card has 62 pins, 32 14-bit analog outputs AO0-AO31 and the rest are ground. The comedi driver software uses the analog pin number. The mapping between analog pin number and wire pin is found in its documentation repository (linked above).


18x Amplifiers model: 30A8


The PCI-1724U analog output pin 25 is used to enable all the Amplifiers. Testing with 15 amplifiers plugged in pulls roughly 80mA, the PCI-1724U analog output pins are rated for 10mA. To supply the needed current to the enable pins a relay is used with a wall mounted 5V power supply using the PCI-1724U analog output to trigger the relay instead. 

January 2023 the wall mounted 5V power supply is broken, unclear why. Purchased equivalent
https://www.amazon.com/dp/B09W96X88K

On the computer the omnimagnets are plugged into the following analog out pins on the PCI-1724U card. Ordering is in theory, inner coil, middle coil, outer coil.

1. Omni0: 2,0,18
2. Omni1: 3,11,19
3. Omni2: 4,12,20
4. Omni3: 5,13,21
5. Omni4: 6,14,22


3 of the amplifiers are currently not currently in use.

[source]: https://bitbucket.org/utahtelerobotics/omnimagnet_system_driver/src
[pci-1724u-docs]: https://bitbucket.org/utahtelerobotics/docs-pci-1724u/src/master/