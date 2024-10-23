# How an H-Bridge Works
## Layout 
An H-bridge is a device built out of four transistors that allows for electricity to run in either direction through a load:

![image](https://github.com/user-attachments/assets/b2321abe-0277-472d-985c-0641899fcdf0)


## MOSFETs

Q1,2,3,4 are MOSFETs, a type of transistor that works as an electrical switch.

![image](https://github.com/user-attachments/assets/adcd7165-bc18-4b9a-877e-adea40c7439d)


When we apply a voltage to the gate pin, the MOSFET will conduct between the drain and source pin- just like connecting the two wires together. This means we can use a low voltage, low current signal to turn on and off a powerful device like a motor- which will be very important later on when we want to use a microcontroller to turn the motors on an off.

Our sumobot controllers can only supply about 40mA of current, while these motors can draw over 1000mA- which will cook the sumobot controller easily. Luckily, turning the MOSFETs on and off only takes a tiny amount of current. This also means we can use the 3.3v that the sumobot controller runs on to switch the ~6v that the battery provides, which will make the motors far more powerful.

## How This Helps Your Sumobot Run Away
There's no shame in a tactical retreat, and in Sumobots it's likely you may find yourself wanting to do this. By applying voltage to the pins labeled INA, current will flow as shown:

![image](https://github.com/user-attachments/assets/986336cd-2f45-4e02-87b7-ff89aaf22a28)



However, by applying voltage to INB, the current will flow in the opposite direction:

![image](https://github.com/user-attachments/assets/049bdd72-847d-4923-8df6-d4369cc52bbc)

This will allow you to run your motor either forwards or backwards.

# Futher details
MOSFETs can come in different varieties such as: N-channel or P-channel and enhancement or depletion. This can alter whether positive or negative voltages need to be used on the gate, and whether it conducts when the gate is high or low. However, N-channel enhancement MOSFETs are the most common type due to better performance and lower cost. This means they are generally a better choice as a switch than other types of MOSFET.

I have also oversimplified some details here, such as: gate charge, on resistance, thermal current limits and more. The motor drivers we use also feature control logic that can prevent all four MOSFETs turning on and causing a short circuit, as well as (allegedly) over temperature shutdown. They also make use of what's known as a gate driver, which handles a few issues that arrise when you switch MOSFETs very quickly. MOSFET gate voltage is also determined by the difference between source and gate- so if the voltage at the source is higher than zero, you need to somehow boost your gate voltage to be (source + switching voltage)- this is also handled by the gate driver. 

If you want to learn more about advanced power control, consider joining the locomotion team for Eurobot where you'll get involved building high power motor drivers for three phase motors.
