Lab 0: Installation of tools 
![Screenshot GTKWave](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/e27255da-469b-481d-b963-9b3462ea48cd)
![Screenshot yosys](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/5a164a3a-d08f-44ab-b221-0e0ec611ea25)
![Screenshot iverilog](https://github.com/AvneetK2/SFAL-VSD/assets/173355761/f59c520f-06a6-457e-973e-91b526b1985f)

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











































































































