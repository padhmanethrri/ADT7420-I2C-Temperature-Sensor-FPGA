# I2C-Based Temperature Sensor Interface on Nexys A7 FPGA

A Verilog HDL implementation of an **I2C-based temperature sensing system** using the **ADT7420 temperature sensor** and the **Nexys A7 FPGA board**.

The FPGA acts as the **I2C master**, communicates with the ADT7420 temperature sensor, reads the temperature data, and displays the result using **7-segment displays and LEDs**.

## Overview

This project demonstrates the implementation of an I2C temperature sensor interface on a Xilinx Artix-7 FPGA.

### Main features

* I2C master implemented in Verilog HDL
* ADT7420 temperature sensor interface
* 100 MHz FPGA clock divided to 200 kHz
* 10 kHz SCL generated for I2C communication
* Temperature data read from the ADT7420
* Temperature output displayed on:

  * 8 LEDs in binary format
  * 7-segment displays in decimal format
* Simulation, synthesis, and FPGA implementation using Xilinx Vivado

## Hardware Used

| Component          | Specification                    |
| ------------------ | -------------------------------- |
| FPGA Board         | Digilent Nexys A7                |
| FPGA               | Xilinx Artix-7 XC7A100T-1CSG324C |
| Temperature Sensor | ADT7420                          |
| Programming/Power  | USB Cable                        |

## Software

* **Xilinx Vivado**
* **Verilog HDL**

## Working Principle

The Nexys A7 provides a **100 MHz clock**, which is first divided to **200 kHz** using the `clkgen_200kHz` module.

The `i2c_master` module then uses this clock to generate a **10 kHz SCL** signal for communication with the ADT7420.

The FPGA acts as the I2C master and communicates with the ADT7420 slave by sending the device address and reading the temperature data.

The received temperature data is then:

* Displayed in binary using the **8 LEDs**
* Displayed using the **7-segment displays** through the `seg7` module

### Communication Flow

```text
100 MHz FPGA Clock
        |
        v
clkgen_200kHz
        |
        v
   200 kHz Clock
        |
        v
   i2c_master
        |
        | 10 kHz SCL
        | SDA
        v
    ADT7420
 Temperature Sensor
        |
        v
 Temperature Data
        |
        +-------------> 8 LEDs
        |
        +-------------> 7-Segment Display
```

## Project Files

| File                    | Description                            |
| ----------------------- | -------------------------------------- |
| `clkgen_200kHz.v`       | Clock generation/division module       |
| `i2c_master.v`          | I2C master controller                  |
| `i2c_master_TB.v`       | Testbench for simulation               |
| `seg7.v`                | 7-segment display driver               |
| `top.v`                 | Top-level module connecting the system |
| `const_temp_sensor.xdc` | FPGA pin and timing constraints        |

## Simulation

The design can be simulated using the provided testbench:

```text
i2c_master_TB.v
```

The simulation can be used to observe the I2C communication and verify the operation of the design before FPGA implementation.

## FPGA Implementation

The project can be opened and synthesized using **Xilinx Vivado**.

The generated bitstream can then be programmed onto the **Nexys A7 FPGA board** through USB.

