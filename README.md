Lab 0: Installation of tools 
![Screenshot GTKWave](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/e27255da-469b-481d-b963-9b3462ea48cd)
![Screenshot yosys](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5a164a3a-d08f-44ab-b221-0e0ec611ea25)
![Screenshot iverilog](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/f59c520f-06a6-457e-973e-91b526b1985f)

RTL design using Verilog with SKY130 Technology 

Lab 1: Introduction to verilog design and synthesis

<img width="587" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/e3bf56e3-5d4d-43e6-b91c-72aa9e07390e">


In this lab, we view the timing diagram of the tb_good_mux.vcd using GTKWave. From the timing diagram, it was observed that the output followed the i1 when the sel=1 and i0 when sel=0. This observation was confirmed by the reading the test bench file.

![WhatsApp Image 2024-07-02 at 20 16 53_ed691506](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/ab6e8074-01be-47e4-a701-a620266bc6cf)
![WhatsApp Image 2024-07-02 at 20 25 48_0dbaac85](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/a8995b70-d21b-42ce-a7c5-6a8a72f18035)

We then looked into the yosys setup and learnt how we can verify the systhesis.

![WhatsApp Image 2024-07-02 at 20 31 25_b02816fc](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/58a9e65c-0b19-4566-be47-010f708050a1)
![WhatsApp Image 2024-07-02 at 20 34 55_1e35273f](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/391f5260-414b-4482-bfcc-f5af4b884105)

Day 2- Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

There are three factors on which our design mainly depends, namely, PVT where
P-process (variation due to design)
V-voltage 
T-temperature.

![WhatsApp Image 2024-07-03 at 13 55 39_ea3af7e3](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/2e42fd99-f6ab-4999-9643-6179837d278c)
From left to right, the cells (and2 cells of different flavors) are constructed with wider transistors, highlighting that the area and power consumption increases and the delay decreases for wider transistors.

Hierarchical vs flat synthesis lab

Using yosys to sythesize the mutliple_modules.v 

<img width="430" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/12c3a688-94ee-4185-a1be-4c5fc1116cef">
<img width="150" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/2147b5ac-fa39-4848-9951-fe178f64a93a">



<img width="655" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/49361eb1-2ed2-4306-9095-6ccbbb66a12c">

<img width="616" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/0772b5ab-08df-4fd8-9778-897d55931510">

The hierarchy is observed in the netlist.

<img width="622" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/f2315413-d352-497f-9ea9-0d7c9c19617d">

Heirarchy is flattend out using the flat-end switch.



<img width="574" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/d9aea9c6-0ca3-48ee-9cec-c5049b871578">

(Executing show command after flattening)

Sythesizing at the sub-module leval and the executing the show command.

<img width="348" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/b082429f-05ba-4543-9489-8491befe0e2a">

Note - module level sythsis is preferred when we have multiple instance of the same module or when we are using the divide and conquer approach for massive designs.

Various Flop Coding Styles and Optimization:

Flops are mainly used to prevent glitches that happen due to different time delay of different gate operations, etc. in different combination circuits. Flops present between combinational circuits alllowed to store values to prevent glitches. 

![WhatsApp Image 2024-07-06 at 16 40 33_81e5db7d](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/c6fc507a-7924-43c7-a0bf-530868617434)

To intialize the flop control pins sucha as reset and set are present. Note that reset and the set of the flop can be synchronous or asynchronous.


Example of an asynchronous reset d-flip-flop:


![WhatsApp Image 2024-07-06 at 16 49 31_50f0666c](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/cfe5670f-20d2-498d-ba5b-57c3aa25be55)


Timing diagram of a asynchronous reset d-flip-flop:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/823923f8-f09f-481f-bc12-c008fdd9e3ec">


Timing diagram of a asynchronous set d-flip-flop:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/6267e940-1497-4e41-b029-0d436e26564f">


Timing diagram of a synchronous reset d-flip-flop:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/6cb16c15-a3b2-4cff-a335-41f2691ef291">

Obtaining the netlist and the diagram on synthesizing the dff_asyncres:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/de1a8c3e-2c53-4d8b-871c-a5e785c4f6a2">

Obtaining the netlist and the diagram on synthesizing the dff_async_set:

<img width="929" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/71fd46d4-d890-468b-8384-c50516da8ded">

Obtaining the netlist and the diagram on synthesizing the dff_syncres:

<img width="923" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/63b4594c-b326-4cfd-b3ac-1538a38d29fa">

Special cases:

1)On synthesizing mul2 (left shift in binary representation by multiplying with 2), we learn that it is unnecessary to map ABC as there is nothing to map.

<img width="914" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/4d6d7276-7693-499e-ac92-9868ae319566">

2)Multiplying a 3-bit binary number with 9 such that the 6-bit binary number obtained is just repetion of the three bit number twice. Again, the message "Don't call ABC as there is nothing to map" appears when it is invoked.

<img width="918" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/6bf49642-d702-45fa-83dd-aeb25a8708d8">

Day3 - Combinational and sequential optimizations

1)Combinational optimization

Constant proporgation: When an one or more inputs are constants/fixed values, the expression can be futher simplified.

![WhatsApp Image 2024-07-06 at 18 41 45_d245ebad](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/1c19c239-86b1-455d-9a39-a59aa34e48da)

Boolean logic optimization: Expressions can be simplified using boolean laws, boolean algebra, K-maps. 

![WhatsApp Image 2024-07-06 at 18 47 10_50b445d1](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/637efe73-79ac-4e8f-b5f4-0b63f17dcc4e)

2)Sequential optimization

Sequentional constant proporgation: A flop having a constant Q value irrespective of the clock/reset/set is and example of this type of proporgation.

![WhatsApp Image 2024-07-06 at 18 59 58_4b1d18c1](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/d9be018c-7858-4646-8ed3-fcb4ab3742f6)

