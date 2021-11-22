# NEXYS 4 DDR & MicroBlaze
This repo is a small tutorial on implementing the **MicroBlaze** processor on a hardware design using **Vivado**. The hardware used to run the design is the **NEXYS 4 DDR** FPGA. The design is built using the IP (Intellectual Property) integrator in **Vivado 2018**. The first stage in this tutorial is to create a block design that incorporates the MicroBlaze. Then, a Hardware description file is generated and exported to create a simple software application that can be programmed/run on the FPGA (target board). In the second stage, **Xilinx SDK** (Software Development Kit) **2018** is used to create a simple **"Hello World" application**.  Finally, a PuTTY terminal is used to interface with the FPGA and view the results.

## Content:
  1. [Prerequisites]
  2. [initial setup]
  3. Vivado 2018.2 (Hardware Design)
  4. SDK 2018.2 (Create application using C)
  5. PuTTY Terminal (Results)


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
   > By default Vivado comes with a limited amount of board files. Therefore, the Nexys 4 DDR FPGA board files have to be added manually to the board library of Vivado. 
   >> 1. [Download the board files](/vivado-boards-master.zip)
   >> 2. Extract the folder
   >> 3. Navigate to the following folder: vivado-boards-master\new\board_files
   >> 4. Select and copy all the board files
   >> 5. Locate and open the folder where you installed the Vivado Design Suite
   >> 6. Navigate to the following folder: xilinx\SDK\2018.2\data\boards\board_files
   >> 7. Paste the board files in the Vivado board folder


## Vivado 2018.2
   ### 1. Create new project:
   > Open Vivado and you should see the same window as the image below. Under "Quick Start" click on "Create Project". A new window with the title "Create a New Vivado Project" will appear. Click the "Next" button.
   >> ![img](/images/img1.png)
   
   > In the "Project Name" window, you can change the file name and location. Or you can leave it as default. Click the "Next" button.
   >> ![img](/images/img2.png)
   
   > In the "Project Type" window, make sure that the "RTL Project" option is selected. Also, select the "Do not specify sources at this time" setting. Click the "Next" button.
   >> ![img](/images/img3.png)
   
   > In the "Default Part" window, select the board section. This section is circled in the image below. **DO NOT** add the part from the Part section. If you do, it will create a problem later in the tutorial. Under the board section, type the model of the FPGA in the search bar. As shown in the image below, the "Nexys 4 DDR" board should appear as the only option. Select the board and click the "Next" button.
   >> ![img](/images/img4.png)
   
   > On the "New Project Summary" window, verify that the summary is the same as the image below. The only exception is the name of the project, which is arbitrary. However, the board information must be the same. If everything is correct, then click the "Finish" button to create the project
   >> ![img](/images/img5.png)
   
   
## Creating a Hardware Design Using The IP Integrator   
   > After you create a new project, you will first see the Vivado IDE (Integrated Development Environment). As shown in the image below, the far left panel is called the "Flow Navigator."  To create the hardware design, we will use the "IP Integrator" option in the Flow Navigator.The IP Integrator contains multiple predefined hardware sources that are used to create new hardware designs. Under this option, click the "Create New Design."
   >> ![img](/images/img6.png)
   
   > In the "Create Block Design" window, you can rename the design or leave it as default. Then, click the "OK" button to create the block design workspace.  
   >> ![img](/images/img7.png)
   
   > In the  "Design" window, click on either of the blue-plus (add IP) symbols to add an IP block. The plus symbols are circled in the image below. Once you click it, a catalog of pre-built IP blocks from Xilinx IP repository will appear. Type "microblaze" on the search bar and double-click the first option. Now, the Xilinx Microblaze IP block should be visible on your design.
   > ![img](/images/img8.png)
   > ![img](/images/img9.png)
