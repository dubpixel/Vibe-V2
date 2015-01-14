Vibe V2
=======

Firmware and board files for Dame Products EVA Vibe V2. More product info here...

http://www.dameproducts.com/

Note that this V2 of the board. The older V1 board files are here...

https://github.com/bigjosh/VibeSystem

User Interface
--------------
Device is normally in a low-power off state.

Each press of the button steps to the next speed setting. There are 3 speed settings (low, medium, high) and a 4th button press returns to off state.

A long button press (~0.25 sec) goes straight to off state from any speed.

When battery gets low, the motor turns off and the red LED lights for about 1 second. Subsequent button pushes blink the red LED again to indicate not enough power to turn on. Note that Litium Polymer batteries recover some voltage while resting, so it is possible to briefly turn the unit back on even after it has automatically turned off from low battery. Doing this repeatedly will lead to shorter and short on times until eventually the battery is too depleated to have any revcovery left.

Because the battery has reduced voltage under load, there are different cutoff voltages for initial turn on and continuing operation. The battery must be at least 3.3 volts for the motor to start, but once started it will continue to run until the battery drops to 3.1 volts. 

The white LED is lit at about 50% brightness whenever the button is pushed for feedback.

The white LED also indicates charger status: 

* Off means no charger connected
* On solid full brightness means charger is connected and battery is fully recharged
* Slow pulse (1Hz) means charging

Motor is always off while charger connected. Button state is ignored while the charger is connected.

Test Mode
---------
On initial power-up, the devices enters a test mode...

1. You should see the LEDs alternate blinking red and white at about 10Hz. This lets you visually verify both LEDs are working. 
  1. If you don't see anything on power-up, then either both LEDs are broken or there is some worse problem.
  2. If you see a single LED blinking on and off at 10Hz, then the other LED is bad.
  3. If you see the while LED on at 50%, then you probably have a stuck button. 

2. Press the button. The white LED should light solid at 50% brightness for as long as you hold down the button. The LED should go out when you release the button.
  1. If the LEDs continue to alternate flash after you push the button, then you probably have a bad button or bad connection from the board to the button. 
  2. If the white LED stays lit at 50% brightness after you release the button, then you probably have a stuck button.

Note that both above LED indications time out after about 30 seconds to avoid killing the battery. If the button stays down past the timeout, the the unit will enter "stuck button defense" mode (see below). 

Note that test mode only happens on initial power up. Because the board is very low power, it can continue to operate off the residual charge in the capacitor for a long time (days-months). Because of this, you must follow this procedure to re-enter test mode once the device has been powered up (it is not enough just to remove the battery and replace it)... 

1. disconnect all power (unplug the battery, unplug charger)
2. push and hold the button for a second to exhaust all the residual power from the capacitors
3. reconnect power and test mode should start again
 
Stuck Button Defense
--------------------
To avoid damage to the battery, if the button is held down for more than about 30 continuous seconds then it is assumed to be stuck (maybe becuase something is resting on top of the unit and pressing the button) and the button is disabled. When this happens, the Vibe must be plugged into a charger to reset it. 

Features
--------
* Current draw of <0.1uA when idle, so battery self-drain is likely the limiting factor for maximum off time.
* Zero latency button debounce.
* Motor output power is scaled to battery power so motor speed stays constant though battery discharge (at least until there is not enough voltage left to maintain speed). 
* Code size of about 1.5K easily fits into cheap ATTINY24A parts. 
* A full processor WatchDog reset is executed every time the motor is turned off or the charger is unplugged. This hopefully makes the unit more robust to failures.

Connections
-----------
The specified battery is a 160mAh Polymer Li-ion. Verify the polarity on the connector because it is non-standard and reversed polarity will blow a protection diode. 

The specified motor is a vibration type nominally rated for 130mA at 3V.

Note that the battery polarity is swapped compared  to normal! Follow the markings on the board (positive battery wire towards middle of the board).