State Optimization: By optimizing the unused states, we can reduce the delay caused in the operation.

![WhatsApp Image 2024-07-06 at 19 10 36_d8b48079](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/ac8b210c-6e19-43a2-b769-b0194f42dabc)

Combinational Logic Optimization Lab:

Example 1: Simplifying y=a?b:0 to y=ab

![WhatsApp Image 2024-07-07 at 08 03 12_05059d1f](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/0f20e6b1-1dea-46df-b038-33350e3023bf)

<img width="924" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/4cbea998-ff6f-4e95-9492-6586db842b87">

Example 2: Simplifying y=a?1:b to y=a+b

![WhatsApp Image 2024-07-07 at 08 08 57_204174ab](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/6a1dff20-9492-428d-a305-3f35f7675946)

<img width="931" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/a617e9ff-b767-4153-9820-9d94e7015b38">

Example 3: Simplifying y=a?(c?b:0):0 to y=abc 

![WhatsApp Image 2024-07-07 at 08 20 32_34e1a214](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/d1bd7de9-edc2-4f1c-8dc7-1aebf7e2d370)

<img width="924" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/21165b04-773c-40d3-ad29-c65a0a8aa221">

Example 4: Simplifying y = a?(b?(a & c ):c):(!c) to y=a(xnor)c

![WhatsApp Image 2024-07-07 at 08 56 24_5e1f66af](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/2a77f95b-009b-4394-9b96-a7c105d3149a)

<img width="928" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5704b96d-db04-4bb7-9286-6075c0065016">

Example 5: Synthesizing and flattening multiple_module_opt.v

![WhatsApp Image 2024-07-07 at 09 11 38_bb0b9b67](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/9642fa66-a8c6-4d94-b024-17ef4e37ce36)

Example 6: Synthesizing and flattening multiple_module_opt2.v

<img width="931" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/7a75b3d0-9e0a-4f5e-9837-bd2e098c2531">

Sequential Logic Optimization Lab:

Example 1: D input of the flip-flop is set to high

<img width="671" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/005dc9bc-b4db-441b-b04e-5f8af6497ece">

Viewing the timing diagram:

<img width="929" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/52652433-a256-4b27-99f2-cc94184e051a">

Running the synthesis and viewing the result-

<img width="925" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/904eac91-28af-4772-8fa5-5fc826c768bf">

Example 2: the output Q is always high irrespective of the clk and reset 

<img width="620" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/7985305e-14a9-4882-86af-fc5bc2c1ddb1">

Viewing the timing diagram:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/3c3786fe-4358-4efc-9477-5945de074a88">

Running the synthesis and viewing the result-

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5098e452-fceb-4a76-af95-aa22388e6339">

Example 3: Using two flip-flops 

<img width="674" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/9d9c0fc9-f5df-42c3-948c-58efd4e78d10">

Viewing the timing diagram:

<img width="931" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/1cf9efd6-29c3-4a89-8b96-bbfec2c5011c">

Running the synthesis and viewing the result-

<img width="923" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/0b204b25-8bfc-4eba-bcc9-f146bda22107">

Example 4: Using two flip-flops but no flip-flop is inferred after synthesis

<img width="619" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/1f64982f-9d4a-4d1e-af1f-a32b51ce477f">

Viewing the timing diagram:

<img width="920" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/7ce39038-6f90-4442-a042-b084b6c022fd">

Running the synthesis and viewing the result-

<img width="923" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/46483a5b-b138-4329-b494-f07a142a8a4b">

Example 5: Using two flip-flops

<img width="614" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5196958f-cd39-4c44-8f06-dc7c524ce5bc">

Viewing the timing diagram:

<img width="926" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/b83bcfba-ac1f-4a7d-9a8f-2854d5ee1cf9">

Running the synthesis and viewing the result-

![WhatsApp Image 2024-07-07 at 11 26 27_c7d02952](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/304edc50-32d3-45bd-8570-6e1d21734d7d)

Sequential Optimization of unused outputs:

Example 1: 3 bit counter in which the Q output only depends on the least significant bit of the counter 

<img width="623" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/0b5f0c49-c2b8-44de-9f9d-bf76369f6eb8">

Running the synthesis and viewing the result-

<img width="932" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/b415c0de-2e05-4b0a-afde-c8cdaf86671b">

Example 2: Using the previous 3 bit counter and changing the unused outputs to be used this time 

<img width="620" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5595e4ed-44fb-4e86-86aa-a8d6161f0cc4">

Running the synthesis and viewing the result-

<img width="930" alt="image" src="https://github.com/AvneetK2/SFAL-VSD/assets/173355761/8f541e24-e80b-4849-9777-8aaee2fee34c">

Day 4 - GLS, blocking vs non-blocking and synthesis-simulation mismatch

