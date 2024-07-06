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

































