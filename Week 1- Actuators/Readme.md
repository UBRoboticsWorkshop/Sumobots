# Week 1: Actuators

Welcome to our first weekly workshop! Today, we're going to be looking at some of the actuators we'll be working with for Sumobots.

Today, we've given you a few components:

- TT motor
- MX1508 motor driver
- 9g servo motor

The main purpose of this lab is to get you used to working in the CTL, using the VirtualBench all in one electronics lab and getting a feel for what you can expect from the components we provide. Engineering is often flooded with equations and simulations, so this is a chance to get an intuitive feel for how these systems work in the real world.

We'll be providing you with your full bag of parts (including some better servos) in a later workshop (Workshop 3- Programming) where you'll learn about how to integrate a programmable controller into your robot. Next week, we'll show you how you can use CAD models of these components to quickly create 3D designs and get them ready for rapid prototyping.

Last off, we'll have plenty of catchup sessions throughout the process and we'll also be going more in depth on how to troubleshoot and find issues later on as you get more comfortable with the lab equipment. There's plenty of committee members around the lab ready to help you, so feel free to flag one of us down if you need a hand.

## Step 1: Powering on the VirtualBench
Firstly, make sure the power button on the VirtualBench is glowing blue to show that it is turned on. Next, follow the video to connect it to your PC:



https://github.com/user-attachments/assets/c603f638-95df-4d05-8037-df8cd587d8ef



Next, open the NI VirtualBench App:

