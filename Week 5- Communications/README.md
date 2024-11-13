# Communications

As your Sumobot is a (hopefully) remote operated system, you'll need a way to transfer data between your controller and your robot. In second semester we'll look at some slightly more advanced ways to achieve this, but for Sumobots we'll be primarily using WiFI.

We'll be mostly looking at using UDP in order to control the robot from your laptop, using WASD. 

Read over the code here carefully, since there are a few easy ways to boost your robot by modifying it from defaults.

## WiFi Protocols
### TCP
TCP is a handshake based system. What this means is that if a packet fails to be transmitted, it'll get re-sent. In many applications this is useful, however for our robots an old packet suddenly coming through might cause your robot to act erratically- a hard left turn might've been wanted 10 seconds ago, but now will send you flying off the edge.

For this reason, TCP isn't a very choice here- we'd rather dropped packets just disappear.

### UDP
Universal datagram packets are an array of bytes which can be used to transmit data over WiFi. Here, it should be fine to simply represent all of our values as either signed or unsigned integers- numbers from -127 to 128 or 0-255 respectively.

However, we can also use these bytes to represent more complex data types such as floats, or multi byte integers. We'll look more at this in second semester- Sumobots won't really require complex maths or finer control than single bytes provide.

## Network design
There are two types of WiFi unit here: access point, and station. The ESP32 is capable of acting as both. Access points are Wifi sources, like a router or a mobile hotspot while stations are the devices that connect to them, like a phone or laptop.

However, operating an access point requires more power on the ESP32 so it makes more sense to offload this task to either your phone or laptop. The easiest approach is to open WiFi sharing on your laptop, and create an access point there.

#### Make sure to keep your access point password secret! Consider changing it on competition day

Any attempts at electronic warfare will result in a ban, and great sense of shame.

Go into settings -> Network and internet -> Mobile hotspot (this may be called network sharing on some devices)

