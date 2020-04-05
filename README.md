# Hardware agnostic I2C driver for AXP192 PMU

To use this library you must to provide HAL functions for both reading and writing the I2C bus. Function definitions must be the following.

```c
int32_t i2c_read(uint8_t address, uint8_t reg, uint8_t *buffer, uint16_t size);
int32_t i2c_write(uint8_t address, uint8_t reg, const uint8_t *buffer, uint16_t size);
```

Where `address` is the I2C address, `reg` is the register to read or write, `buffer` holds the data to write or read into and `size` is the amount of data to read or write. For example HAL implementation see [ESP I2C master HAL](https://github.com/tuupola/esp_i2c_hal). For minimal working example see [M5Stick RTC demo](https://github.com/tuupola/esp-examples/tree/master/017-m5stick-rtc).

## Usage

```
$ make menuconfig
```

```c
#include "axp192.h"
#include "your-i2c-hal.h"

float vacin, iacin, vvbus, ivbus, temp, vbat, icharge, idischarge;

axp192_init(i2c_read, i2c_write);
axp192_read(AXP192_ACIN_VOLTAGE, &vacin);
axp192_read(AXP192_ACIN_CURRENT, &iacin);
axp192_read(AXP192_VBUS_VOLTAGE, &vvbus);
axp192_read(AXP192_VBUS_CURRENT, &ivbus);
axp192_read(AXP192_TEMP, &temp);
axp192_read(AXP192_BATTERY_VOLTAGE, &vbat);
axp192_read(AXP192_CHARGE_CURRENT, &icharge);
axp192_read(AXP192_DISCHARGE_CURRENT, &idischarge);

printf(
    "vacin: %.2fV iacin: %.2fA vvbus: %.2fV ivbus: %.2fA temp: %.0fC",
    vacin, iacin, vvbus, ivbus, temp
);

printf(
    "vbat: %.2fV ichage: %.2fA idischarge: %.2fA",
    vbat, icharge, idischarge
);

```