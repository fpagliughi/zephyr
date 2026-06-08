.. zephyr:board:: adafruit_feather_m0_bluefruit_le

Overview
********

The Adafruit Feather M0 Bluefruit LE is a thin, light ARM development
board with an onboard battery connector and charger for 3.7 V lithium
polymer batteries, charging status indicator and user LEDs, native USB
connector, 20 I/O pins, and an nRF51822 Bluetooth LE module.

.. image:: img/adafruit_feather_m0_bluefruit_le.webp
   :align: center
   :alt: Adafruit Feather M0 Bluefruit LE

Hardware
********

- ATSAMD21G18A ARM Cortex-M0+ processor at 48 MHz
- 32.768 kHz crystal oscillator
- 256 KiB flash memory and 32 KiB of RAM
- Battery connector and charger for 3.7 V lithium polymer batteries
- Charging indicator LED
- User LED
- Reset button
- Native USB port
- nRF51822 Bluetooth LE module

Supported Features
==================

.. zephyr:board-supported-hw::

Connections and IOs
===================

The `Adafruit Feather M0 Bluefruit LE Learn site`_ has detailed
information about the board including `pinouts`_ and the `schematic`_.

System Clock
============

The SAMD21 MCU is configured to use the 32.768 kHz external oscillator
with the on-chip PLL generating the 48 MHz system clock.

Serial Port
===========

The SAMD21 MCU has 6 SERCOM based USARTs.  On the Adafruit Feather M0
Bluefruit LE, SERCOM0 is the Zephyr console and is available on pins 0
(RX) and 1 (TX).

I2C Port
========

The SAMD21 MCU has 6 SERCOM based I2C controllers.  On the Adafruit
Feather M0 Bluefruit LE, SERCOM3 is available on pin 20 (SDA) and pin
21 (SCL).

SPI Port
========

The SAMD21 MCU has 6 SERCOM based SPIs.  On the Adafruit Feather M0
Bluefruit LE, SERCOM4 is available on pin 22 (MISO), pin 23 (MOSI), and
pin 24 (SCK).  SERCOM4 is also used by the on-board Bluetooth LE module.

Bluetooth LE
============

The on-board nRF51822 Bluetooth LE module communicates with the SAMD21
over SERCOM4 SPI using Adafruit's proprietary SDEP (Simple Data Exchange
Protocol).  The module chip select, interrupt, and reset lines are
connected to PA06, PA21, and PA08 respectively.  These signals are not
exposed on the Feather header and are reserved for the BLE module.

There is currently no Zephyr driver for the SDEP protocol.  An
application that requires Bluetooth LE must provide its own driver or
use the module in a pass-through mode.

USB Device Port
===============

The SAMD21 MCU has a USB device port that can be used to communicate
with a host PC.  See the :zephyr:code-sample-category:`usb` sample
applications for more, such as the :zephyr:code-sample:`usb-cdc-acm`
sample which sets up a virtual serial port that echos characters back to
the host PC.

Programming and Debugging
*************************

.. zephyr:board-supported-runners::

The Adafruit Feather M0 Bluefruit LE ships with a BOSSA compatible
SAM-BA bootloader.  The bootloader can be entered by quickly tapping
the reset button twice.

Flashing
========

#. Build the Zephyr kernel and the :zephyr:code-sample:`hello_world` sample application:

   .. zephyr-app-commands::
      :zephyr-app: samples/hello_world
      :board: adafruit_feather_m0_bluefruit_le
      :goals: build
      :compact:

#. Connect the Adafruit Feather M0 Bluefruit LE to your host computer
   using USB

#. Connect a 3.3 V USB to serial adapter to the board and to the
   host.  See the `Serial Port`_ section above for the board's pin
   connections.

#. Run your favorite terminal program to listen for output. Under Linux the
   terminal should be :code:`/dev/ttyACM0`. For example:

   .. code-block:: console

      $ minicom -D /dev/ttyACM0 -o

   The -o option tells minicom not to send the modem initialization
   string. Connection should be configured as follows:

   - Speed: 115200
   - Data: 8 bits
   - Parity: None
   - Stop bits: 1

#. Tap the reset button twice quickly to enter bootloader mode

#. Flash the image:

   .. zephyr-app-commands::
      :zephyr-app: samples/hello_world
      :board: adafruit_feather_m0_bluefruit_le
      :goals: flash
      :compact:

   You should see "Hello World! adafruit_feather_m0_bluefruit_le" in your terminal.

References
**********

.. target-notes::

.. _Adafruit Feather M0 Bluefruit LE Learn site:
    https://learn.adafruit.com/adafruit-feather-m0-bluefruit-le

.. _pinouts:
    https://learn.adafruit.com/adafruit-feather-m0-bluefruit-le/pinouts

.. _schematic:
    https://learn.adafruit.com/adafruit-feather-m0-bluefruit-le/downloads
