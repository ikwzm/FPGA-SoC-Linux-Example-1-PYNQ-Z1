FPGA-SoC-Linux-Example-1-PYNQ-Z1
================================

FPGA-SoC-Linux example(1) binary and project and test code for PYNQ-Z1

### Requirement

* Board: PYNQ-Z1
* OS: [FPGA-SoC-Linux](https://github.com/ikwzm/FPGA-SoC-Linux.git)

## Install

### Install python3-numpy

```
shell# apt-get install python3-numpy
```

### Download FPGA-SoC-Linux-Example-1-PYNQ-Z1

```
shell$ git clone FPGA-SoC-Linux-Example-1-PYNQ-Z1
shell$ cd FPGA-SoC-Linux-Example-1-PYNQ-Z1
```

### Install to FPGA and Device Tree

```
shell# rake install
cp pump_axi4.bin /lib/firmware/pump_axi4.bin
dtbocfg.rb --install uio_irq_sample --dts uio_irq_sample.dts
/config/device-tree/overlays/uio_irq_sample/dtbo: Warning (unit_address_vs_reg): Node /fragment@0 has a unit name, but no reg property
/config/device-tree/overlays/uio_irq_sample/dtbo: Warning (unit_address_vs_reg): Node /fragment@1 has a unit name, but no reg property
/config/device-tree/overlays/uio_irq_sample/dtbo: Warning (unit_address_vs_reg): Node /fragment@1/__overlay__/pump-uio has a reg or ranges property, but no unit name
[  890.222539] fpga_manager fpga0: writing pump_axi4.bin to Xilinx Zynq FPGA Manager
[  890.300541] OF: overlay: WARNING: memory leak will occur if overlay removed, property: /amba/fpga-region0/firmware-name
[  890.314198] fclkcfg amba:fclk0: driver installed.
[  890.320780] fclkcfg amba:fclk0: device name    : amba:fclk0
[  890.326894] fclkcfg amba:fclk0: clock  name    : fclk0
[  890.332038] fclkcfg amba:fclk0: clock  rate    : 100000000
[  890.337590] fclkcfg amba:fclk0: clock  enabled : 1
[  890.349545] u-dma-buf udmabuf4: driver version = 3.0.1
[  890.356273] u-dma-buf udmabuf4: major number   = 242
[  890.361255] u-dma-buf udmabuf4: minor number   = 0
[  890.366709] u-dma-buf udmabuf4: phys address   = 0x1f100000
[  890.372284] u-dma-buf udmabuf4: buffer size    = 1048576
[  890.377709] u-dma-buf udmabuf4: dma device     = amba:pump-udmabuf4
[  890.383984] u-dma-buf udmabuf4: dma coherent   = 1
[  890.388830] u-dma-buf amba:pump-udmabuf4: driver installed.
[  890.401043] u-dma-buf udmabuf5: driver version = 3.0.1
[  890.406288] u-dma-buf udmabuf5: major number   = 242
[  890.411257] u-dma-buf udmabuf5: minor number   = 1
[  890.418866] u-dma-buf udmabuf5: phys address   = 0x1f200000
[  890.424433] u-dma-buf udmabuf5: buffer size    = 1048576
[  890.431504] u-dma-buf udmabuf5: dma device     = amba:pump-udmabuf5
[  890.438686] u-dma-buf udmabuf5: dma coherent   = 1
[  890.443477] u-dma-buf amba:pump-udmabuf5: driver installed.
```

## Run sample1 or sample2

### Compile sample1 or sample2

```
shell# rake sample1 sample2
```

### Run sample1

```
shell# ./sample1
time = 0.005896 sec
time = 0.005954 sec
time = 0.005917 sec
time = 0.005864 sec
time = 0.005963 sec
time = 0.005935 sec
time = 0.005925 sec
time = 0.005893 sec
time = 0.005916 sec
time = 0.005903 sec
```

### Run sample2

```
shell# ./sample2
time = 0.005907 sec
time = 0.005948 sec
time = 0.005917 sec
time = 0.005929 sec
time = 0.005916 sec
time = 0.005960 sec
time = 0.005904 sec
time = 0.005975 sec
time = 0.005909 sec
time = 0.005946 sec
```

## Run sample.py

```
shell# python3 sample.py
elapsed_time:5.948[msec]
elapsed_time:5.874[msec]
elapsed_time:5.882[msec]
elapsed_time:5.888[msec]
elapsed_time:5.865[msec]
elapsed_time:5.876[msec]
elapsed_time:5.86[msec]
elapsed_time:5.882[msec]
elapsed_time:5.889[msec]
average_time:5.885[msec]
thougput    :178.178[MByte/sec]
udmabuf4 == udmabuf5 : OK
```

## Uninstall

```
shell# rake uninstall
dtbocfg.rb --remove uio_irq_sample
[  951.566944] u-dma-buf amba:pump-udmabuf5: driver removed.
[  951.573809] u-dma-buf amba:pump-udmabuf4: driver removed.
[  951.582218] fclkcfg amba:fclk0: driver unloaded
```


## Build Bitstream file

### Requirement

* Vivado 2016.1 - 2017.2.1

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
shell$ tools/fpga-bit-to-bin.py --flip project/project.run/impl_1/design_1_wrapper.bit pump_axi4.bin
```
