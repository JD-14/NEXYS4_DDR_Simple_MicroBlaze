# NEXYS 4 DDR & MicroBlaze
This repo is a small tutorial on implementing the **MicroBlaze** processor on a hardware design using **Vivado**. The hardware used to run the design is the **NEXYS 4 DDR** FPGA. The design is built using the IP (Intellectual Property) integrator in **Vivado 2018**. The first stage in this tutorial is to create a block design that incorporates the MicroBlaze. Then, a Hardware description file is generated and exported to create a simple software application that can be programmed/run on the FPGA (target board). In the second stage, **Xilinx SDK** (Software Development Kit) **2018** is used to create a simple **"Hello World" application**.  Finally, a PuTTY terminal is used to interface with the FPGA and view the results.

## Content:
  1. [Prerequisites]
  2. [initial setup]


## Prerequisites
  1. Xilinx Software:
      
      - [Vivado Design Suite - HLx Editions - 2018.2  Full Product Installation](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive.html)
        - Vivado 2018.2 & Xilinx SDK 2018.2 
  2. FPGA:
      - [Digilent Nexys 4 DDR FPGA Board](https://digilent.com/reference/programmable-logic/nexys-4-ddr/start)
      - Micro USB Cable
  3. Terminal:
      - [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)


## Initial Setup
**IMPORTANT: Do not skip this step**

  - Xilinx Software Compatibility Check:
    > Please verify that the Vivado and SDK software that it's installed is the same version. In this case, both should display the 2018.2 version. If the versions don't match, the Vivado software won't be able to launch the SDK software to create the application. Moreover, if you have ISE Design Suite installed, this software might create a path conflict because ISE  Design Suite uses a different version of the SDK software. If you encounter any path issues or errors when you try to launch SDK from Vivado, do the following:
    >> 1. completely uninstall the Vivado Design Suite
    >> 2. reinstall the Vivado Design Suite in a separate folder from other Xilinx tools
 
 - FPGA Board Files:
   > 
  
