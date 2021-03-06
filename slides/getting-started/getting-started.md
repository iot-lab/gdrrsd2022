class: center, middle

# Tutorial IoT on Microcontrollers

## Getting started

---

## Your working environment

- The [FIT IoT-LAB](https://www.iot-lab.info) testbed will be used to perform
  the exercises that require hardware.

- We provide temporary accounts, just for this tutorial.

- For the ease of use, all exercises are performed online in Jupyter Notebooks

.center[
    <img src="images/jupyter.png" alt="" style="width:600px;"/>
]

---

## About the Jupyter Notebooks

.center[
Available at **https://labs.iot-lab.info**


<img src="images/iotlab-jupyterhub.png" alt="" style="width:300px;"/>

**Short demo: discover Jupyterlab notebooks!**
<form class=notebook>
    <input class=login id="login_start" type="text" oninput="check_login('login_start', 'launcher_start')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_start" type="button" value="Launch notebook" onclick="open_notebook('login_start', 'start.ipynb')">
</form>
]

---

## Your first experiment on IoT-LAB

Let's launch a simple experiment on IoT-LAB!

.center[
<form class=notebook>
    <input class=login id="login_experiment" type="text" oninput="check_login('login_experiment', 'launcher_experiment')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_experiment" type="button" value="Launch notebook" onclick="open_notebook('login_experiment', 'first-experiment/first-experiment.ipynb')" disabled>
</form>
]

---

## Advanced monitoring manipulations on IoT-LAB (1)

IoT-LAB provides power-consumption monitoring, let's see how to work with this feature:

.center[
<form class=notebook>
    <input class=login id="login_consumption" type="text" oninput="check_login('login_consumption', 'launcher_consumption')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_consumption" type="button" value="Launch notebook" onclick="open_notebook('login_consumption', 'testbed/monitoring/consumption.ipynb')" disabled>
</form>
]

---

## Advanced monitoring manipulations on IoT-LAB (2)

IoT-LAB provides radio RSSI monitoring per node, let's see how to work with this feature:

.center[
<form class=notebook>
    <input class=login id="login_radio" type="text" oninput="check_login('login_radio', 'launcher_radio')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_radio" type="button" value="Launch notebook" onclick="open_notebook('login_radio', 'testbed/monitoring/radio.ipynb')" disabled>
</form>
]

---

class: center, middle

# Play with RIOT

---

## Structure of a RIOT application

A minimal RIOT application consists in:

- A `Makefile`

```mk
APPLICATION = example

BOARD ?= native

RIOTBASE ?= $(CURDIR)/../../../RIOT

DEVELHELP ?= 1

include $(RIOTBASE)/Makefile.include
```

- A C-file containing the main function

```c
#include <stdio.h>

int main(void)
{
    puts("My first RIOT application");
    return 0;
}
```

---

## Build a RIOT application

- The build system of RIOT is based on **make** build tool


- To build an application, call **make** from the application directory:
  ```sh
  $ cd <application_directory>
  $ make
  ```

  ```sh
  $ make -C <application_directory>
  ```

---

## Run a RIOT application

This depends on the target board:

- Running on **native**: the RIOT application executed is a simple Linux process
```sh
$ make BOARD=native -C <application_dir>
$ <application_dir>/bin/native/application.elf
```

- Running on **hardware**: the RIOT application must be *flashed* first on the
  board

&#x21d2; use the **flash** and **term** targets with make
  - **flash**: build and write the firmware on the MCU flash memory

  - **term**: opens a terminal client connected to the serial port of the
    target

All this can be done in one command:

```sh
$ make BOARD=<target> -C <application_dir> flash term
```

*Note:* the last command can also be used with **native** target

---

## Exercise: your first RIOT application

Let's build and run our first RIOT application !<br><br>

.center[
<form class=notebook>
    <input class=login id="login_hello" type="text" oninput="check_login('login_hello', 'launcher_hello')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_hello" type="button" value="Launch notebook" onclick="open_notebook('login_hello', 'riot/basics/hello-world/hello-world.ipynb')" disabled>
</form>
]

---

## How to extend the application

&#x21d2; by adding modules in the application `Makefile` or from the command line:

- Add extra modules with **USEMODULE**<br>
    &#x21d2; `xtimer`, `fmt`, `shell`, `ps`, etc

- Include external packages with **USEPKG**<br>
    &#x21d2; `lwip`, `semtech-loramac`, etc

- Use MCU peripherals drivers with **FEATURES_REQUIRED**:<br>
    &#x21d2; `periph_gpio`, `periph_uart`, `periph_spi`, `periph_i2c`

--

Example in a `Makefile`:
```mk
USEMODULE += xtimer shell

USEPKG += semtech-loramac

FEATURES_REQUIRED += periph_gpio
```
Example from the command line:
```sh
$ USEMODULE=xtimer make BOARD=b-l072z-lrwan1
```

---

## Exercise: read sensor data using the shell

Let's write a more advanced RIOT application to read sensors values.
<br>

The application will use advanced techniques to read some data in a separate thread and use mutexes to synchronize the threads!

<br>
.center[
<form class=notebook>
    <input class=login id="login_sensors" type="text" oninput="check_login('login_sensors', 'launcher_sensors')" placeholder="Enter your IoT-LAB login">
    <input class=launcher id="launcher_sensors" type="button" value="Launch notebook" onclick="open_notebook('login_sensors', 'riot/basics/sensors/sensors.ipynb')" disabled>
</form>
]

---

## Go further: extra hands-on activities

- [LwM2M](https://iot-lab.github.io/gdrrsd2022/slides/lwm2m): use 802.15.4 and IPv6 to interact with a LwM2M server

- [LoRaWAN](https://iot-lab.github.io/gdrrsd2022/slides/lorawan): send sensor data over LoRaWAN and display them on a web dashboard

- [Security](https://iot-lab.github.io/gdrrsd2022/slides/security): discover security in IoT and perform a firmware update
