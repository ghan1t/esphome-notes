# ESP32-CAM

The ESP32-CAM is a dual core ESP32-S board, that is equvalent to Espressif's ESP-WROOM-32 module. It comes with an OV2640 camera sensor, a MicroSD card slot, WIFI and an LED (connected to GPIO33).

## Programming

Connect programmer to GPIO1 and GPIO3 (reverse RX and TX between programmer and ESP32) and either 5v or 3v. Bridge IO0 to GND, press reset and start programming. Remove the Bridge between IO0 to GND after programming.

![Programming](ESP32-CAM-FTDI-programmer.webp)

## Pinout

![PINOUT 1](ESP32-CAM-Pinout.png)

![PINOUT 2](ESP32-CAM-pinout-mischianti.png)

## Pin Restrictions

⚠️ – Pay close attention because their behavior, particularly during boot, can be unpredictable. Also, some GPIOs are shared with the microSD card. So use them with caution.  
❌ – It is recommended that you avoid using these pins.  
✅ – Your top priority pins. They are perfectly safe to use.

| Label | GPIO | Safe to use? | Reason |
|-------|------|--------------|--------|
| D0    | 0    | ⚠️          | must be HIGH during boot and LOW for flashing |
| TX0   | 1    | ❌          | Tx pin, used for flashing and debugging |
| D2    | 2    | ⚠️          | must be LOW during boot, cannot be used when microSD card is present |
| RX0   | 3    | ❌          | Rx pin, used for flashing and debugging |
| D4    | 4    | ⚠️          | Connected to the on-board Flash LED, cannot be used when microSD card is present |
| D12   | 12   | ⚠️          | must be LOW during boot, cannot be used when microSD card is present |
| D13   | 13   | ⚠️          | cannot be used when microSD card is present |
| D14   | 14   | ⚠️          | cannot be used when microSD card is present |
| D15   | 15   | ⚠️          | must be HIGH during boot, prevents startup log if pulled LOW, cannot be used when microSD card is present |
| RX2   | 16   | ✅          | |

## References

[Pinout](https://lastminuteengineers.com/esp32-cam-pinout-reference/)

[ESPHome](https://devices.esphome.io/devices/esp32-cam/)

[Camera Example](https://devices.esphome.io/devices/esp32-cam/) [Camera Webserver](https://esphome.io/components/esp32_camera_web_server/)

## Example with Camera

```yaml
esphome:
  name: esp32-cam
  friendly_name: esp32-cam

esp32:
  board: esp32dev
  framework:
    type: esp-idf

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "key"

ota:
  - platform: esphome
    password: "ota"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  manual_ip:
    static_ip: ip
    gateway: router
    subnet: 255.255.255.0

web_server:
  port: 80

esp32_camera:
  external_clock:
    pin: GPIO0
    frequency: 20MHz
  i2c_pins:
    sda: GPIO26
    scl: GPIO27
  data_pins: [GPIO5, GPIO18, GPIO19, GPIO21, GPIO36, GPIO39, GPIO34, GPIO35]

  # the order of the data_pins is significant, don't mix up the order

  vsync_pin: GPIO25
  href_pin: GPIO23
  pixel_clock_pin: GPIO22
  power_down_pin: GPIO32
  resolution: 800x600
  name: esp_cam02
  idle_framerate: 0.1fps

# Example configuration entry
esp32_camera_web_server:
  - port: 8080
    mode: stream
  - port: 8081
    mode: snapshot
  
output:
  - platform: ledc
    pin: GPIO4
    channel: 2 # channel 1 is used for esp32_camera
    id: led
light:
  - platform: monochromatic
    output: led
    name: espcam_02 light
```