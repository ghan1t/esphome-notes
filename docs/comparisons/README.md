# Hardware Comparisons

This section provides comparisons between different ESP32 boards and Ethernet modules to help you choose the right hardware for your project.

## Ethernet Modules

### ETH01-EVO (ESP32-C3)

- **Ethernet**: DM9051 over SPI instead of PHY (uses less GPIOs)
- **Core**: 32-bit Single Core
- **GPIO**: 10
- **PoE**: Supported
- **Price**: ~EUR 12.- / 22.- with PoE
- **Notes**: Native SPI interface used for Ethernet, not usable for anything else
- **Resources**: https://community.home-assistant.io/t/how-to-esphome-on-the-wt32-eth01-evo-esp32-c3/752518/6
- **AliExpress**: https://www.aliexpress.com/item/1005006528549724.html

### ESP32-S3-ETH

- **Ethernet**: W5500 over PHY
- **Core**: 32-bit Dual Core 240MHz
- **GPIO**: 48 (-6 for Ethernet)
- **PoE**: Supported
- **Notes**: USB-C for flashing, MicroSD
- **Price**: ~EUR 18.- / 22.- with PoE
- **AliExpress**: https://www.aliexpress.com/item/1005008155822956.html or https://www.aliexpress.com/item/1005007945002026.html

### LilyGO T-ETH-Series

- **Ethernet**: RTL8201 RMII
- **Core**: 32-bit Dual Core 240MHz
- **GPIO**: 46 (-6 for Ethernet)
- **PoE**: Supported
- **Price**: ~EUR 15 / 21.- with PoE
- **Notes**: Good documentation and community support
- **Resources**: https://github.com/Xinyuan-LilyGO/LilyGO-T-ETH-Series
- **AliExtress**: https://www.aliexpress.com/item/1005006021822040.html

### WT32-ETH01 (ESP32-S1-ETH)

- **Ethernet**: LAN8720 RMII
- **GPIO**: 13
- **PoE**: NOT Supported
- **Price**: ~EUR 4.50
- **Notes**: Smallest and cheapest Ethernet option
- **Resources**: https://wled.discourse.group/t/wt32-eth01-lan-wifi-flash-tutorial/2786 https://community.home-assistant.io/t/how-i-installed-esphome-on-the-wt32-eth01/359027

### Olimex ESP32-POE

- **Ethernet**: Built-in PoE support
- **Price**: Varies
- **Notes**: Commercial option with good support

## Performance Notes

- SPI Ethernet modules may have lower throughput than RMII / PHY
- Dual-core ESP32-S3 offers better performance for complex applications
- Check flash size (usually 4MB minimum for ESPHome)

## Resources

- [ESPHome Ethernet Documentation](https://esphome.io/components/ethernet.html)
- [ESP32 Comparison Chart](https://products.espressif.com/)