![image](https://github.com/user-attachments/assets/e15f0229-3292-4196-b8f1-8d9283ccbc6b)


Once opened, you should be met with this:

![image](https://github.com/user-attachments/assets/9cf3eab4-d96b-4035-8890-8b0f4025acac)


You should see a red line on the screen in the main panel- this is the oscilloscope, which will soon be your best friend when things go wrong. This can be used to measure voltage, and see how it changes over time. Let's try it out:

![image](https://github.com/user-attachments/assets/89d9b801-8d3c-448b-9a16-dff13037912b)

Press this button to turn on the DC power supply. Now, plug two wires into +5 volts and ground of the Power Puck:

![619mdu96pwL](https://github.com/user-attachments/assets/889ece24-d3bd-4987-ab2b-b3446d2345df)
Alligator clips can be used to grab wires.


![Group 1 copy](https://github.com/user-attachments/assets/ae584e7b-62bb-4bec-8a0d-ad5bd0561c41)
This is the main DC output of the VirtualBench.


<details> <summary> Oh No! I shorted out the power supply!

</summary>

Don't worry, this power supply can automatically detect if you touch power and ground together. If you do this, it'll just turn off until you disconnect them.

![image](https://github.com/user-attachments/assets/6c65a0fd-58c3-4f1a-b9d1-fbfa92731706)

Here, we can see that it will highlight which part has a short circuit. 

</details>

![WhatsApp Image 2024-10-10 at 22 07 54 (1)](https://github.com/user-attachments/assets/5bddb0dc-ace3-44d1-b123-8d22d5d90369)

Add a probe to channel 1 of the oscilloscope, and one to the function generator: 

https://private-user-images.githubusercontent.com/110237339/276246666-073db8e7-e66d-4dd9-986e-72c3535ebe6d.MOV?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MjkwMDEzMDAsIm5iZiI6MTcyOTAwMTAwMCwicGF0aCI6Ii8xMTAyMzczMzkvMjc2MjQ2NjY2LTA3M2RiOGU3LWU2NmQtNGRkOS05ODZlLTcyYzM1MzVlYmU2ZC5NT1Y_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMDE1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTAxNVQxNDAzMjBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NjVkM2RhZDE0MzE5YTY4NDJkNTBmZWIxZDhjMjA4MjAwMzE0Mjg4OWRlNjVhMjQ2N2Q3MzdjZGIyZDRhMTllJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZEvNy6WtsBvkAHiocHCWJpqEy3pHr8yC50MiNWit2Ts

Make sure the slider on the probe is set to 1x. If it's set to 10x, the function generator may do odd things. We'll use the probe connected to FGEN later, for now just use channel 1.

Now, touch the probe to the wire that's connected to the +6V port. You should see the red line jump up, like so:

![image](https://github.com/user-attachments/assets/56001bef-2b97-4acf-ba02-6cd8d3bffa60)

Looking at the red underlines, we can see that the scale in the top right is set to 2V per division and the voltage is set to 5V. The red line is 2.5 lines up from the middle line (shown by the little red arrow to the left), indicating that the probe is reading 5V. Using the arrows above and below the volts per division indicator, we can zoom in and out to better see small or large signals. During Sumobots, we won't need to zoom in and out much.

Throughout this workshop, feel free to use the probe to see what voltage the different parts of the circuits are at by simply touching it to exposed connectors.

<details> <summary> Don't I need to connect the oscilloscope ground as well?

</summary>

The small wire with an alligator clip is the ground pin of the probe. You can connect this to any part of the circuit to see the voltage difference between the clip and the probe.

By default, it is tied to the ground of the power supply- so if you're powering your robot off the VirtualBench, there's no need to use it.

Later, when your robot is battery powered, you'll need to clip this to the negative terminal of the battery pack.

</details>

## Step 2: Wiring up a DC motor
Solder some wires to the DC motor following the video below:



https://github.com/user-attachments/assets/abdbac26-b67c-46c6-8ea6-03529b887984



You can now connect the VirtualBench power supply to the motor, and it should begin to spin. Reverse the leads, and it should spin backwards. You can change the voltage and see how the motor speed changes. Make sure that you're using the channel marked +6V.

#### DON'T USE MORE THAN 6v, THIS WILL BURN THE MOTOR

## What's PWM, and why?
To make a robot move smoothly, we'll often want to set a motor to go at speeds other than fully off or fully on. The easiest way to do this is to simply change the voltage that you apply to the motor. 

However, most motor drivers and microcontrollers don't provide any way to do this- they're either 100% on or 100% off. To get around this, we can just turn it on and off really, really quickly- somewhere in the order of 20,000 times per second.

We can adjust how much time we spend on vs off, which is called duty cycle. We can refer to this as a percentage from 0-100. For example: 1ms on followed by 1ms off repeating would be 50% duty, 1.5ms on followed by 0.5ms off would be 75% duty, 2ms on followed by 0ms off would be 100% duty.

As we are controlling on and off times, we refer to this as "Pulse Width Modulation"


## Step 3: Using PWM to control a DC motor 
For this, we'll use the function generator on the VirtualBench. This allows us to generate repeating signals. In this case, we'll create a square wave between 3.3V and 0V- which is what we'll later generate from the microcontroller. To connect the function generator, use another probe like the one for the oscilloscope. They should also come with caps that allow a wire to be grabbed, which can then be plugged into your breadboard.

However, both the microcontroller and the function generator aren't able to run the motor- the motor needs up to 1000mA of current, and the microcontroller can only provide about 40mA. This is where a motor driver comes in- we can use it as an electrical switch, where our 3.3v signal can control out 6v motor. There will also be next to zero current needed to control the motor driver, so our microcontroller will be kept safe.

Soldering the motor driver will be a little more difficult. If you're new to soldering, pick up a sheet of perfboard from the front and practice like so:

https://github.com/user-attachments/assets/acad5f65-a17c-4fb4-99eb-d68c94bd34d7

You can see here how the copper surface of the PCB wicks heat away from the solder joint, and briefly causes the solder to resolidify. If this happens, continue to apply heat until you get a good joint with strong contact on both the wire and the PCB. 

![SolderLooks](https://github.com/user-attachments/assets/9202a508-8e00-4759-87f6-61134a78f12e)


The leftmost joint is what happens when you only heat the pin and not the board. Next, too much solder- it might creep over onto other tracks. Finally, a good joint with gently curving solder on to the pin.

Now, move on to the motor driver:

https://github.com/user-attachments/assets/799cba47-a495-4bb7-8b3e-e515852fb567

Now wire it up like so:

![image](https://github.com/user-attachments/assets/ff7cc30b-3c1f-40ca-a2f8-b495ee56af37)


And set up your function generator like this:

![image](https://github.com/user-attachments/assets/e53554ac-2abc-4569-aceb-6e9ce17d4b8c)

Make sure the underlined values are the same.

## Step 4: Looking inside the wires with an oscilloscope, or something to that effect
The main display panel is for the digital oscilloscope, which shows voltage over time. You can use this to see how the voltage flowing through the wires changes over time, giving you an easy way to spot errors and see how the system works. Try probing the wire from the function generator as well as the wires going to the motor- is the voltage to the motors what you'd expect it to look like? 


https://github.com/user-attachments/assets/48323594-7fd9-4a88-9e7d-455e5e5f29ce


## Step 5: PWM for signals 
For driving the DC motor, we used PWM to quite directly switch the motor on and off. However, this is not the only use for PWM- it can also be used to transfer data, in this case by Modulating the Width of the Pulses between 1000uS and 2000uS. Servo motors time how long the pulse is on for, and then go to an angle proportional to the length of the pulse- 0 degrees, for 1000uS, 180 degrees for 2000uS, 90 degrees for 1500uS. Wire up the servo motor as shown in the following:



https://github.com/user-attachments/assets/e0b9c290-dd0c-4a3b-9724-88757a17357e

The brown wire should connect to ground, the red servo wire should be connected to power (between 3 and 6 volts) and the yellow/orange wire should be connected to the function generator. 

![thumbnail_VB8012-31FC7FA_2024-10-10_14-54-23 07p duty cycle](https://github.com/user-attachments/assets/82e00f2a-2932-4f60-a77c-b02927b5d7e2)

![VB8012-31FC7FA_2024-10-10_14-55-00 13p duty cycle](https://github.com/user-attachments/assets/03ea5db7-3f51-4517-9e8c-8812e2c55ec4)


Please note that PWM is quite an outdated way of sending signals- it's acceptable for basic servos like these and it's simple to use. For more complex data transmittion, serial data protocols like I2C and SPI are generally needed; we'll circle back to this later on in semester 2, where you'll see how to use these to communicate with drone avionics.

# Conclusion 

Hopefully you enjoyed our intro session and have had a chance to network with your new teammates! Next week our session will be on CAD- increasingly, requirements of rapid prototyping is taken as a given for prospective engineering jobs. Knowing how to take designs from Fusion 360 and use a range of machinery to best create a suitable part is an invaluable skill to employers, and there's no better place to learn than the SoE makerspace. Join us next week to get started!

Also, make sure to sign up for PPMS and hand tool training. If your whole team can show that they have these sorted, you'll receive a BIG SERVO. When I run out of BIG SERVOs, there will be no more- so get trained fast, and crush your enemies with a BIG SERVO.