![image](https://github.com/user-attachments/assets/08ee4867-e7e4-4491-b4f6-40f38305ea64)

Set the SSID to your team name, and pick a password for testing. Ensure that the band is set to 2.4GHz, as the ESP32 cannot use 5GHz networks.


# Step 1: Python
We'll begin by writing a small program to send keyboard commands to your robot. For this, you'll need to install a python module called pygame- we can use this to parse keyboard commands, and it also allows for simple GUIs. This should work with any recent version of python.

If you already have python and pip installed, simply type pip install pygame into command prompt. To verify that it has installed properly, you can type py.exe to run the interpreter, and then import pygame. An error will be thrown if it has not installed properly.

If you're having issues with this method, you can try a few other options [here](https://www.pygame.org/wiki/GettingStarted).

If you don't have python, you can get it from the microsoft store or [here](https://www.python.org/downloads/release/python-3100/).

If you have multiple versions of python, make sure you are running and installing on the same version of python. Call py.exe -(version number here) to run a specific version of python- the exact version shouldn't matter too much here though, since we're only using very basic functionality.

Using either your preferred IDE or notepad, copy in this code:

```python
import socket
import time
import pygame
import sys
import array

def constrain(val, min_val, max_val):
    return min(max_val, max(min_val, val))

pygame.init()
display = pygame.display.set_mode((300,300))

UDP_IP = "192.168.137.133"
UDP_PORT = 100

class DATA:
    left = 0
    right = 0
    ch1 = 90
    ch2 = 0
    ch3 = 0
    ch4 = 0
    ch5 = 0
    ch6 = 0


sock = socket.socket(socket.AF_INET, # Internet 
                     socket.SOCK_DGRAM) # UDP
keys = pygame.key.get_pressed()

ArrDATA = array.array('b',[DATA.left, DATA.right, DATA.ch1, DATA.ch2, DATA.ch3, DATA.ch4, DATA.ch5, DATA.ch6])        
sock.sendto(ArrDATA, (UDP_IP, UDP_PORT))
lastTime = 0
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    
    keysPrev = keys
    keys = pygame.key.get_pressed() #The PyGame keys function is deranged, I'm sorry about the code that follows. Why can't it just return a string!

    if (keys != keysPrev):
        print("changed")
        DATA.left = 0
        DATA.right = 0
        keyPressed = False

        if keys[pygame.K_w]:
            DATA.left += 127
            DATA.right += 127
            keyPressed = True

        if keys[pygame.K_s]:
            DATA.left -= 127
            DATA.right -= 127
            keyPressed = True

        if keys[pygame.K_d]:
            DATA.left += 100
            DATA.right -= 100
            keyPressed = True

        if keys[pygame.K_a]:
            DATA.left -= 100
            DATA.right += 100
            keyPressed = True

        if keys[pygame.K_q]:
            DATA.ch1 = 70
            keyPressed = True

        if keys[pygame.K_e]:
            DATA.ch1 = 110
            keyPressed = True

        if keys[pygame.K_q]:
            #Add some servo stuff in empty channels
            keyPressed = True

        if keys[pygame.K_e]:
            #Add some servo stuff in empty channels
            keyPressed = True

        if not(keyPressed):
            DATA.left = 0
            DATA.right = 0
        DATA.left = constrain(DATA.left, -127, 127)
        DATA.right = constrain(DATA.right, -127, 127)
        

        
    if (time.time()-lastTime>0.1 or keys != keysPrev):
        lastTime=time.time()
        ArrDATA = array.array('b',[DATA.left, DATA.right, DATA.ch1, DATA.ch2, DATA.ch3, DATA.ch4, DATA.ch5, DATA.ch6])
        sock.sendto(ArrDATA, (UDP_IP, UDP_PORT))
```

If you're not using an IDE, you can run this code by saving it as a .py file, then using command prompt to navigate to the folder you saved it in and then calling py.exe filename.py in the command prompt. 

A faster way to get to the folder is to find the file in file explorer and type "cmd" in the bar at the top. A command prompt should then open already in the correct location.

![image](https://github.com/user-attachments/assets/34f744d3-b3f1-41eb-8cf4-f8bd119fc9b8)

When you run the file, a window should pop up- you'll need to click into this window to start sending keypresses to the Arduino.

# Step 2: It's like wires... without wires
In this program, we'll be splitting our code into multiple pages in order to streamline it. Download the .zip file and unzip it. We'll be modifying this script from here on out.

<a href="./Sumo2024Minimal.zip" download>Download link: Sumo2024Minimal.zip</a>

The first thing you need to change is adding your team name as the SSID, and choosing a password. Make sure these match what you set up on your PC or phone hotspot.

If you are running your hotspot on an android phone, you may need to change the gateway. Near the top, comment out the line: 
```cpp
IPAddress gateway(192, 168, 1, 1);
```
And uncomment 
```cpp
IPAddress gateway(192, 168, 43, 1);
```

You can then run the code. It should print "connecting" repeatedly, until it manages to connect to the network.

Now, run the python script from before. You should see a line of numbers being printed and when the WASDQE keys are pressed, the numbers will change.

# Step 3: Wiring it up
To get your robot working, wire it up as so:

### Power

From | To
--- | --- 
Battery positive terminal | Red power rail (on the side of the breadboard)
Battery negative terminal | Blue power rail
VIN ESP32 pin | Red power rail
GND ESP32 pin | Blue power rail
Motor driver + pin | Red power rail
Motor driver - pin | Blue power rail
Servo motor red wire | Red power rail
Servo motor black wire | Blue power rail
Left motor wires | Motor A
Right motor wires | Motor B

### Signals

From | To
--- | --- 
Servo yellow signal wire | ESP32 pin 7
Motor driver IN1 | 8
Motor driver IN2 | 9
Motor driver IN3 | 10
Motor driver IN4 | 11

If you find the motors spin the wrong way in testing, simply swap the wires connecting the motor driver to the motor.

# Step 4: Moving
packetBuffer is an array with the 8 values from the python code ```(DATA.left, DATA.right, DATA.ch1, DATA.ch2, DATA.ch3, DATA.ch4, DATA.ch5, DATA.ch6)``` stored in order. We're using the first two values to dictate motor speed for left and right, as well as channel 1 to set the servo position. If you assign values to the other channels in the python code, they should show up in ```packetBuffer``` on the ESP32. 

We currently aren't doing anything with the values from packetBuffer aside from putting them in to these variables:
```cpp
  int speedLeft = (int8_t)packetBuffer[0]; 
  int speedRight = (int8_t)packetBuffer[1];
  int servoPos = packetBuffer[2];
```
In order to actually send them to our actuators, you'll need to use the objects we created at the top of the code: ```SimpleMotor left```, ```SimpleMotor right``` and ```Servo servo```. Have a look in the Actuators.h file to find out what the methods are used to control the actuators, and what values they expect. 

<details> <summary> Need a hint?

</summary>

Call these methods like so:

```cpp left.methodName(value) ```

But replacing methodName and value with the correct method and variable respectively, with one each for the three actuators. Put these just before delay(5) at the end of the main loop.

</details>



# Step 5: Delemonization
Currently, if the WiFi connection is lost, your robot will sit there like... a lemon. Generally you will then lose.

To make this not happen, we can check if we are connected like so:

```cpp
WiFi.status() != WL_CONNECTED
```

We can now simply call 

```cpp
WiFi.begin(ssid, password);
```

To start connecting again. Put this in a while loop, in order to keep trying to reconnect to the network until you succeed. You can test if your implementation is working by simply turning off the access point, then turning it on again. If the robot resumes control, your solution is functional.

Remember to add a delay of 100 to the loop, so it doesn't spam connection attempts.

<details> <summary> Need a hint?

</summary>
The correct structure for the while loop is this: 

```cpp
  while (WiFi.status() != WL_CONNECTED) {  //If we're disconnected
  
    Serial.println("reconnecting");
    delay(100);
  }
```
Now add the WiFi.begin() the same way it was added in ```setup()```
  

</details>

I was also going to suggest using the indicator light here to show when a disconnection occurs, but adding an easy kill indicator for your opponents is probably not the most "Sun Tzu Art of War" design choice.

# Conclusion

Well, you've now mostly completed Sumobots- but the real work has only just begun.

From here, you'll need to upgrade your robot into something to strike fear into your enemies:

![image](https://github.com/user-attachments/assets/5d61ef0d-0e12-49b8-9359-e12f654854b6)

Sadly grainy filters and dramatic shadows will not be available in the arena, so you'll need to resort to engineering.


There will be one more catch-up workshop where you can fill in anything you missed or ask to committee for help with your robot. We'll also be opening G49 to anyone with hand tool training in the afternoons of the week leading up to competition (more details soon to follow), where we'll have various hand tools and soldering stations available. Members of the technical team will also be there to assist you with any questions and final preparation.

## Good Luck!
