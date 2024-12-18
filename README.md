# ECE425_Final_Project


ECE 425

Microprocessor Systems

Final Project
Pathfinder Robot


Lenny Marron
Roger Xu
Instructor: Aaron Nanas
Fall 2024


Introduction:
This project fulfills the final project requirement for the following classes at California State University, Northridge (CSUN):

Project Goals
To design and assemble a small robot that involves the use of an ultrasonic sensor, and Two DC geared motors to give the robot the ability to follow a specified path while avoiding obstacles/obstructions. Using software written in C with Keil as the development tool, the software instructions are sent to the TM4C123GXL hardware board to process the data. This project explores data transmission and communication protocols like UART, motor control with PWM, Timer, and main microcontroller-peripherals interactions.


Background and Methodology:

We used UART module 1 to transmit and receive the distance measured by the ultrasonic sensor to the microcontroller and we used UART module 0 to allow us to view the data seen by the microcontroller. Once the data was confirmed to be correct we then commented out the code relating to UART module 0.
The DC motors were driven by the DRV8833 breakout board which used 4 separate PWM inputs to allow the robot to move forward, backward, left, and right. We based our motor control using logic in Table 1 below.

				Table 1 Motor Control Logic
 
By using the DRV8833, it provided the ability to control 2 DC motors with +3.3V input logic and a small footprint. The speed of the motors was adjusted by changing the duty cycle of the PWM modules. When one motor has a higher speed than the other, the car will turn in that direction. When both motors have the same speed, the car will move forward or backward.

Once the drivers for all 4 PWM signals and the 2 UART modules were confirmed as working, a Timer Interrupt was created in order to periodically check for any objects in front of the robots path. The timer was set to count every 1 ms but would only check the distance in front of it every 1 second. Whenever an object was less than 10 cm away from the robot the robot would reverse and turn right, for all other cases the robot would continue to drive forward.




We also 3D printed the ultrasonic sensor housing below in order to keep the location of the US-100 sensor the same the entire time.
CAD model of 3d Printed Parts

![alt text](https://github.com/lmarron7138/ECE425_Final_Project/blob/main/Schematic/Pathfinder_Schematic.pdf)


  
Block Diagram:

 
Table of Components:
Part	QTY	Picture
5 Channel IR Tracking sensor module	1	 
DC Geared Motors with wires	1	 
Adafruit DRV8833 DC/Stepper Motor Driver Breakout Board	1	 
EK-TM4C123GXL microcontroller	1	 
US-100 Ultrasonic sensor	1	 
+6V (AA) battery Pack	1	 
+5V Coast Rechargeable Battery	1	 

Pinout Table :

EK-TM4C123GXL Microcontroller	Function Used	DRV8833 
Breakout Board	US-100 
Ultrasonic Sensor
PB6	PWM0_0
(Right motor forward)	BIN1	
PB4	PWM0_1
(Right motor backward)	BIN2	
PF2	PWM1_3
(Left motor forward)	AIN2	
PA6	PWM1_1
(Left motor back)	AIN1	
PA0 (U0RX)	UART0		
PA1 (U0TX)	UART0		
PB0 (U1RX)	UART1		Echo/RX pin 3
PB1 (U1TX)	UART1		Trig/TX pin 2
Schematic:

 













Analysis and Results :
One of the issues we ran into while working on this project was implementing both the 5 channel IR tracking Sensors and the US-100 sensor at the same time. Although the interrupt function for the IR sensor worked fine we always had errors when implementing both together. Next time we will order an IR-sensor module that includes a datasheet and comes from a reliable source. When troubleshooting this module using a multimeter, we noticed the output voltages at ~ +1.7V when sensing the black tape, which in turn caused the micro to read the input as a Logic High, instead of Logic Low. We believe that if it weren’t due to the lack of a datasheet we might have been able to fix this issue. 
Another issue we faced is parsing the distance value measured by the ultrasonic sensor to the microcontroller. We have had a lot of trouble setting the microcontroller to measure the time it takes for the ultrasonic sensor to receive its echo(which is how it measures distance), we bypassed this issue by using UART as a communication method instead of a direct pin connection. Aside from programming obstacles, we have also experienced physical hardware roadblocks. The ultrasonic sensor holder was not fitting properly, so we had to 3D print new parts. However, despite all the setbacks, we were able to successfully build a robot that scans its surroundings using sensors and makes speed and direction changes based on its sensory inputs.

Video Demonstration
Short video demonstration of collision avoidance:
●	Video demo 1
●	Video demo 2
Conclusion:
In conclusion, this project is the culmination of everything we have learned in the class, from C programming to GPIO to GPTM to PWM to UART. We connected different parts and peripherals to the microcontroller by assigning and connecting them using GPIO pins. We applied communication methods of UART to transfer distance data from the ultrasonic sensor to the MCU by setting the appropriate baud rate. In addition we designed the robot to periodically check its surroundings so as to not drain the batteries as quickly.  We learned how to use duty cycles to change the speed of the motors by manipulating the duty cycle of the PWM, and thus enabling us to adjust the speed of the motor. We also learned how to use an H-bridge circuit to control the direction of our robot. We used various C programming techniques to build up the control logic needed to instruct the robot how to handle different situations. This project has helped us gain a deeper understanding of MCUs and the crucial roles they play in real life embedded systems. 
