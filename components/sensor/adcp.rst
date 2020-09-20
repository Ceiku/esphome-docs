ADCP Sensor
===========

.. _adcp-component:

Component
---------
The ``adcp`` domain binds an analog input source, such as an analog input pin and multiplexes the power to each attached sensor using binary GPIO pins.
This allows for the creation of individual sensors using the :ref:`ADCP Sensor Platform <adcp-sensor>`.

.. code-block:: yaml

    adcp:
      sensor: adc0

    sensor:
      - platform: adc
        pin: A0
        id: adc0

Configuration variables:
************************

- **sensor** (**Required**, string): The id of the voltage_sampler/analog source.
  The example above shows a general configuration using the on-board analog pin. :ref:`ADC Sensor <adc-sensor>`

.. _adcp-sensor:

Sensor
------

The ``adcp`` sensor allows you to use multiple analog sensors on one analog input source.
Each sensor specifies a pin for powering the attached sensor, and the data lines are wired in paralell to the on-board analog input.
First, setup a :ref:`ADCP Component <adcp-component>` and then use this
sensor platform to create individual sensors that will report the
voltage to Home Assistant.


.. code-block:: yaml

    adcp:
      sensor: adc0
      
    sensor:
      - platform: adc
        pin: A0
        id: adc0
        
      - platform: adcp
        pin: D0
        name: adcp0
      - platform: adcp
        pin: D1
        name: adcp1
        delay: 100ms

Configuration variables:
************************

-  **name** (**Required**, string): The name for this sensor.
-  **pin** (**Required**, int): The digital pin to power the sensor.
-  **update_interval** (*Optional*, :ref:`config-time`): The interval
   to check the sensor. Defaults to ``60s``.
-  **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.
