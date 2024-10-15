# Breakover Voltage

DC motors exhibit a feature known as breakover voltage- this is the minimum voltage at which the motor will start to turn.

For a robot which will be trying to attempt to outmanoeuvre your opponents, it's really important that your low-speed control is very precise so you can slip in at that perfect angle to catch the opponent off guard.

## What are we actually controlling?
This is always a good question to ask when designing a control system. PWM attempts to emulate an analog voltage: 6v supply at 25% duty cycle means about 1.5v on average. But how does the voltage applied to the motor actually effect the physical world?

We can model a motor as follows:

![image](https://github.com/user-attachments/assets/9faf72da-8372-49f2-bcb5-5cf2e84a6401)

A resistor, inductor and "back EMF" voltage supply wired up in series.

The back EMF creates voltage in the opposite direction to the supply, proportional to the speed. How many volts it generates is determined by the motor's construction- how many turns in the windings of the motor, how strong the permanent magnets are and so on.

A resistor opposes the flow of current, which will be the voltage across the resistor divided by its resistance. This is determined by the resistance of the copper coils used to create the motor.

An inductor opposes changes in current- when a voltage is applied to it, the current flowing through it will change at a rate proportional to the voltage across it. This is determined by the materials the motor is made of, and also how many turns are in the motor's coils.

In short, when we apply voltage to a motor the current running through it will begin to rise as the inductor resists the change in current. Eventually, the inductor will "saturate"- this means it acts as a short circuit, with zero resistance. When this point is reached, the current will be limited by V=IR- where V is the difference between the voltage applied to the motor and the voltage created proportional to the speed of the motor, and R is the resistance of the motor's windings.

Current flowing through a magnetic field (created by permanent magnets in the motor) is what creates twisting force- torque. This means that as the current rises, the torque created by the motor will also increase.

The motor will spin faster and faster as the torque causes the angular velocity of the motor to increase. However, the back EMF voltage created by the motor will also rise until eventually it becomes equal (or close to equal) to the power supply- at this point, the current flowing through the motor will be nearly zero (or, however much current is required to overcome frictional forces in the motor). Applying load to the motor will drop the speed, and in turn increase the voltage difference between the supply and back EMF- causing more current to flow. This is why current in the motor increases when we add more load to the output shaft.

## How can we control it better?
There will be a few times in this process where you can improve your Sumobot by modifying how you control the motors. In order to experiment with reducing the breakover voltage for finer low speed control, try adjusting the PWM frequency. How does this affect the motion of the motor? Is there an optimal frequency? And considering the model of the motor, why is this the case?
