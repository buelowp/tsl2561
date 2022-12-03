# TSL2561

Raspberry Pi C driver for the TSL2561 sensor.

This driver is basically a port of the [Adafruit TSL2561 Light Sensor Driver](https://github.com/adafruit/Adafruit_TSL2561).

This fork drops the Python support as that is readily available using pip3 and the Adafruit install mechanism. Resources to use python can be found elsewhere.

## Configure I2C

Install the following packages:
* i2c-tools 
* libi2c-dev

```
# sudo apt install i2c-tools libi2c-dev
```

Depending on usage needs, you can instanatiate a new I2C bus if you need, or use the exposed /dev/i2c-1 which is available using raspi-config.

To create a new i2c bus see the following

https://www.instructables.com/Raspberry-PI-Multiple-I2c-Devices/

## Building the driver
### C language

This library uses cmake. Change directory into the parent and do the following
```
# mkdir build
# cd build
# cmake ..
# make
# sudo make install
```

## Usage
### C language

```c
#include "tsl2561.h"
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>

int main(int argc, char **argv) {
	int address = 0x39;
	char *i2c_device = "/dev/i2c-1";

	void *tsl = tsl2561_init(address, i2c_device);
	tsl2561_enable_autogain(tsl);
	tsl2561_set_integration_time(tsl, TSL2561_INTEGRATION_TIME_13MS);
 
	if(tsl == NULL){ // check if error is present
		exit(1);
	} 
	
	int c;
	long lux;
	for(c = 0; c < 5; c++){
		lux = tsl2561_lux(tsl);
		printf("lux %lu\n", lux);
		usleep(3 * 1000 * 1000);
	}
	
	tsl2561_close(tsl);
	i2c_device = NULL;
	return 0;
}

```

## License
Adafruit_TSL2561, a C++ library, is licensed under BSD as specified [here](https://github.com/adafruit/Adafruit_TSL2561); the derivative work tsl2561 is provided under the MIT licence. This fork maintains the MIT license.
