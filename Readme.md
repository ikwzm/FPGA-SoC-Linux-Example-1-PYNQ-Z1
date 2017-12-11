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
dtbocfg.rb --install uio_irq_sample --dts uio_irq_sample.dts
/config/device-tree/overlays/uio_irq_sample/dtbo: Warning (unit_add[  280.418362] fpga_manager fpga0: writing pump_axi4.bin to Xilinx Zynq FPGA Manager
ress_vs_reg): Node /fragment@0 has a unit name, but no reg property
/config/device-tree/overlays/uio_irq_sample/dtbo: Warning (interrupts_property): Missing interrupt-parent for /fragment@0/__overlay__/pump-uio@43c10000
[  280.498217] udmabuf amba:fpga-region0:pump-udmabuf4: driver probe start.
[  280.513478] udmabuf udmabuf4: driver installed
[  280.517845] udmabuf udmabuf4: major number   = 245
[  280.524513] udmabuf udmabuf4: minor number   = 0
[  280.529049] udmabuf udmabuf4: phys address   = 0x1f100000
[  280.536134] udmabuf udmabuf4: buffer size    = 1048576
[  280.542137] udmabuf amba:fpga-region0:pump-udmabuf4: driver installed.
[  280.549159] udmabuf amba:fpga-region0:pump-udmabuf5: driver probe start.
[  280.563975] udmabuf udmabuf5: driver installed
[  280.568351] udmabuf udmabuf5: major number   = 245
[  280.574119] udmabuf udmabuf5: minor number   = 1
[  280.578655] udmabuf udmabuf5: phys address   = 0x1f200000
[  280.585722] udmabuf udmabuf5: buffer size    = 1048576
[  280.591714] udmabuf amba:fpga-region0:pump-udmabuf5: driver installed.
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
[  526.495500] udmabuf udmabuf5: driver uninstalled
[  526.500654] udmabuf amba:fpga-region0:pump-udmabuf5: driver unloaded
[  526.508393] udmabuf udmabuf4: driver uninstalled
[  526.513555] udmabuf amba:fpga-region0:pump-udmabuf4: driver unloaded
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
