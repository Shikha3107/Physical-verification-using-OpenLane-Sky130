
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
  2. Open New Schematic, Insert inverter.sym here
  3. A simple inverter symbol will be created
  
  ![image](https://user-images.githubusercontent.com/24937940/129459737-2638d8c5-7d2c-4596-a14f-30bf2ff33465.png)

  4. Include voltage source, Gnd, connect through wires
  
  ![image](https://user-images.githubusercontent.com/24937940/129459834-c0ff1cb6-0072-45a6-84b4-5acbb57caaa6.png)
  
  5. Fill voltage source configuration
  
  ![image](https://user-images.githubusercontent.com/24937940/129459864-50427c13-ade8-45f6-b21e-90bfef26b8a2.png)
  
  6. Create two text based components by choosing from code shown
  
  ![image](https://user-images.githubusercontent.com/24937940/129459901-93cbad5b-54d7-445a-bac9-f26496c51285.png)

  7. First one will be used to tell testbench that which device models will be included and which techfile and corner will be selected
  
  ![image](https://user-images.githubusercontent.com/24937940/129459970-0bb75a72-21b9-42e7-94fb-810d49e860ae.png)

  8. Second one is to fill transient analysis for simulation

  ![image](https://user-images.githubusercontent.com/24937940/129459998-64116ab9-ac5e-4903-bb8a-60f0c929babd.png)

  9. Save this as inverter_tb.spice
  
  ![image](https://user-images.githubusercontent.com/24937940/129460013-547dca0e-2bdd-4390-8c76-7b955c3456de.png)

  10. Run Simulation
  
  ![image](https://user-images.githubusercontent.com/24937940/129460115-23294a40-657b-4464-8da0-a1f8fd9a2039.png)

  11. Check the plot
  
  ![image](https://user-images.githubusercontent.com/24937940/129460125-27e5eb98-334d-4061-83cd-cb5148ef721e.png)

  12. With this we have functionally evaluated our testbench
  13. Before moving to layout we need to have netlist that is not a testbench itself but a circuit.
  14. Open inverter.sch and edit, Check the LVS netlist top level is a .subckt
  15. Click on simulation this will create inverter.spice
  
  ### Importing Schematic to layout and layout steps
  
  Following are the steps to be followed for importing schematic to layout and completing inverter layout
  1. Go to magic directory, cd ../mag
  2. Run, magic -d XR
  3. Go to File menu and Click on Import SPICE
  
  ![image](https://user-images.githubusercontent.com/24937940/129460324-fb8d2f60-2280-4d3b-94f3-bdd6afda9bf1.png)
  
  Devices present in circuit will be dropped on layout window.
  
  ![image](https://user-images.githubusercontent.com/24937940/129460827-babed2df-f807-4e58-9c2e-08ea8026bd87.png)

  4. Apply some of the configurations for PFET and NFET devices.
  
  ![image](https://user-images.githubusercontent.com/24937940/129460880-7ced7a83-8aa8-4715-b8ec-bdef46c00c3a.png)
  ![image](https://user-images.githubusercontent.com/24937940/129460912-bd739ce5-9f57-48e8-aa0f-697f8a4913e4.png)

  5. Start connecting the devices and pins using metal1 layer.
  
  ![image](https://user-images.githubusercontent.com/24937940/129480464-f4861d96-5ba5-45cc-a069-897175f4b425.png)
  
  6. Save the layout.
  
  ### DRC/LVS and Post Layout Simulation
  
  Following are the steps for running DRC/LVS and Post layout Simulation for inverter design
  1. Run, extract do local and extract all for running extraction in magic own format
  2. For obtaining in spice format, run ext2spice lvs and then ext2spice, ext2spice will create output spice netlist in ngspice format preferred for simulation.
  
  ![image](https://user-images.githubusercontent.com/24937940/129478997-9fca832c-7c57-49dd-8f0e-2d5f2fdcf989.png)
  
  3. For removing any unparameterized cell, run following script,

  ![image](https://user-images.githubusercontent.com/24937940/129479142-bea720f3-1339-459d-aebb-2ae144cce53e.png)
  
  4. For running LVS, Go to netgen dir, cd ../netgen
  5. Run on terminal, netgen -batch lvs "../mag/inverter.spice inverter" "../xschem/inverter.spice inverter"
     Circuit should matches and give LVS match.
  6. If LVS matches properly then continue with extraction
  7. Run, extract do all, extract all, ext2spice lvs, ext2spice cthresh 0, ext2spice one by one on terminal
  8. Look into inverter.spice for parasitic capacitances extracted.
  9. To run simulation, copy inverter_tb.spice from xschem directory into mag directory, align .subckt according to layout .subckt and include layout spice by .include inverter.spice
  10. copy .spiceinit from xschem directory to run simulation
  11. Run, ngspice inverter_tb.spice
  
  ![image](https://user-images.githubusercontent.com/24937940/129481629-741bbad0-cc43-45d3-9bd9-77327a0a2e1d.png)


## DAY 2 - Introduction to DRC and LVS

Understanding GDS, extraction, DRC and LVS

### DRC
The main objective of DRC is to maintain if foundary rules for masking are meeting in the concerned layout.

### Layout vs Schematic (LVS)
The main objective of LVS run is to make sure if Layout matches the Schematic in electrical connectivity and devices.

### Extraction

![image](https://user-images.githubusercontent.com/24937940/129482115-c64a3dd4-e0ff-4f42-af5a-a15261d245cf.png)

### Reading GDS

Following are the steps performed,
1. Know how many styles cif supports, by running magic -d XR and typing below commands,

2. Run commands for gds read

![image](https://user-images.githubusercontent.com/24937940/129482518-80d4e7b9-f489-4409-a6ce-7b3409543982.png)

3. Then load cell from gds, by selecting Options-> Cell manager -> Choose cell -> Load

![image](https://user-images.githubusercontent.com/24937940/129482846-e8b5ac9b-bb4c-4226-8c38-e82e3c66e33d.png)

4. To prevent duplicates overwriting when trying to read same cell from different skywater130 say skywater130(vendor), run, gds noduplicates true

### Understanding Ports

1. Select any port and run, port index

![image](https://user-images.githubusercontent.com/24937940/129482997-4307e5cf-bd4c-4da9-a094-a8e964ce5ff8.png)

2. To know about name, class etc. of ports

![image](https://user-images.githubusercontent.com/24937940/129483070-8c19c51c-e4b4-43fa-a57b-a0cf0e0103df.png)

### Abstract Views

Abstract views are in form of LEF/DEF where layer information is present
1. For reading lef, lef read "name of lef file"

![image](https://user-images.githubusercontent.com/24937940/129483647-33b0a035-9b98-488a-b3fa-bea08991b79e.png)

2. Load cell,

![image](https://user-images.githubusercontent.com/24937940/129483698-7f1fabc7-563a-4a49-88c4-aef5e9e68ed5.png)

3. Viewing abstract View of cell by loading the cell by getcell

![image](https://user-images.githubusercontent.com/24937940/129484089-6d5c41ab-794e-49bb-becd-cf776f4e6849.png)

4.Read abstract view in gds format, not all layers are present

![image](https://user-images.githubusercontent.com/24937940/129484209-1b81a7f6-eb55-469b-a514-a630b8ea0017.png)

### Basic Extraction

1. Load cell

![image](https://user-images.githubusercontent.com/24937940/129485489-bf72c384-2f69-4270-bbd7-ad90459dccc4.png)

2. Run on terminal, extract all, ext2spice lvs, ext2spice
3. Now lets continue with capacitance extraction

![image](https://user-images.githubusercontent.com/24937940/129485698-94d31597-1319-40f7-9fad-a476232daabf.png)

4. For extracting resistance, follow commands, it will create .sim and .nodes files in terminal

![image](https://user-images.githubusercontent.com/24937940/129485842-ee0995f3-e22e-48fa-ab00-0d15767fb8b3.png)

5. For having one single netlist, follow following steps,

![image](https://user-images.githubusercontent.com/24937940/129485975-63e52715-f1a0-4cec-85e4-39997833eb9e.png)

### DRC Setup

Follow below steps to run DRC check,
1. 

### LVS setup

For LVS run simple steps are required, netgen -batch lvs "../mag/inverter.spice inverter" "../xschem/inverter.spice inverter"

### XOR Setup


## DAY 3 - Front-End and back-End DRC







 
