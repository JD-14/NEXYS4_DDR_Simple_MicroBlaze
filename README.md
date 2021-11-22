# NEXYS 4 DDR & MicroBlaze
This repo is a small tutorial on implementing the **MicroBlaze** processor on a hardware design using **Vivado**. The hardware used to run the design is the **NEXYS 4 DDR** FPGA. The design is built using the IP (Intellectual Property) integrator in **Vivado 2018**. The first stage in this tutorial is to create a block design that incorporates the MicroBlaze. Then, a Hardware description file is generated and exported to create a simple software application that can be programmed/run on the FPGA (target board). In the second stage, **Xilinx SDK** (Software Development Kit) **2018** is used to create a simple **"Hello World" application**.  Finally, a PuTTY terminal is used to interface with the FPGA and view the results.

## Content:
  1. Prerequisites
  2. initial setup
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
   
   
   ### 2. Creating a Hardware Design Using The IP Integrator: 
   > After you create a new project, you will first see the Vivado IDE (Integrated Development Environment). As shown in the image below, the far left panel is called the "Flow Navigator."  To create the hardware design, we will use the "IP Integrator" option in the Flow Navigator.The IP Integrator contains multiple predefined hardware sources that are used to create new hardware designs. Under this option, click the "Create New Design."
   >> ![img](/images/img6.png)
   
   > In the "Create Block Design" window, you can rename the design or leave it as default. Then, click the "OK" button to create the block design workspace.  
   >> ![img](/images/img7.png)
   
   > In the  "Design" window, click on either of the blue-plus (add IP) symbols to add an IP block. The plus symbols are circled in the image below. Once you click it, a catalog of pre-built IP blocks from Xilinx IP repository will appear. Type "microblaze" on the search bar and double-click the first option. Now, the Xilinx Microblaze IP block should be visible on your design.
   >> ![img](/images/img8.png)
   >> ![img](/images/img9.png)
   
   ### 3. MicroBlaze IP Properties: 
   > After adding the Xilinx Microblaze IP block to the design, we need to adjust some settings to continue.
   >> ![img10](https://user-images.githubusercontent.com/37168081/142785426-01839ed8-5806-4f76-9997-3086dd1e8e50.png)
   
   > Click the "Run Block Automation" option that is circled in the image below.
   >> ![img11](https://user-images.githubusercontent.com/37168081/142785320-90e6ee17-9ac5-4250-af96-a0f884de8f90.png)
   
   > In the "Run Block Automation" window, adjust the settings (under options) to match the ones in the image below. After changing the settings, click the "OK" button.
   >> ![image](https://user-images.githubusercontent.com/37168081/142785277-6de209b1-7e3a-47ca-b81f-f31f2e5d91ce.png)
   
   > After running the block automation, you should see the same blocks shown in the image below. **DO NOT** click the "Run Connection Automation" yet.
   >> ![image](https://user-images.githubusercontent.com/37168081/142785812-aa8639dc-85cc-4f4e-8caf-ea4a07260828.png)
   
   
   ### 4. Clock Wizard IP Block Customization:
   > On the design, double click the "Clocking Wizard" (clk_wiz_1) IP block. Then, a "Re-customize IP" window should open.
   >> ![image](https://user-images.githubusercontent.com/37168081/142786138-505f795f-8295-4743-b37d-a772e1229a1d.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142786236-1e61c4e5-889c-4ad5-a88f-174c569359bd.png)
   
   > In the "Re-customize IP" window, under the "Board" tab, change the **CLK_IN1** from **custom** to **sys clock**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142786546-d4a3e762-16d7-4d33-9c37-39c683bf6b74.png)
   
   > Under the "Output Clocks" tab, select the clk_out2 and change the output frequency from 100 to 200 Mhz. Then, scroll down to the "Reset Type" and change it to Active Low. If you look at the block on the left panel, you may notice that there is a "resetn" and "clk_out2" pin added to the block. Now, click the "ok" button to apply the changes.
   >> ![image](https://user-images.githubusercontent.com/37168081/142787430-90369536-4eaa-4cd5-92ba-23f28615c70d.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142787512-3b1a59f2-6b20-42a1-b9ec-f8576faca88b.png)
   
   
   ### 5. UART IP Block:
   > Click the Add IP (Blue plus symbol) option in the design window and type "UART" in the search bar. Double-click the "AXI Uartlite" option to add the block to your design. **The UART controller is used to communicate between the terminal window on the Host-PC and the Nexys 4 DDR hardware.**
   >> ![image](https://user-images.githubusercontent.com/37168081/142788066-43d2af14-9708-4b82-b699-6e255c9357dd.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142788286-50859c34-7523-4856-abff-762fac44fac7.png)
   
   
   ### 6. Running Connection Automation:
   > Click the "Run Connection Automation." In the "Run Connection Automation" window, select only the "ext_reset_in" and make sure the "Board Part Interface" is set to reset. Next, click the "Ok" button to run the connection for the selected option.  
   >> ![image](https://user-images.githubusercontent.com/37168081/142788753-bb28bdbe-9355-47c0-aeaf-0b62ae2fef3a.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142789167-3d28122e-4522-46c2-b06e-7b93c308e1ed.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142789366-077bb6be-486b-4551-b3da-a12f12a5b5b6.png)
   
   > Now, rerun the connection automation but this time select all available connections and click OK. After running the automation, all the IP blocks in the design will be connected. Moreover, the automation added an IP block called "AXI INterconnect" (microblaze_0_axi_periph) that is required for the design. Furthermore, two signal pins, "reset" and "sys_clock" were added to the design as well. 
   >> ![image](https://user-images.githubusercontent.com/37168081/142789660-bce6bd6c-da10-4898-bd20-4d5f24a9103a.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142790338-04c0fd9b-8198-4930-8c48-a52916ad3990.png)
   
   
   ### 7. Adding and Customizing Memory Interface Generator IP Block:
   > Click the Add IP option in the design window and type "MIG" in the search bar. Double-click the "Memory Interface Generator" option. Then, click the "Run Block Automation" option.
   >> ![image](https://user-images.githubusercontent.com/37168081/142791232-933b11ee-bba8-4804-83e1-77f99ba60a43.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142791603-9bf3d107-aeea-4b8e-9185-e9835f6a2d15.png)
   
   > In the "Run Block Automation" window, the **Board Part Interface** should be displayed as **ddr2_sdram**. Click the "OK" button to run the block automation.
   >> ![image](https://user-images.githubusercontent.com/37168081/142792004-951c82cc-0d5d-47c2-8335-48141df76868.png)
   
   > When the MIG block automation is run, you will see this specific error message [BD 41-1273]. You can ignore this for now. It will not affect your design in any way. The MIG block will be configured as per the board support files that have been downloaded for Nexys 4 DDR. Click OK to dismiss this message. 
   >> ![image](https://user-images.githubusercontent.com/37168081/142792203-4d64889a-2727-414f-82df-bf123345ab77.png)
   
   
   ### 8. Running Connection Automation For The Second Time:
   > Click the "Run Connection Automation" option. 
   >> ![image](https://user-images.githubusercontent.com/37168081/142792692-2792171b-248b-4215-8b43-a8b4be7c00d7.png)
   
   > In the "Run Connection Automation" window, select only the "mig_7series_0" section. Moreover, **unselect** the **sys_clk_i** option. Furthermore, **DO NOT** select the "microblaze_0" section. Then, click OK to run the connection automation. As you may notice, new signals connections were added to the design.
   >> ![image](https://user-images.githubusercontent.com/37168081/142793677-944de16f-4f36-4de1-88a3-d45e97e72313.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142793971-9f979c83-e749-47b2-b7f0-badc3b21776f.png)

   
   
   ### 9. Manual Connection:
   > Manually connect the **clk_out2** output port signal on the **clk_wiz_1** to the **sys_clk_i** input port on **the mig_7series_0** block. Place your cursor pointer on the **clk_out2** output and you should see the cursor change into a graphical representation of a pen. Drag and drop the connection to the **sys_clk_i** input port. Then, the manual connection will be highlighted.
   >> ![image](https://user-images.githubusercontent.com/37168081/142794605-d835931b-9118-4667-b559-1a9be9cf31fd.png)
   
   
   > Now click the blue-circle button, this option is called **Regenerate Layout**. This option will re-arrange the IP block in the design.
   >> ![image](https://user-images.githubusercontent.com/37168081/142795074-0a14197a-2fd3-4401-89fb-7df2a83a3af8.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142795131-59c8a19c-993a-45c6-ba63-de346243f6a9.png)
   
   
   ### 10. Make DDR2 Signal External
   > On the **Memory Interface Generator** (mig_7series_0) block, place your cursor on this symbol || next to the DDR2+ port name. Your cursor will change to look like a pencil. Right click here and in the options list select **Make External**. Then, regenerate the layout again.
   >> ![image](https://user-images.githubusercontent.com/37168081/142795750-6246bc71-fc46-4b48-8ad0-5c0614c1106c.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142795839-8857a42c-9059-4aab-a2e8-8f0c5df145f4.png)
   
   
   ### 11. Validate Design:
   > In the design window, click the check mark. This option is called **Validate Design** and is used to check for design and connection errors. Note that this validation will only display error messages for **critical** errors. If everything is fine, you should see the message shown in the image below. Click OK to close the message window.
   >> ![image](https://user-images.githubusercontent.com/37168081/142796498-e5ebc4e5-9371-47c5-98f4-4346794ef54b.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142796739-59f1a5e3-8f12-4d45-9b54-43420ee4534c.png)
   
   
   ### 12. Creating HDL System Wrapper
   > On the left section of the "Block Design" window, there is a tab named **sources**. Under **design sources**, right click on **design_1** (the name of your design file might be different) and select **Create HDL Wrapper**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142797096-a42d4117-8b47-4c4b-81ba-54fa3758e64e.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142797512-a533a124-e035-41dd-8b5e-12a15e9cd632.png)
   
   > In the "Create HDL Wrapper" Window, select the "Let Vivado manage wrapper and auto-update" option. Then, click OK.
   >> ![image](https://user-images.githubusercontent.com/37168081/142797818-b93a4cc4-c2cd-4554-b7d4-073877c79ffe.png)
   
   > A system wrapper file will be generated and a message will be displayed in the tcl console informing us that the wrapper.v file has been generated. Note that the path of where the file is saved is arbitrary. However, the last line "update_compile_order -fileset sources_1" should be the same.
   >> ![image](https://user-images.githubusercontent.com/37168081/142797956-094d7ebc-f717-4ced-bce2-5c4055a59163.png)
   
   
   ### 13. Generating Bit File:
   > Before you continue make sure to save (Ctrl + s) your design. In the **Flow Navigator** panel, under **Program and Debug** click the **Generate Bitstream** option. In the **No Implementation Results Available** window, click **Yes**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142798626-1c323e97-9e60-43d3-82fd-223d1f479f86.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142798918-abbef6bc-b217-411a-93f1-700f5f8f1c26.png)
   
   > In the "Launch Runs" window, just click OK.
   >> ![image](https://user-images.githubusercontent.com/37168081/142799258-8fdaeb26-aecb-4c29-928d-0a8a1d8cfa26.png)
   
   > Now, the bit file generation will begin. The tool will run Synthesis and Implementation. After both synthesis and implementation have been successfully completed, the actual bit file will be created. You will find a status bar of Synthesis and Implementation running on the top right corner of the project window. Note this process takes at least 20 min
   >> ![image](https://user-images.githubusercontent.com/37168081/142799455-0ed770bd-6a9d-4d9c-a0a2-2d2727dfe98a.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142799595-894408b9-c040-4bb4-a024-9998dd8662ca.png)
   
   > Once the **Bitstream** is generated, a "Bitstream Generation Completed" window will appear. If you don't get this window, it means that there was an error. Next, click "Cancel" to close the window.
   >> ![image](https://user-images.githubusercontent.com/37168081/142803157-af5813f7-789a-4d19-b3d4-de36a89f27a0.png)
   
   
   
   ### 14. Exporting Hardware Design to SDK:
   > On the top left section of the window, click the **File** option and select **Export Hardware**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142803716-a71eff54-69bb-4a5e-9be2-d4e338e29281.png)
   
   > IN the "Export Hardawre" Window, select the "Include bitstream" option and click OK. This will export the hardware design with system wrapper for the Software Development Tool (Vivado SDK).
   >> ![image](https://user-images.githubusercontent.com/37168081/142804141-17ba8549-06df-408e-b377-c5e1365a047a.png)
   
   > A new file directory will be created under project_1.SDK similar to the Vivado hardware design project name. Two other files, .sysdef and .hdf are also created. This step essentially creates a new SDK Workspace.
If you browse to the location on the drive where the Vivado project has been created, you will see that new folders have been created under SDK. See TCL Console message in the screen capture below. 
   >> ![image](https://user-images.githubusercontent.com/37168081/142805002-e110208a-4083-4de4-a92e-856644ed7973.png)



## SDK 2018.2
   ### 1. Launching SDK:
   > Now that the design has been exported to Software Development Kit (SDK) tool, the next step will be to launch the SDK tool. On the top left section of the window, click the **File** option and select **Launch SDK**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142805464-29842eba-20f5-4658-b256-f81d68dcfd0f.png)
   
   > In the "Launch SDK" window, click OK. The SDK file created local to the Vivado design project location will be launched. At this stage, we have finished with the Vivado tool and will continue from the SDK tool.
   >> ![image](https://user-images.githubusercontent.com/37168081/142805607-2c38536e-0039-4ffb-bb62-853699c3a2b2.png)
   
   
   ### 2. Inside SDK for Vivado
   >  A new window for SDK will open. The HardWare (HW) design specification and included IP blocks are displayed in the system.hdf file. SDK tool is independent of Vivado, i.e. from this point, you can create your SoftWare (SW) project in C/C++ on top of the exported HW design. If necessary, you can also launch SDK directly from the SDK folder created in the main Vivado Project directory.
   >> ![image](https://user-images.githubusercontent.com/37168081/142806678-1877e58b-331d-4535-862e-a20e1ab9040d.png)   
   >> **IMPORTANT NOTE:** if you need to go back to Vivado and make changes to the HW design, then it is recommended to close the SDK window and make the required HW design edits in Vivado. After this you must follow the sequence of creating a new HDL wrapper, save design and bit file generation. This new bit file and system wrapper must then be exported to SDK.
   
   
   > On the left corner of the main SDK window, you will find the "Project Explorer" panel. Notice that there is a main project folder under the name **design_1_wrapper_hw_platform_0**. **design_1** is the name of your block design created in Vivado. This hardware platform has all the HW design definitions, IP interfaces that have been added, external output signal information and local memory address information.
   >> ![image](https://user-images.githubusercontent.com/37168081/142807300-a8d51f95-6ca6-4b46-8b1f-271fc2b7c649.png) 
   
   >> **IMPORTANT NOTE:** if you close the SDK tool, make edits to your existing hardware design, and exported your design to SDK then after launching the SDK tool, you will find a new hardware platform called: **design_1_wrapper_hw_platform_1** in addition to the old HW design i.e. **design_1_wrapper_hw_platform_0**.
   
   
   ### 3. Creating New Application Project in SDK:
   > On the left corner of the main SDK window, click on **File**, then **New**, and select the **Application Project**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142807938-99bb868a-b271-4707-bea2-6d4343a927d4.png)
   
   > In the "New Project" window, type an arbitrary name for the project. In this case, the project name is "microblaze_HelloWorld." Then, select "C" as the language and click Next.
   >> ![image](https://user-images.githubusercontent.com/37168081/142808753-4beceb0e-d2e5-4b64-a3b5-a6fb0be5db78.png)
   
   > Now, select the "Hello World" option from the available templates. Then, click Finish.
   >> ![image](https://user-images.githubusercontent.com/37168081/142809085-ad232d1b-f50d-4575-b7f4-9640836bb3c6.png)
   
   
   > After creating the **Hello World** application, you will see two new folders in the Project Explorer panel:
   >  - **microblaze_HelloWorld** which contains all the binaries, .C and .H (Header) files
   >  - **microblaze_HelloWorld_bsp** which is the board support folder
   >> ![image](https://user-images.githubusercontent.com/37168081/142809499-3d30980c-b4c5-4107-8424-6bce249bcff4.png)
   
   
   
   ### 4. Verify Linker Script File for Memory Region Mapping:
   > **microblaze_HelloWorld** is our main working source folder. This also contains an important file shown here which is the lscript.ld. This is a Xilinx auto generated linker script file. Double-click on this file to open. In the linker script, take a look at the Section to Memory Region Mapping box. If you did the **Make DDR2 External** step then the target memory region must read **mig_7series_0**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142810301-a973f943-ef9e-46c1-8269-60ca9d755fc3.png)
   >> **IMPORTANT NOTE:** scroll down to check if this applies to all rows. If for any region it does not say mig_7series_0, then click on the row under the Memory Region column and select mig_7series_0.
   
   
   > In the **Project Explorer**, double click and open **helloworld.c** under the **src** (source) folder. This is the main .C file which will print hello world in the console when executed.
   >> ![image](https://user-images.githubusercontent.com/37168081/142810907-a0c4e2b7-ce37-419d-9e78-b3368d7867d1.png)
   
   
   ### 5. Programming FPGA with Bit File:
   > Now, make sure that the **Nexys 4 DDR** is **turned on** and connected to the host PC with the provided micro USB cable. Next, in the quick selection tool bar, you will find a symbol with a **red arrow and three green square boxes**. Click on this symbol to open the Program FPGA window.
   >> ![image](https://user-images.githubusercontent.com/37168081/142811898-85d4184b-699f-40d6-9ac7-3e912c6dd26e.png)
   
   > In the "Program FPGA" window, make sure that the Hardware Platform selected is design_1_wrapper_hw_platform_0. Moreover, in the **software configuration** box, under **ELF File to Initialize in Block RAM**  column, the row option must read **bootloop**. If not, click on the row and select bootloop. Then, click on **Program**.
   >> ![image](https://user-images.githubusercontent.com/37168081/142814760-ccce0266-ae2e-4652-b659-9c51a981b9ee.png)



## PuTTY Terminal 
   ### 1. Terminal Configuration:
   > After the FPGA is programmed, the only thing left is to open a terminal to see the results. Open the Putty application. In the "Putty Configuration" window, under **Connection type** select the **Serial* option. Then, in the **Serial Line** box, type the communication port (COMX) that your FPGA is connected to. If you are not sure which COM port you are using, then on windows, open **Device Manager** and select the **Ports (COM &LPT)** option to view the available ports. Usually, **COM4** is the port that is most commonly used. In my case, The **Serial Line* is **COM4**. Next, set the **Speed** to 9600. Next, Click **Open** to view the terminal/console.
   >> ![image](https://user-images.githubusercontent.com/37168081/142817439-c8312e73-d535-44b5-9aa8-a7ed7949726b.png)
   >> ![image](https://user-images.githubusercontent.com/37168081/142817375-e1f65424-8f94-493e-8b17-265cfc9aa4b0.png)
   >> **IMPORTANT NOTE:** if you are unsure which port the FPGA is using, try all the available ports until a terminal is successfully opened.
   
   
   ### 2. Display Hello World Output on Terminal:
   > After you open the terminal, you should notice that the terminal is empty/blank.
   >> ![image](https://user-images.githubusercontent.com/37168081/142818708-16cc5c64-aa68-4840-b677-0af6c216d94d.png)
   
   > Now, on the SDK tool window, go to the **Project Explorer** window. Right-click the "microblaze_HelloWorld" folder, select **Run As**, and click the "Launch On Hardware (System Debugger)" option. Then, The script will be executed on the FPGA.
   >> ![image](https://user-images.githubusercontent.com/37168081/142818983-f70d7c17-b248-4e8d-9d0b-dce993fffc1e.png)
   
   > Switch back to the terminal window, as you may notice, **Hello World** is displayed on the terminal. Finally, this concludes the tutorial.
   >> ![image](https://user-images.githubusercontent.com/37168081/142819749-f9310800-8fd9-49a6-a280-12fb6c404312.png)



##Reference
1. [Getting Started with Microblaze](https://digilent.com/reference/learn/programmable-logic/tutorials/nexys-4-ddr-getting-started-with-microblaze/start)
