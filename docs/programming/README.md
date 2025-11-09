# Programming ESPHome Devices

This section covers how to program and flash ESPHome firmware onto ESP32 devices.

## Programming Methods

### USB Serial Adapter

Most common method using a USB-to-serial adapter:

```bash
esptool --port /dev/tty.usbserial-1130 write_flash 0x0 Downloads/testwt32-eth01.factory.bin
```

### Finding USB Ports

List available USB serial ports:

```bash
ls -lha /dev/tty* | grep usb
```

## Boot Modes

### Programming Mode

To enter programming mode:

1. Disconnect VCC
2. Connect EN (enable) to GND
3. Connect VCC
4. Disconnect EN from GND

### Normal Boot Mode

Ensure IO0 is pulled high or floating for normal operation.

## ESPHome CLI

Install ESPHome and use the command line tools:

```bash
pip install esphome
esphome run device.yaml
```

## PlatformIO

Use PlatformIO for advanced development:

```bash
platformio run -t upload
```

## Troubleshooting

- **Boot failures**: Check strapping pins (IO0, IO2, IO12, IO15)
- **Programming errors**: Verify correct port and baud rate
- **Power issues**: Ensure stable power supply during programming
- **Driver problems**: Install appropriate USB serial drivers

## Resources

- [ESPHome Getting Started](https://esphome.io/guides/getting_started.html)
- [esptool Documentation](https://github.com/espressif/esptool)
- [PlatformIO ESP32 Guide](https://docs.platformio.org/en/latest/boards/espressif32/)