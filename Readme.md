FPGA-SoC-Linux-Example-1-PYNQ-Z1
================================

FPGA-SoC-Linux example(1) binary and project and test code for PYNQ-Z1

### Requirement

* Board: PYNQ-Z1
* OS:
   + ~~[FPGA-SoC-Linux](https://github.com/ikwzm/FPGA-SoC-Linux.git)~~
   + [FPGA-SoC-Debian12](https://github.com/ikwzm/FPGA-SoC-Debian12.git)
   + [FPGA-SoC-Debian13](https://github.com/ikwzm/FPGA-SoC-Debian13.git)

## Install

### Install python3-numpy

```console
shell# apt-get install python3-numpy
```

### Download FPGA-SoC-Linux-Example-1-PYNQ-Z1

```console
shell$ git clone FPGA-SoC-Linux-Example-1-PYNQ-Z1
shell$ cd FPGA-SoC-Linux-Example-1-PYNQ-Z1
```

### Install to FPGA and Device Tree

```console
shell# rake install
cp pump_axi4.bin /lib/firmware/pump_axi4.bin
dtbocfg.rb --install uio_irq_sample --dts uio_irq_sample.dts
<stdin>:22.13-27.20: Warning (unit_address_vs_reg): /fragment@1/__overlay__/pump-uio: node has a reg or ranges property, but no unit name
<stdin>:9.13-41.4: Warning (avoid_unnecessary_addr_size): /fragment@1: unnecessary #address-cells/#size-cells without "ranges", "dma-ranges" or child "reg" property
[   58.676407] fpga_manager fpga0: writing pump_axi4.bin to Xilinx Zynq FPGA Manager
[   58.988398] OF: overlay: WARNING: memory leak will occur if overlay removed, property: /axi/fpga-region0/firmware-name
[   59.075681] fclkcfg axi:fclk0: driver version : 1.9.0
[   59.080768] fclkcfg axi:fclk0: device name    : axi:fclk0
[   59.104802] fclkcfg axi:fclk0: clock  name    : fclk0
[   59.109918] fclkcfg axi:fclk0: clock  rate    : 100000000
[   59.115572] fclkcfg axi:fclk0: clock  enabled : 1
[   59.120316] fclkcfg axi:fclk0: driver installed.
[   59.121092] u-dma-buf udmabuf4: driver version = 5.3.0
[   59.136082] u-dma-buf udmabuf4: major number   = 243
[   59.141081] u-dma-buf udmabuf4: minor number   = 0
[   59.149413] u-dma-buf udmabuf4: phys address   = 0x1f100000
[   59.155276] u-dma-buf udmabuf4: buffer size    = 1048576
[   59.160629] u-dma-buf axi:pump-udmabuf4: driver installed.
[   59.177059] u-dma-buf udmabuf5: driver version = 5.3.0
[   59.182238] u-dma-buf udmabuf5: major number   = 243
[   59.190735] u-dma-buf udmabuf5: minor number   = 1
[   59.201493] u-dma-buf udmabuf5: phys address   = 0x1f200000
[   59.211009] u-dma-buf udmabuf5: buffer size    = 1048576
[   59.218206] u-dma-buf axi:pump-udmabuf5: driver installed.
```

## Run sample1 or sample2

### Compile sample1 or sample2

```console
shell# rake sample1 sample2
```

### Run sample1

```console
shell# ./sample1
elapsed_time = 6.301379 [msec]
elapsed_time = 6.329146 [msec]
elapsed_time = 6.341878 [msec]
elapsed_time = 6.318863 [msec]
elapsed_time = 6.343589 [msec]
elapsed_time = 6.312727 [msec]
elapsed_time = 6.334130 [msec]
elapsed_time = 6.314487 [msec]
elapsed_time = 6.335140 [msec]
elapsed_time = 6.305995 [msec]
```

### Run sample2

```console
shell# ./sample2
elapsed_time = 6.324314 [msec]
elapsed_time = 6.347614 [msec]
elapsed_time = 6.316893 [msec]
elapsed_time = 6.345872 [msec]
elapsed_time = 6.345226 [msec]
elapsed_time = 6.337047 [msec]
elapsed_time = 6.338420 [msec]
elapsed_time = 6.354789 [msec]
elapsed_time = 6.352918 [msec]
elapsed_time = 6.345540 [msec]
```

## Run sample.py

```console
shell# python3 sample.py
elapsed_time:6.48[msec]
elapsed_time:6.387[msec]
elapsed_time:6.271[msec]
elapsed_time:6.32[msec]
elapsed_time:6.323[msec]
elapsed_time:6.264[msec]
elapsed_time:6.311[msec]
elapsed_time:6.294[msec]
elapsed_time:6.253[msec]
average_time:6.322[msec]
thougput    :165.851[MByte/sec]
udmabuf4 == udmabuf5 : OK
```

## Uninstall

```console
shell# rake uninstall
dtbocfg.rb --remove uio_irq_sample
[  230.245811] u-dma-buf axi:pump-udmabuf5: driver removed.
[  230.253000] u-dma-buf axi:pump-udmabuf4: driver removed.
[  230.264141] fclkcfg axi:fclk0: driver removed.
```


## Build Bitstream file

### Requirement

* Vivado 2016.1 - 2017.2.1 or 2025.1

### Download FPGA-SoC-Linux-Example-1-Base

```
shell$ pushd FPGA-SoC-Linux-Example-1-Base
shell$ git submodule init
shell$ git submodule update
shell$ popd
```

### Create Project

```
Vivado > Tools > Run Tcl Script > project/create_project.tcl
```

### Implementation

```
Vivado > Tools > Run Tcl Script > project/implementation.tcl
```

### Convert from Bitstream File to Binary File

```
shell$ python3 tools/fpga-bit-to-bin.py --flip project/project.runs/impl_1/design_1_wrapper.bit pump_axi4.bin
```
