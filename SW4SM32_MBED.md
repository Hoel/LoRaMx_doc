## Setting up a SW4STM32 (AC6) project exported from MBED online compiler


### When an SW4STM32 project is exported from MBED online compiler few settings have to be adjusted so that the project can build:

* go to **project properties / C/C++ build / MCU GCC compiler / includes** and change includes files to point to the actual **mbed_config.h** situated at the root of project folder
* go to **project properties / C/C++ build / MCU G++ compiler / includes** and change includes files to point to the actual **mbed_config.h** situated at the root of project folder
* go to **project properties / C/C++ build / MCU G++ compiler /miscellaneous / linker flags** and remove the following flags: **-Wl,--wrap=_malloc_r -Wl,--wrap=_free_r -Wl,--wrap=_calloc_r**


### STLink connection and configuration:

On windows you should install the STLink driver, you can do so by installing the [STLink utility](http://www.st.com/en/development-tools/stsw-link004.html). On Mac and Linux no driver installation is usually required.
We assume the STLink debugger is connected via **GND VCC DIO CLK**, with **RESET** line omitted.
If you want to use the reset line change reset mode to : **hardware reset** in **debug/run configuration** as explained below. 
_N.B. unless special cases there is no interrest to use **reset** line, we advise to connect **GND VCC DIO CLK** only._ 


### For the first run of the project run/debug configuration has to be setup:

* Go to contextual menu of the run button (green button with arrow)
* select **run as** / **AC6 STM32 C/C++ application**
* the upload will attempt and fail because the reset mode is not set yet
* return to contextual menu of run button, select **run configuration** go to debugger tab, clic **show generator options**
* find **reset mode** and select **software reset** run button is now functional, it will compile, upload and reset board automatically


### RUN / ISP switch:

Most boards have a RUN / ISP DIP switch, this switch can be used in the eventuality you need to use the internal bootlader from UART since some variants only offer internal (read only ROM) bootloader on UART (namely STM32F103, STM32L151) to do so you can set the RUN / ISP switch to **OFF** (ISP). In all other cases, we advise to always let the RUN / ISP switch set to **ON**, this will not interfere the upload nor debug when STlink is connected.


### FAST CHARGE switch / solder jumper:

When set to **ON** the **fast charge** DIP switch allows maximum current current charging to LiPo (1000mA), by default (set to **OFF**) charging current is 100mA. Some LoRaMx boards have a solder jumper instead of a DIP switch, solder jumper open charging current is 100mA, solder jumper closed it is 1000mA. 