![WhatsApp Image 2024-07-13 at 08 36 13_2bd4043f](https://github.com/user-attachments/assets/ca8ecd3f-faa1-42d0-ad88-a351bd91c621)

![WhatsApp Image 2024-07-13 at 08 41 16_983d8336](https://github.com/user-attachments/assets/f2b001a8-3b1a-4b6a-9beb-82a6146cc472)

There are namely three reasons that can cause synthesis simulation mismatch-

<img width="352" alt="image" src="https://github.com/user-attachments/assets/f400a60d-73b9-499e-8559-ed86647ac563">

An example for Missing Sensitivity List -

<img width="553" alt="image" src="https://github.com/user-attachments/assets/b48fae41-1484-40a5-9db0-d50841812739">

Examples for Caveats with Blocking Statement - 

<img width="541" alt="image" src="https://github.com/user-attachments/assets/ea617f34-b95a-4bbe-bd04-7191f6ae170d">

<img width="536" alt="image" src="https://github.com/user-attachments/assets/3c7247c7-0902-46fb-8962-df6385f9b0aa">

Labs on GLS, blocking vs non-blocking and synthesis-simulation mismatch

Lab 1 - RTL simulation and GLS simulation of ternary_operator_mux and comaparing the results 

Veiwing the timing diagram of ternary_operator_mux upon RTL simulation

![WhatsApp Image 2024-07-13 at 18 57 10_21b887f7](https://github.com/user-attachments/assets/19a3a967-6d7e-4f08-9154-639fef526a6d)

A mux is inferred during synthesis

<img width="917" alt="image" src="https://github.com/user-attachments/assets/8f50cf74-4a94-40c8-ba7d-4b4fd7a1192b">

Upon GLS simulation using iverilog using the netlist, the behavior model of the cells and the same testbeanch used for RTL simulation, we obtain a similar timing diagram confirming the same mux behavior.

<img width="928" alt="image" src="https://github.com/user-attachments/assets/d8837e54-131d-48ed-91a0-ade44812cb24">



Lab 2 - RTL simulation and GLS simulation of bad_mux and comaparing the results 

Veiwing the timing diagram of bad_mux upon RTL simulation

<img width="901" alt="image" src="https://github.com/user-attachments/assets/0e28aa15-6e71-41ef-951b-b1099ce52b55">

A mux is inferred during synthesis

<img width="921" alt="image" src="https://github.com/user-attachments/assets/d8db4ab5-d773-4996-90f0-71d27ab6e1d9">

Upon GLS simulation using iverilog using the netlist, the behavior model of the cells and the same testbeanch used for RTL simulation, we obtain a different timing diagram.

<img width="933" alt="image" src="https://github.com/user-attachments/assets/fb2d9ea9-ae30-41b0-8644-ed51315964a1">

Thus, we observe different timing diagrams during RTL simulation and during GLS simulation.This is an example of synthesis simulation mismatch which occurs due to missing sensitvity list.



Lab 3 - RTL simulation and GLS simulation of blocking_caveat and comaparing the results 

Veiwing the timing diagram of blocking_caveat upon RTL simulation

<img width="929" alt="image" src="https://github.com/user-attachments/assets/d48d7119-096b-4552-be55-9b33964b057d">

A simple logic diagram is inferred during synthesis

<img width="934" alt="image" src="https://github.com/user-attachments/assets/6d7c8128-f826-42bf-9489-9d70311860ec">

Upon GLS simulation using iverilog using the netlist, the behavior model of the cells and the same testbeanch used for RTL simulation, we obtain a different timing diagram.

<img width="929" alt="image" src="https://github.com/user-attachments/assets/6043db04-1233-49fc-a844-c676c22aa0dc">

Thus, we observe different timing diagrams during RTL simulation and during GLS simulation.This is an example of synthesis simulation mismatch which occurs due to blocking statements.

Advanced Synthesis and STA with DC

Brief recap-

![WhatsApp Image 2024-07-16 at 11 18 25_12bcb359](https://github.com/user-attachments/assets/e82f31ed-6132-4ee1-ab40-b328d90ed017)

![WhatsApp Image 2024-07-16 at 11 26 33_fc29b083](https://github.com/user-attachments/assets/7b00020f-2cbf-44fd-9014-ce7dc89af101)

We learnt that there are differnt flavors of some gate to meet diferent requirements such as delay, power consumption and area occupied.

![WhatsApp Image 2024-07-16 at 11 30 15_dd87767e](https://github.com/user-attachments/assets/b3d0d951-72ea-49e8-96fb-b346ec0a0517)

![WhatsApp Image 2024-07-16 at 11 33 26_111356cc](https://github.com/user-attachments/assets/d3e3e3f4-548d-4749-8a50-41b4ad47087a)

While faster cells help us maximize the speed of operation, the slower cells help us to maintain the hold requirements. 

![WhatsApp Image 2024-07-16 at 11 35 43_b420b335](https://github.com/user-attachments/assets/c0a508fc-c7d2-43b1-a215-333950469f51)

Faster cells are implemented using wider transistors which have greater area and power consumption. On the other hand, slower cells use norrower transistors which have lesser area and power consumption. 

![WhatsApp Image 2024-07-16 at 11 36 32_9bc1f5d1](https://github.com/user-attachments/assets/eef564fd-8024-49ac-b8cf-fb65c2fdd751)

Thus, the contraints guide the synthesizer in choosing different flavors of cells for the optimized implementation of the logical circuit. 

![WhatsApp Image 2024-07-16 at 11 37 57_36240f62](https://github.com/user-attachments/assets/65ad5653-68d0-46b7-acdb-776a3fa0a49e)

![WhatsApp Image 2024-07-16 at 11 40 32_2dcd91cd](https://github.com/user-attachments/assets/9c49730c-a45b-408e-b871-df4ab3291255)

![WhatsApp Image 2024-07-16 at 11 45 11_1bea6770](https://github.com/user-attachments/assets/c0e975f1-307a-46c0-905d-ecfd2f36ca00)

![WhatsApp Image 2024-07-16 at 11 50 21_924a0378](https://github.com/user-attachments/assets/54ad708a-c3fc-4800-917c-eeb0e5324ede)

Intoduction to Design Compiler(DC)-

![WhatsApp Image 2024-07-16 at 12 06 13_ea783840](https://github.com/user-attachments/assets/be544e01-2a7b-42d3-85f2-1875e109b1c5)

![WhatsApp Image 2024-07-16 at 12 10 22_c74b0e5f](https://github.com/user-attachments/assets/317040cd-ddd4-4b54-b785-d3ba798aa6e1)

![WhatsApp Image 2024-07-16 at 12 12 01_112404f0](https://github.com/user-attachments/assets/fe36d7ef-4201-4713-8c70-d016f7131a75)

![WhatsApp Image 2024-07-16 at 12 13 37_48a066d4](https://github.com/user-attachments/assets/11155894-cf27-4ef5-83f1-d2502bf91a88)

We got a glimpe into the steps involved in the coversion of RTL Design to Physical Database/GDS

![WhatsApp Image 2024-07-16 at 12 18 59_f979de5d](https://github.com/user-attachments/assets/2cec995a-218f-4b18-8ee4-90cf6911f0b5)
 
We also learnt about the steps involved in DC Synthesis Flow-

![WhatsApp Image 2024-07-16 at 12 22 46_462343ff](https://github.com/user-attachments/assets/0acea42f-e499-4593-a60e-87eeb3afaf68)

Lab 1 - Invoking dc basic setup 

View the .lib file to understand its PVT (Process, Voltage, Temperature). Note electronic circuit operation is a function of its process, voltage and temperature. From the .lib file we learn that there are different flovors of the same cell to meet our time delay, area and power specifications.

<img width="922" alt="image" src="https://github.com/user-attachments/assets/d85c5d7f-6612-4dc8-8fba-d3c4ade0c059">

Viewing the verilog code for the flip flop with asynchronous reset

<img width="926" alt="image" src="https://github.com/user-attachments/assets/27f450f6-6089-41dd-8b4b-9b0b6f2ef6c4">

As there was no standard cell library provided, the library is written out in the form of GTECH. GTECH  is virtual library in DC's memory to understand the design.

<img width="925" alt="image" src="https://github.com/user-attachments/assets/9ce33dda-7d79-411d-a301-4dec5fe17ab8">

We notice that when the netlist is written in sky130 library, the SEQGEN is no longer used.

<img width="919" alt="image" src="https://github.com/user-attachments/assets/39c75bcf-c7e2-4e05-b9d6-5225c5bb342f">

Lab 2 - Into to dcc gui with design_vision

Note that ddc saves all the information in the tool memory for that particular session. One disadvantage of using ddc is that it is Synopsys proprietry format. 

<img width="920" alt="image" src="https://github.com/user-attachments/assets/71f338a3-b217-4524-ae51-1f4b69e9841b">

Viewing the schematic on Design Vision

<img width="925" alt="image" src="https://github.com/user-attachments/assets/4999d288-b454-484c-b9af-bed139f09ceb">

Lab 3 - dc synopsys dc setup

It is observed that the libraries need to be explicitly configured.

<img width="572" alt="image" src="https://github.com/user-attachments/assets/4705130a-62d1-4293-80ba-f44485b154c1">

Using .synopsys_dc.setup we can set up the $target_library and the $link_library. Thus, we do not have to explicity configure the libraries

<img width="926" alt="image" src="https://github.com/user-attachments/assets/ccb51fa2-c1e9-4cd8-9690-f0966d8b130c">

TCL quick refresher 

<img width="438" alt="image" src="https://github.com/user-attachments/assets/9099029c-a629-4eb4-b24b-e774ccac84a6">

<img width="458" alt="image" src="https://github.com/user-attachments/assets/b01428c0-acfa-45a1-a0b7-64b5e945ae0b">

<img width="529" alt="image" src="https://github.com/user-attachments/assets/a41efc00-9d51-4cc8-ba3c-62e9b4e91404">

<img width="359" alt="image" src="https://github.com/user-attachments/assets/2f3b19d7-39f6-48a3-bdaa-59fd57adb868">

<img width="534" alt="image" src="https://github.com/user-attachments/assets/135c1005-017c-4348-a603-dfaaaf765952">

<img width="528" alt="image" src="https://github.com/user-attachments/assets/0aa8377c-6f3c-4791-a2a9-347bebd83f12">

Lab 4 - TCL Scripting 

Using for loop to print from 0 to 11.

<img width="923" alt="image" src="https://github.com/user-attachments/assets/db7e2a0c-9721-4995-bb21-37ce3fef42d8">

Using while loop to print from 0 to 10.

<img width="921" alt="image" src="https://github.com/user-attachments/assets/9e29c86a-bec3-4bff-847f-004619af5012">

Creating a list and printing out its contents. 

<img width="922" alt="image" src="https://github.com/user-attachments/assets/48709e97-e0c1-4ddf-8e9a-d0222066deb2">

On trying to print the collection, we observe that _sel13 acts as a pointer. Thus, it is acolletion of pointers. 

<img width="923" alt="image" src="https://github.com/user-attachments/assets/1879b4ac-8653-4340-a4bb-53b7a8bc5f7b">

To print the contents of the collection of pointers, we use get_object_name. 

<img width="925" alt="image" src="https://github.com/user-attachments/assets/3af21393-71f4-4aae-8e76-8b3adbd48ffc">

Making  a TCL file to print the result of multiplication of two numbers.

<img width="923" alt="image" src="https://github.com/user-attachments/assets/84cfeffd-8230-412b-adad-33c061519ebd">

Viewing the output. 

<img width="921" alt="image" src="https://github.com/user-attachments/assets/a62c551e-ff29-4bbb-af9c-824a92b40dc8">

Day 2 - Basics of STA

Getting  a deeper understanding of the minimum and maximum time delay due to hold time and the clock frequency respectively.

<img width="561" alt="image" src="https://github.com/user-attachments/assets/1a7d557c-7337-47dc-96e3-3ba4a513cf16">

Understanding an exaple about the inflow of water and relating it to the inflow of current. 

<img width="550" alt="image" src="https://github.com/user-attachments/assets/b916b7a8-583d-45c4-a36e-7d0cae33aa40">

An example to understand the direct proportionality between delay and load capacitance.

<img width="570" alt="image" src="https://github.com/user-attachments/assets/52802b30-9db1-47eb-8b5d-092bb34541be">

Understanding the relationship between the delay of the gate and the input transition and output load.

<img width="481" alt="image" src="https://github.com/user-attachments/assets/22ea11b2-7a05-4e00-8524-996ccc7bfc7a">

<img width="465" alt="image" src="https://github.com/user-attachments/assets/b8bd80e3-34e9-47ad-8d1c-d1078fe6cbee">

<img width="481" alt="image" src="https://github.com/user-attachments/assets/8a8389d8-e411-4a84-8137-8033b45429b4">

<img width="472" alt="image" src="https://github.com/user-attachments/assets/50ac57cc-f835-4d9f-bd45-1ae0dd3398ef">

<img width="543" alt="image" src="https://github.com/user-attachments/assets/ce654643-d142-4ae1-ba76-3019ff275055">

![WhatsApp Image 2024-07-27 at 12 43 06_7cd0c08b](https://github.com/user-attachments/assets/01e0dabe-a097-4beb-9692-baa0184b6844)

An example for timing paths-
![WhatsApp Image 2024-07-27 at 12 49 48_75ec7433](https://github.com/user-attachments/assets/2bc8280d-24b2-4242-8365-8960eb0948d6)

![WhatsApp Image 2024-07-27 at 13 03 16_988952e5](https://github.com/user-attachments/assets/544c51b8-8575-42f3-93c4-991a4230c8ef)

Thus the synthesis tool optimized the combinational logic based on the provided clock frequency.

![WhatsApp Image 2024-07-27 at 13 15 38_bd633c0d](https://github.com/user-attachments/assets/1cf58d07-6000-498b-8c8b-81b7dca8d4db)

There is an acceptable input and output delays defined in the contraints.

<img width="543" alt="image" src="https://github.com/user-attachments/assets/9025a409-8711-4e22-8738-f2021c119574">

<img width="581" alt="image" src="https://github.com/user-attachments/assets/a73b1744-3c93-473a-ab36-3e4b34847641">

<img width="539" alt="image" src="https://github.com/user-attachments/assets/596a0a29-cdd7-4ff6-8340-10b376c5b5c0">

Thus, the input external delay and the output external delay are calculated with respect to the assoiciated clock signal by the synthesizing tool.

<img width="587" alt="image" src="https://github.com/user-attachments/assets/85f8d07d-f214-4671-b7d3-5819d74d702c">

Thus it is observed that IO Modelling is based on two main factors as mentioned below-

<img width="367" alt="image" src="https://github.com/user-attachments/assets/af07d241-cafd-44c4-a8ba-fb3a819b7bf6">

![WhatsApp Image 2024-07-27 at 13 41 22_2ac76b50](https://github.com/user-attachments/assets/f29e66e8-d856-4635-bc03-2c9c1f9c2993)

Understandig how non-ideal signals affect the IO Delay Modelling.

<img width="547" alt="image" src="https://github.com/user-attachments/assets/fb599c38-c301-4349-94ce-a14b9039d757">

<img width="547" alt="image" src="https://github.com/user-attachments/assets/c16f9ffd-22b2-4846-9156-f7b37031cc9b">

<img width="538" alt="image" src="https://github.com/user-attachments/assets/4d80bc30-139e-4c8d-9d4f-68fedd97a5b7">

<img width="543" alt="image" src="https://github.com/user-attachments/assets/62357b90-ff91-4fbf-92d7-4303640ed7d6">

<img width="485" alt="image" src="https://github.com/user-attachments/assets/7f5772ed-d01b-47d3-a855-c84411d16168">

Lab 5 - Timing dot Libs

<img width="922" alt="image" src="https://github.com/user-attachments/assets/264f9814-7ce8-4fe7-a131-a57e5a86ea58">

If the maximum capacitance limit is violated then the net is buffered.

<img width="566" alt="image" src="https://github.com/user-attachments/assets/542f74e5-c832-4baa-bb7e-7bcfa073162d">

Understanding the funtionality of the Delay Model Lookup Table.

<img width="526" alt="image" src="https://github.com/user-attachments/assets/8ce854cd-fbe5-4e45-abdc-cfc22e5ec4d6">

There are different flavors of the same cell to meet the requiremets for the power consumption, area and delay. Note that dot lib also contain information about the cell leakage power and the power pins.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/d6f4e047-96ec-48af-b5e5-105225bcf592">

The dot lib also contains information about a paticular pin, for eaxample the pin is a signal pin or a clock pin, and capacitance associated with that pin.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/7c8a6e6b-919e-4e9b-8962-664d410a8ac5">

Thus for a flip flop, the clock attribute is true.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/dacd1fa5-48b0-44f9-9cad-b0b73eadfa94">

An example of the lookup table for and gates of different flavors to understand the delays for various output loads.

<img width="950" alt="image" src="https://github.com/user-attachments/assets/1de9fc4d-fe4b-4424-a560-0ae3e9aed092">

Comparing how the delay is affected for the vaious output loads for 2 input AND gate of different flavors.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/e47dc3d8-bef3-484a-86dc-c122b526470d">

The synthesis tool uses the properties of unateness to transmit information.

It is observed the AND and OR gates exhibit positive unateness while NOT, NAND and NOR gates have negative unateness. Note that XOR gate is non-unate. Thus a XOR gate can exhibit both positive and nagative unateness based on the inputs for the XOR gate.

<img width="558" alt="image" src="https://github.com/user-attachments/assets/f10ea268-40f9-4ba8-9d33-ad8b33f29e6a">

Complex gate can have one pin as positive unate and the other pin as negative unate.

![WhatsApp Image 2024-07-27 at 15 18 29_c3c641f0](https://github.com/user-attachments/assets/5a611924-5b9e-450d-b032-a3cf705db29c)


Lab 2 - Exploring dot Lib 

It is observed that the clock atrribute is true for an active low Flip Flop.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/d11464d5-bbb7-474d-8b17-4ce46f22bf88">

It is observed that the clock atrribute is false for an active low Flip Flop for the D pin.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/73c118bb-eaf8-48af-bfaf-017b250aa570">

It is observed there is no unateness for the output pin Q with respect to a clock for a FlipFlop.

<img width="337" alt="image" src="https://github.com/user-attachments/assets/378cf66c-a5bf-4a49-8bc6-014eb633100f">

We observe that the timing type is combination for an AND gate and falling edge for a Flip Flop.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/64a45093-260c-41d6-8a19-544330ed932a">

Note that the timimg type is with respect to the positive clock for the posedge Flip Flop and the negative clock for the negedge Flip Flop. This is observed  in the dot lib file as well.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/89ae1713-2501-40c2-9e90-f17bb5e7fa5d">

![WhatsApp Image 2024-07-30 at 20 02 04_88994eff](https://github.com/user-attachments/assets/c6869af1-94b9-4bfc-8f52-a95632ec3a9c)

Similary, the setup time is respect to the positive clock for the posedge Flip Flop and the negative clock for the negedge Flip Flop.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/9b8698d2-7dd9-40e6-9efa-98b1b0188567">

It is observed that the setup time is with respect to negative edge for the posedge latch and with respect to the positive edge for a negedge latch, which is observed in the dot lib file a as well.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/bacc78af-3deb-4d67-9047-7cd80f01b497">

![WhatsApp Image 2024-07-30 at 20 40 28_295c9666](https://github.com/user-attachments/assets/95161fb8-b63f-4f29-b946-cfe32f91e3db)

Introduction to the BabySoC:

Overview of SoC:

A System on Chip (SoC) is a single-die chip that integrates various intellectual property (IP) cores. These IPs can range from entirely digital components, such as microprocessors, to entirely analog components, such as 5G modems.

An SoC typically includes a central processing unit (CPU), memory, input and output ports, secondary storage devices, and peripheral interfaces such as timers. 

SoCs that deliver equivalent functionality often exhibit enhanced performance characterized by reduced power consumption and a smaller semiconductor die area.

The package-on-package (PoP) configuration is often employed in high-performance SoCs, where they are paired with physically separate memory or secondary storage that may be layered on top of the SoC.

It is important to note that a significant difference between a motherboard and an SoC is that the former comprises detachable components, whereas an SoC integrates all components onto a single integrated circuit.

Most mobile phones incorporate Snapdragon SoCs.

![WhatsApp Image 2024-08-08 at 11 47 34_f0d647c1](https://github.com/user-attachments/assets/db3cba00-6712-48f5-8be3-08a04e698613)


It has been observed that a Snapdragon SoC features an ARM architecture and includes a Krait CPU, an Adreno GPU, and a Hexagon DSP, among other components. 

A graphics processing unit (GPU) is a specialized electronic circuit designed to manipulate and alter memory to accelerate the creation of images in a frame buffer, which is then output to a display device. These GPUs are utilized in embedded systems such as mobile phones, personal computers, and gaming consoles.

A digital signal processor (DSP) is employed to measure, compress, or filter continuous real-world analog signals.

There are three distinct types of SoCs:
a) SoCs built around a microprocessor,
b) SoCs built around a microcontroller, commonly found in mobile phones,
c) Specialized application-specific integrated circuit (ASIC) SoCs designed for specific applications.

SoC Structure:

A System on Chip (SoC) comprises hardware functional units, including microprocessors that execute software code, as well as a communication subsystem to connect, control, direct, and interface between these functional modules. 

Functional components primarily consist of processor cores, memory, interfaces, digital signal processors (DSPs), and other essential elements. Inter-module communication within the SoC includes bus-based communication and network-on-chip (NoC) architectures.

The memory associated with an SoC can be either volatile or non-volatile. Volatile memory includes SRAM and DRAM, while non-volatile memory includes ROM. Encoders and decoders are used for interrupt handling and code conversion.

Peripheral devices connected to the SoC consist of externally connected interfaces such as Bluetooth, Wi-Fi, HDMI, and other similar technologies.

A Universal Asynchronous Receiver Transmitter (UART) is employed to transmit and receive serial data to and from the SoC. 

![WhatsApp Image 2024-08-08 at 11 51 01_477a7779](https://github.com/user-attachments/assets/15cdc697-226f-4a27-84c4-f2b469699ded)

![WhatsApp Image 2024-08-08 at 11 51 23_f66669f8](https://github.com/user-attachments/assets/a8fbbaef-84dd-45c3-8709-cda7709e34ae)

The RVMyth core features a RISC-V processor. A phase-locked loop (PLL) is used for synchronization purposes, such as clock signal generation and distribution. A digital-to-analog converter (DAC) is used in modern communication systems to convert digital output signals into analog signals, allowing the waveform to be easily viewed.

This structure ensures efficient integration and communication of various functional units, enabling the SoC to perform complex tasks effectively within a compact and power-efficient design.

Introduction to Modeling

Modeling Overview:
In the context of electronic systems, modeling refers to the creation of a physical or logical representation of a given system to generate data, inform decisions, or predict system behavior. This process aids in defining, analyzing, and communicating a set of concepts. Modeling and simulation are extensively utilized in the VLSI (Very Large Scale Integration) domain to support system analysis, specification, design, verification, and validation.

Purpose of Modeling:
System models are developed specifically to:
a) Support analysis and specification,
b) Facilitate design,
c) Enable verification,
d) Conduct validation,
e) Communicate specific information effectively.

Notably, mixed-signal circuits are primarily designed using modeling and simulation methods. FPGA (Field-Programmable Gate Array) is frequently employed for verification purposes.

BabySoC Modeling

Structure and Initial Setup:
The BabySoC modeling process begins with feeding initial input signals into the vsdbabysoc module, which triggers the PLL to generate the appropriate clock (CLK) signal for the circuit. This clock signal enables the RVMyth core to execute instructions stored in its memory (imem), subsequently filling register r17 with values cycle by cycle. These values are utilized by the DAC core to produce the final output signal, named OUT. The primary modeling task involves the three main IP cores: RVMyth, PLL, and DAC.

Introduction to RVMyth

RVMyth Details:

RVMyth stands for "RISC-V-based MYTH," where MYTH denotes "Microprocessor for You in Thirty Hours," and RISC signifies "Reduced Instruction Set Computer." The RISC-V ISA (Instruction Set Architecture) comprises a base integer ISA, which must be present in any implementation, plus optional extensions. The primary base integer variants are RV32I and RV64I, where "32" and "64" indicate the size of the registers, and "I" denotes integer operations. 

![WhatsApp Image 2024-08-08 at 11 55 30_88d0f288](https://github.com/user-attachments/assets/5821fd1e-6661-459d-84bd-45a00ede6a54)

Processor Stages:
The RISC-V processor utilizes a Harvard Architecture, featuring separate storage and buses for instruction and data to overcome the Von Neumann Architecture bottleneck. The processor operates in five stages:
1. Fetch,
2. Decode,
3. Read,
4. Execute,
5. Write back.

Pipelining is employed to perform multiple functions simultaneously, although it is essential to manage pipelining hazards. 

![WhatsApp Image 2024-08-06 at 13 43 16_80761d95](https://github.com/user-attachments/assets/62276f36-f547-40be-8324-2a43fad82f20)

Introduction to Phase-Locked Loop (PLL)

PLL Functionality:
A phase-locked loop (PLL) is an electronic circuit that uses a voltage-driven oscillator to constantly adjust to match the frequency of the input signal. PLLs are essential for generating, stabilizing, modulating, and demodulating frequencies.

Necessity of PLL in SoC:
Clocks in SoCs are generated using a quartz crystal oscillator. While off-chip oscillators can be used for frequencies under 100MHz, higher frequencies require on-chip PLLs due to several factors:
1. The need to supply clocks to multiple blocks on the chip, where longer wires could cause delays and clock jitter,
2. Different blocks on the same chip may require varying clock frequencies (e.g., one block may need a 300MHz clock while another needs a 100MHz clock),
3. The accuracy of the clock, measured in parts per million (ppm), which can have ppm errors when using off-chip clocks.

![WhatsApp Image 2024-08-06 at 13 52 35_2bb0a817](https://github.com/user-attachments/assets/700661ff-25ad-44eb-afb7-ac392ce27c7b)

![WhatsApp Image 2024-08-06 at 13 53 31_7a3412ce](https://github.com/user-attachments/assets/587833b2-d896-4dc0-a7ee-9dff50f6754e)

![WhatsApp Image 2024-08-06 at 13 54 25_62d83806](https://github.com/user-attachments/assets/39f997d4-abcd-4713-9e41-3b1430f8b7ad)
   
Introduction to Digital-to-Analog Converter (DAC)

A Digital-to-Analog Converter (DAC) transforms a digital input signal into an analog output signal. The digital signal is represented as a binary code, composed of a combination of 0s and 1s. A DAC typically features multiple binary inputs and a single analog output, with the number of binary inputs usually being a power of two.

Types of DACs

There are two primary types of DACs:
1. Weighted Resistor DAC
2. R-2R Ladder DAC

Weighted Resistor DAC:
A Weighted Resistor DAC generates an analog output that closely approximates the digital (binary) input by employing binary weighted resistors within an inverting adder circuit. This type of DAC is commonly referred to simply as a Weighted Resistor DAC. 

![WhatsApp Image 2024-08-08 at 12 04 33_8d7d777a](https://github.com/user-attachments/assets/3d50516a-fbb9-4563-9cf6-ea0d36cf3dfc)

Disadvantages of Weighted Resistor DAC:
The primary disadvantages of a Weighted Resistor DAC include issues related to precision and scalability, as the accuracy of the output heavily depends on the precision of the resistor values, which can become impractical for high-bit applications.

R-2R Ladder DAC:
The R-2R Ladder DAC addresses the disadvantages associated with the Weighted Resistor DAC. As the name implies, the R-2R Ladder DAC produces an analog output that closely matches the digital (binary) input by utilizing an R-2R ladder network within the inverting adder circuit. This design simplifies the resistor requirements, making it more practical and scalable for high-resolution applications.

![WhatsApp Image 2024-08-08 at 12 05 25_c2623a95](https://github.com/user-attachments/assets/fc10a868-39a0-4ada-aa9f-bf0863e0b342)

![WhatsApp Image 2024-08-06 at 14 05 45_7c6353a6](https://github.com/user-attachments/assets/92176632-64a1-40b2-a818-b090dac9ae21)

Initiating the Modelling Process
To model RVMyth, which is a digital block, Hardware Description Language (HDL) is employed for designing and verifying its functionality through a testbench. Since the DAC and PLL are analog components, Verilog cannot be directly used for synthesizing these designs. Instead, we simulate these components using Verilog with real data types to ensure their logical correctness. The primary objective is to verify the functionality through simulation. Verilog serves as the modeling language, Icarus Verilog (iverilog) is used for compilation and simulation, and GTKWave is utilized for waveform visualization and debugging.

Modelling and Simulation Workflow:

Modeling and Simulation Steps Using Icarus Verilog:
Icarus Verilog (iverilog) is a compiler for the Verilog hardware description language that produces a netlist in the desired format. The modeling and simulation process in iverilog comprises two primary steps:

Compilation:
iverilog builds the instance hierarchy and generates a binary executable (a.out). This executable is later used for simulation.

Simulation:
During compilation, iverilog generates a binary executable which is then used to simulate the design.

Tips for Effective Modelling:

Avoid race conditions.
Use an optimized testbench for efficient debugging.
Create models that simulate quickly.
Understand the behavior of case statements thoroughly.
Using GTKWave:

GTKWave provides a graphical interface for debugging designs by visualizing waveforms. The design is first run with a valid testbench using the commands:

iverilog design_file.v design_testbench.v

./a.out

This should execute without errors, and preferably without warnings. A .vcd file (Value Change Dump) is generated during this process. Ensure that these commands are run within the project directory or design folder.

RVMyth Modelling Steps:
The RISC-V CPU core is implemented in Verilog, with the corresponding testbench already in place.
The entire C program is converted into hex format and loaded into memory.
The CPU reads the memory contents, processes them, and outputs the result.
The following commands are executed to model and simulate the design once the respective git repository is cloned:

iverilog mythcore_test.v tb_mythcore_test.v

./a.out 

gtkwave mythcore.vcd

![WhatsApp Image 2024-08-20 at 21 25 00_0abcba75](https://github.com/user-attachments/assets/fcc7905b-7a38-4d11-99dd-6bca372b48ee)

Modelling DAC and PLL:
The  following steps are used for the modellling of DAC and PLL-
1. git clone https://github.com/manili/VSDBabySoC.git - this repo contains the design and testbench files for the BabySoc
2. changing the directory using cd VSDBabySoc
3. sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/ command is run to convert the .tlv defined rvmyth to .v
   It generates vmyth.v and rvmyth_gen.v.
   ![WhatsApp Image 2024-09-07 at 21 00 15_4d090f78](https://github.com/user-attachments/assets/dd4a2002-88d7-42fb-b3f1-91f6eaca5c61)

5. iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module - is used to compile and simulate vsdbabysoc design.
6. cd output
7. ./pre_synth_sim.out - generateS pre_synth_sim.vcd file which is used to view the waveform.
8. gtkwave pre_synth_sim.out - to view the waveform in gtkwave tool.

![WhatsApp Image 2024-09-07 at 14 33 19_23293899](https://github.com/user-attachments/assets/c33f6ac1-e5f1-4f91-9787-3c509a78d996)

Post Synthesis Simulation (GLS) on BabySoc 

Note that pre-synthesis simulation id done to check whether the logic designed for a paticular functionality holds good. Post-sysntesis-simulation/gate-level-simulation is done to ensure that the after sysnthesis the delayed accounted for the gates lies within the range of allowed delays such that the timing and the functionality is not violated.

Synopys tools such as Design Compiler (dc_shell) and Library Compiler (lc_shell) will be implemented for the Post Synthesis Simulation.

Steps for Post-sysntesis-simulation
1) avsddac.lib, avsdpll.lib and sky130_fd_sc_hd__tt_025C_1v80.lib need to be converted to .db file using lc_shell
   
   ![WhatsApp Image 2024-09-14 at 20 56 09_fac147ce](https://github.com/user-attachments/assets/6a860819-3bcb-459e-b7ce-75de8d5dcc1e)
   Some errors are observed on performing the above function that need to be debugged. 

   ![WhatsApp Image 2024-09-14 at 21 18 17_1c8572c0](https://github.com/user-attachments/assets/b68e97f8-7932-49ac-bd94-4477146f58aa)
   Once the errors have been debugged only warnings are observed on running the read_lib commmand which can be ignored for now.

   The following commands are used to synthesize the design
   set target_library /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db
  set link_library {* /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/lib/avsdpll.db /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/lib/avsddac.db}
  set search_path {/home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/include /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/src/module}
  read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc  
 link  
 compile_ultra
  write_file -format verilog -hierarchy -output /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC/output/vsdbabysoc_net.v

![WhatsApp Image 2024-09-24 at 21 19 19_46fd3a2e](https://github.com/user-attachments/assets/9a0a25bf-74eb-4a14-9fc0-5d8899ccd349)

The following commandsare then executed in /home/avneet/vsd/VLSI/rvmyth/VSDBabySoC :
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v

 cd output
 
 ./post_synth_sim.out
 
  gtkwave dump.vcd

  The post-synthesis waveform is then compared with the pre-synthesis waveform 
  
![WhatsApp Image 2024-10-05 at 20 56 15_f48a59d5](https://github.com/user-attachments/assets/ee987a59-7c0d-4498-be5e-cc787527892c)

Thus the waveform from the pre-sythesis and from the post-synthesis are the same. 

Sythesis and Timing Analysis of the BabySoc-

Day 1- Inception of open-source EDA, OpenLANE and Sky130 PDK

![WhatsApp Image 2024-08-13 at 21 18 03_7683f1a5](https://github.com/user-attachments/assets/10018a03-00c2-47e4-ba92-611b4a3b4c5a)

Image of a package. This is an example of the QFN-48 package that has dimensions 7mmx7mm.

![WhatsApp Image 2024-08-13 at 21 18 46_1d9636c4](https://github.com/user-attachments/assets/a95e87a8-bb3d-4bc3-97c5-b94f132f45cb)

The chip is placed at the center and is connected to the package using wire bonds.

![WhatsApp Image 2024-08-13 at 21 19 21_5dac7a4c](https://github.com/user-attachments/assets/577091e7-62d8-4e27-9bad-af3dad8f92a2)

![WhatsApp Image 2024-08-13 at 21 29 01_d849464d](https://github.com/user-attachments/assets/b39a71e1-6a47-4a5b-bcfd-6f88f2ea2448)

A diagram of the internal components of the chip with the foundry IPs and the macros indicated. It is to be noted that macros is pure digital logic and the IPs requires some intelligence to built and hence the name intellectual property.





























































































































































































































































