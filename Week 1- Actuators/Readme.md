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



https://github.com/user-attachments/assets/c582d064-72d2-4bd6-991c-af259128a315



Next, open the NI VirtualBench App:

![375402606-e15f0229-3292-4196-b8f1-8d9283ccbc6b](https://github.com/user-attachments/assets/aa75ab68-f03b-419a-a6f7-53090489bfb9)

Once opened, you should be met with this:

![375404248-9cf3eab4-d96b-4035-8890-8b0f4025acac](https://github.com/user-attachments/assets/e34073ed-124c-4ee8-ac79-6e5dec457d25)

You should see a red line on the screen in the main panel- this is the oscilloscope, which will soon be your best friend when things go wrong. This can be used to measure voltage, and see how it changes over time. Let's try it out:

![375405732-89d9b801-8d3c-448b-9a16-dff13037912b](https://github.com/user-attachments/assets/e77c4c44-c7f2-451f-b82b-2a6353d4a21c)


Press this button to turn on the DC power supply. Now, plug two wires into +5 volts and ground of the Power Puck:

![376653325-889ece24-d3bd-4987-ab2b-b3446d2345df](https://github.com/user-attachments/assets/c0fd5d22-d145-4af6-a83f-ab3eb4474bbe)

Alligator clips can be used to grab wires.


![375563558-ae584e7b-62bb-4bec-8a0d-ad5bd0561c41](https://github.com/user-attachments/assets/fa0767b8-b0d3-450d-b869-f5d9d93c749a)

This is the main DC output of the VirtualBench.


<details> <summary> Oh No! I shorted out the power supply!

</summary>

Don't worry, this power supply can automatically detect if you touch power and ground together. If you do this, it'll just turn off until you disconnect them.

![375412868-6c65a0fd-58c3-4f1a-b9d1-fbfa92731706](https://github.com/user-attachments/assets/b26b251d-c09e-46d8-9bda-ca59bb82409c)


Here, we can see that it will highlight which part has a short circuit. 

</details>

![WhatsApp Image 2024-10-10 at 22 07 54 (1)](https://github.com/user-attachments/assets/5bddb0dc-ace3-44d1-b123-8d22d5d90369)

Add a probe to channel 1 of the oscilloscope, and one to the function generator: 

https://github.com/user-attachments/assets/f6ffb65d-b1cd-4f59-90d7-93883830382c

Make sure the slider on the probe is set to 1x. If it's set to 10x, the function generator may do odd things. We'll use the probe connected to FGEN later, for now just use channel 1.

Now, touch the probe to the wire that's connected to the +6V port. You should see the red line jump up, like so:

![375408794-56001bef-2b97-4acf-ba02-6cd8d3bffa60](https://github.com/user-attachments/assets/634c4f5a-f51b-4b25-b8a0-103972d2d50f)

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

https://github.com/user-attachments/assets/9cc833d5-b5dd-425b-8254-63da340a5423

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

https://github.com/user-attachments/assets/17cb1d30-4794-4f8f-8351-be740d171bc2

You can see here how the copper surface of the PCB wicks heat away from the solder joint, and briefly causes the solder to resolidify. If this happens, continue to apply heat until you get a good joint with strong contact on both the wire and the PCB. 

![375563631-9202a508-8e00-4759-87f6-61134a78f12e](https://github.com/user-attachments/assets/647fe92d-1df4-4b4d-8d6e-267297f19a64)


The leftmost joint is what happens when you only heat the pin and not the board. Next, too much solder- it might creep over onto other tracks. Finally, a good joint with gently curving solder on to the pin.

Now, move on to the motor driver:

https://github.com/user-attachments/assets/e7ccd321-b712-4b35-be32-1b9955c77070

Now wire it up like so:

![376662733-ff7cc30b-3c1f-40ca-a2f8-b495ee56af37](https://github.com/user-attachments/assets/6763e306-98a6-496f-904b-71f2ac65196a)

And set up your function generator like this:

![375419324-e53554ac-2abc-4569-aceb-6e9ce17d4b8c](https://github.com/user-attachments/assets/1a0d64f4-c58f-49fe-9b90-57efceea8375)

Make sure the underlined values are the same.

If you want to understand how the MX1508 works, you can read more [here](https://github.com/UBRoboticsWorkshop/Sumobots-2024-25/blob/main/1-Actuators/Detail%3A%20MOSFETs%20and%20Power.md).

To look deeper into the electronics of a DC motor, and how this can help your robot, try [this](https://github.com/UBRoboticsWorkshop/Sumobots/blob/main/Week%201-%20Actuators/Extension%3A%20Breakover%20Voltage.md).

## Step 4: Looking inside the wires with an oscilloscope, or something to that effect
The main display panel is for the digital oscilloscope, which shows voltage over time. You can use this to see how the voltage flowing through the wires changes over time, giving you an easy way to spot errors and see how the system works. Try probing the wire from the function generator as well as the wires going to the motor- is the voltage to the motors what you'd expect it to look like? 

https://github.com/user-attachments/assets/85ef4985-5c84-4bd0-b07a-ec34389e4f43

## Step 5: PWM for signals 
For driving the DC motor, we used PWM to quite directly switch the motor on and off. However, this is not the only use for PWM- it can also be used to transfer data, in this case by Modulating the Width of the Pulses between 1000uS and 2000uS. Servo motors time how long the pulse is on for, and then go to an angle proportional to the length of the pulse- 0 degrees, for 1000uS, 180 degrees for 2000uS, 90 degrees for 1500uS. Wire up the servo motor as shown in the following:

#### Make sure that the function generator setup is the same as in the video! It needs to run at 50Hz

https://github.com/user-attachments/assets/f81ff454-7507-4df9-a888-9be75c805a77


The brown wire should connect to ground, the red servo wire should be connected to power (between 3 and 6 volts) and the yellow/orange wire should be connected to the function generator. 

![375561771-82e00f2a-2932-4f60-a77c-b02927b5d7e2](https://github.com/user-attachments/assets/503e60a3-4aef-4f4d-87c0-075c30d7942d)

![375561860-03ea5db7-3f51-4517-9e8c-8812e2c55ec4](https://github.com/user-attachments/assets/250c5015-2401-44f7-b981-7c0216a61977)


Please note that PWM is quite an outdated way of sending signals- it's acceptable for basic servos like these and it's simple to use. For more complex data transmittion, serial data protocols like I2C and SPI are generally needed; we'll circle back to this later on in semester 2, where you'll see how to use these to communicate with drone avionics.

# Conclusion 

Hopefully you enjoyed our intro session and have had a chance to network with your new teammates! Next week our session will be on CAD- increasingly, requirements of rapid prototyping is taken as a given for prospective engineering jobs. Knowing how to take designs from Fusion 360 and use a range of machinery to best create a suitable part is an invaluable skill to employers, and there's no better place to learn than the SoE makerspace. Join us next week to get started!

Also, make sure to sign up for PPMS and hand tool training. If your whole team can show that they have these sorted, you'll receive a BIG SERVO. When I run out of BIG SERVOs, there will be no more- so get trained fast, and crush your enemies with a BIG SERVO.

[PPMS signup here](https://github.com/UBRoboticsWorkshop/Sumobots/blob/main/Week%201-%20Actuators/PPMS%20Instructions.pdf)
