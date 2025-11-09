# DS18B20 Digital 1-Wire Thermometer

The DS18B20 can be connected to a GPIO of the ESP32 using the [one_wire bus](https://esphome.io/components/one_wire/) 
over [GPIO](https://esphome.io/components/one_wire/gpio/)
and a [Dallas Temperature Sensor](https://esphome.io/components/sensor/dallas_temp/)

## Wiring

The DS28B20 can be used in parasitic power mode (without Vcc), or with a 3-5V power supply. The Data line should be pulled up to Vcc with a 2.7kΩ Resistor for 5V and 4.7kΩ for 3.3V.

![Wiring](wiring.jpg)

## ESP Home Example Code

```yml
one_wire:
  - platform: gpio
    id: one_wire_1
    pin: GPIOXX

# Example configuration entry
sensor:
  - platform: dallas_temp
    address: 0x1234567812345628
    resolution: 12
    name: temperature
    update_interval: 120s
    one_wire_id: one_wire_1
```

`adress` is optional and will be printed by `one_wire` during startup and bus scan.  
`resolution` is between 9 and 12, default is 12.  
`id` and `one_wire_id` is optional if there is only one.

## References

[Makersguide ESP32 and DS18B20](https://www.makerguides.com/esp32-ds18b20-digital-thermometer/)