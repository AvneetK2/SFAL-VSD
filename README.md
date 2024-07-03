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













