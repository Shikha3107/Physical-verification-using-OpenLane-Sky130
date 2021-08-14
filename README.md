
# Physical-verification-using-OpenLane-Sky130

## Contents
  1. Day 1 - Introduction to SkyWater130 PDK and basic DRC/LVS Design Flow
  2. Day 2 - Introduction to DRC and LVS
  3. Day 3 - Introdtuction to DRC Rules
  4. Day 4 - Understanding PNR and Physical Verification
  5. Day 5 - Running LVS

## DAY 1 - Introduction to SkyWater130 PDK and basic DRC/LVS Design flow

SkyWater130 is open source PDK where design rules, layers definition, device definition rules, simulation models and device models are made open for public. In SkyWater130, 130 stands for 130nm or feature size of transistor. SkyWater130 is divided into three parts of public repository mainly Documentation, PDK libraries and files and Community.

The tools that can work with SkyWater PDK are Magic, Klayout, netgen, xschem, openlane, ngspice

Lets understand different components of Skywater130 PDK
* ### **Layers**
  * #### Back End layers
      ##### MiM Cap layers
  * #### Front End Layers
  * #### High Voltage layer
* ### **Devices**
* ### **Libraries**
  * #### Digital Standard Cells
  * #### IO Cells
  * #### Primitive devices and models

### OpenSource Tools and Flows

Learnt about various open source tools like magic, netgen, xschem, ngspice

  #### magic
  magic is used for creation of layout, checking DRC errors
 
  ![Day1_Lab_check_tool_installation_magic](https://user-images.githubusercontent.com/24937940/129443616-bff833e7-b2a3-496b-af50-a2c1430a0267.PNG)

  #### netgen
  netgen is used for running LVS and extraction
  
  ![Day1_lab_check_tool_installation_netgen](https://user-images.githubusercontent.com/24937940/129443330-d7235990-408a-4635-a322-a13d213d3414.PNG)

  #### xschem
  xschem is used for creation of schematics
  
  ![Day1_Lab_check_tool_installation_xschem](https://user-images.githubusercontent.com/24937940/129443365-5cffb405-688c-4d35-9bc6-081db8585b07.PNG)

  #### ngspice
  ngspice is used for running simulation
       
  ![Day1_Lab_check_tool_installation_ngspice](https://user-images.githubusercontent.com/24937940/129443506-cd3088ed-298b-4871-be74-2215c7f19424.PNG)

  #### Steps to be followed for creating setup
  
  ![creating_setup_design](https://user-images.githubusercontent.com/24937940/129444596-bc18c9b3-7537-487b-814d-2f6fe3c57e0d.PNG)

 ### Creating Schematic
 
  Following are the steps to be followed for creating schematic using xschem,
  1. Open xschem
  2. From File choose -> New Schematic
  3. Insert pfet and nfet devices from skywaterPDK and pins like input, output, vdd and vss from device libraries
  
  ![image](https://user-images.githubusercontent.com/24937940/129459345-42caab12-a089-42d1-b60d-8e4b5a86dcef.png)
  
  4. Connect device and pins through wires using "w" key
  
  ![image](https://user-images.githubusercontent.com/24937940/129459504-6a55c6e6-d9e0-443b-ae85-204ce0e42bb1.png)
  
  5. Select devices and pins and update their properties by "q" key
  
  ![image](https://user-images.githubusercontent.com/24937940/129459561-ab64d713-2e0a-480c-b69e-6a7ece3b529d.png)
  
  6. Save the schematic.
  
  ### Creating testbench for simulation
  
  Following are the steps to be followed for creating symbols for testbench simulation
  1. Make symbols from schematics
  2. Open created schematic in .sym format
  3. A simple inverter symbol will be created
  4. Include voltage source, Gnd, connect through wires
  5. Create two text based components by choosing from code shown
  6. First one will be used to tell testbench that which device models will be included and which techfile and corner will be selected
  7. Second one is to fill transient analysis for simulation
  8. Save this as inverter_tb.spice
  9. Run Simulation
  10. Check the plot
  11. With this we have functionally evaluated our testbench
  12. Before moving to layout we need to have netlist that is not a testbench itself but it is a circuit.
  13. Open inverter.sch and edit, Check the LVS netlist is top level .subckt
  14. Click on simulation this will create inverter.spice
  
  ### Importing Schematic to layout and layout steps
  
  
  
## DAY 2 - Introduction to DRC and LVS


 
