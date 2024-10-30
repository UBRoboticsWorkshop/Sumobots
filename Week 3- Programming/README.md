# Programming

According to a poll of whoever was in G49 when I wrote this, 66% of people agree robots are better when you can tell them what to do. The people have spoken so, today, we'll be doing that. 

## The Sumocontroller
The microcontroller you'll be using today is the ESP32-S3-MINI-N4R2, which I'll call the ESP32 from here. Odds are, you probably already own one- they're very often used for handling the internet connection of devices, so you'll find them in a lot of consumer goods. You can't really wire up an ESP32 by itself (or at least not easily), so for projects like this they're mounted to a development board- a PCB which has all the support circuitry needed.

Last year, some members had issues with the off-the-shelf ESP32 boards we were using- they were too wide and you could only connect pins on one side of the breadboard, drivers needed to be installed which didn't work on some computers, some pins were exposed that could mess with the storage and the regulators were somewhat unstable making the ESP32 liable to reset during certain events.

This year, we're using our brand-new Sumocontroller, which features an updated version of the ESP32S3. Not only is it both more powerful and power efficient, it should work all the way down to 3.3v due to the upgraded power system. This one will fit your breadboard without cutting it in two, only features pins which are safe to use and shouldn't need any drivers to work on Mac or Windows. Most people's robots last year had designs which made it hard to reach the USB-C port, so we've made it vertical for easy access.

We've even given you a super bright RGB LED, so you can choose to set it either to our patent pending UBRobotics blue (0x20, 0xe7, 0xf0) or off (0x00, 0x00, 0x00).

![IMG_3250](https://github.com/user-attachments/assets/b4f6f4e1-6ae4-431e-b409-10a917c995d7)


## The Arduino IDE
The ESP32 can be programmed in various IDEs, but the easiest to get started in is the Arduino IDE 2.0. You can download it [here](https://www.arduino.cc/en/software), or if you're working on a university computer you'll have it pre-installed. Next, you'll need to add the board information for the ESP32:
1. Go to the file drop down, and click preferences

![image](https://github.com/user-attachments/assets/5393b6ac-9a80-4f30-8dd6-5c5f65c47ce4)


2. At the bottom of the page, paste this into the Additional Board Manager URLs field

```
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
```

![image](https://github.com/user-attachments/assets/3a5da960-709a-4127-8f7c-3d939aef405a)

3. Open the boards manager tab, highlighted here, and install ESP32. You may need to use the search bar to find it quickly.

![image](https://github.com/user-attachments/assets/f88dcf46-16d6-489b-90b2-e6ac5a24b617)

## Step 1: Connect the ESP32
The ESP32 uses USB-C to connect to your computer's USB ports, and there should be a chime when you plug it in. The ESP32 will at first be in an invalid state and will keep disconnecting and reconnecting from your computer. The following should get it working:

### Getting the ESP32 out of a bad spot
It's unlikely, but possible, that the code on the ESP32 may prevent it from connecting to your computer. When this happens, hold down the boot button while you connect power to the chip (or press reset). The ESP32 should now be solidly connected to your computer, ready to recieve code

<details> <summary> Still not working?

</summary>

There are a few other things that may cause issues here. Here are some possible fixes to try:
1. If using a USB Hub, try directly connecting to your device
2. Try using USB-C to USB-C if you have a cable
3. Try a different USB port- sometimes the CTL computers have issues with connection on the screen USB ports

</details>

## Step 2: The first program
Make sure the box in the top left reads:
![image](https://github.com/user-attachments/assets/20f59edd-34bb-446c-8862-15929d3fdb05)

If it doesn't, click select other board and port. Search for ESP32S3 dev module, and set your port to that.
Delete all the code in the editor, and paste this in:

```cpp
void setup() {
  Serial.begin(115200);

}

void loop() {
  Serial.println("Hi");
  delay(250);
}
```

If all is working, you should have the ESP32 printing "Hi" repeatedly, which you can read by clicking the ![image](https://github.com/user-attachments/assets/e63125fa-ee49-4445-85c4-7b7f921f98fe) Serial Monitor button in the top left corner.


<details> <summary> Not printing anything?

</summary>

Make sure that the settings under tools are as follows:

![image](https://github.com/user-attachments/assets/bb5acea3-e6d0-4730-8dc3-f9183cb34db7)

Most importantly, "USB CDC on boot" needs to be enabled.
</details>

## Step 3: Using the onboard LED
This one is really important.
Upload this code:

```cpp
const int brightness = 27;
const int LED_PIN = 48;
void setup() {
}

float i;
void loop() {
  rgbLedWrite(LED_PIN, (brightness+brightness*sin(i)), brightness+brightness*sin(i+2*PI/3), brightness+brightness*sin(i+4*PI/3));
  delay(10);
  i+=0.1;
}
```

You can use rgbLedWrite(48, RED, GREEN, BLUE) to set the colour of your LED, 48 being the pin that the LED is connected to. RED/GREEN/BLUE are respective brightnesses from 0-255.

## Using GPIO

In our last workshop, we showed you how to use the VirtualBench to probe electrical signals. This will soon be your best friend when it comes to troubleshooting.

Open up the VirtualBench and plug in a probe, before uploading this code:

## Step 4: Turning Pins On and Off

```cpp
void setup() {
  pinMode(14, OUTPUT);
}

void loop() {
  digitalWrite(14, HIGH);
  delay(500);
  digitalWrite(14, LOW);
  delay(500);
}
```

## Using a Probe

Now, attach the probe to pin 10. Modify the code so that pin 10 is the one being turned on and off. You should see that the voltage jumps between 0v and 3v3, every half second. You can also try changing the number to send the signal to different pins. 

<details> <summary> I'm pretty sure that I have modified the code correctly, but the scope isn't moving?

</summary>

You may need to use the ground clip here depending on how it's wired up. You can either add a jumper wire to the ground pin and connect this to the little alligator clip, or just clip it onto the metal part of the USB-C connector- in any good design, this should be connected to ground. Be really careful that it doesn't slip off and short out the controller- if you can't get a firm grip, best to use the extra wire.

</details>

In this sketch, pinMode is used to indicate that a pin will be used to output a signal. The GPIO pins on the microcontroller can both read and emit signals, so we need to define how we're using them. Once this is set,
digitalWrite is used to set the value of a pin. You can use HIGH and LOW, or TRUE and FALSE. Due to how types are handled, you can also use 0 and 1 or any number higher than 1.

## Pulse Width Modulation 
The ESP32 can provide about 40mA per pin at 3v3. There are two problems with this when you try to build a robot:

#### 40mA at 3v3 is not much power at all, and a motor will pull too much current damaging the pin you connect it to
#### Having a motor fully on or fully off is very clunky, we need to be able to vary the speed

These can be fixed by using PWM and an H-Bridge. You should already have seen this in our first workshop, so we'll show you how to use PWM with a microcontroller.

Connect pin 10 to in1, and pin 11 to in2. Wire plus and minus on the motor driver to the positive and negative rails respectively, and connect the rails up to the VirtualBench power supply. Lastly, connect the motor to the two pins marked motorA.

#### Remember to use +6V to connect to the board!

![image](https://github.com/user-attachments/assets/cff28fab-bc36-44bf-b572-24196fd38c08)

## Step 5: Making a Motor Move
```cpp
const int frequency = 1000;
const int resolution = 10;
const int outputPin = 10;

void setup() {
  Serial.begin(115200);
  ledcAttach(outputPin, frequency, resolution);
}

void loop() {
  for (int i = 0; i <= 1000; i += 100){
    ledcWrite(outputPin, i);
    Serial.println(i);
    delay(400);
  }
}
```

You'll probably notice that the motor doesn't spin at values such as 100, 200. This is because we aren't controlling speed directly, we're controlling average voltage across the motor. Every motor has a "breakover voltage", or minimum voltage to start spinning. Try changing the resolution and frequency- which of these has an effect on how finely you can control the motor? remember that when you change the resolution, the max value of a channel will change- here 2^10 = 1024 is fully on, while a resolution of 8 would have 2^8 = 255 as fully on.

Try probing both the pin 10 on the ESP32, and the motor's terminals- you can use this to make sure both that the ESP32 is generating the correct signal, and that the H-Bridge is properly driving the motor.

In semester 2, we'll be looking at much more advanced types of motor- these can provide measurements of their own speed, allowing us to command them to run at an exact speed.

## Driving a Servo
While PWM can be used to approximate an analog voltage, it can also be used as a simple communication protocol. Many more advanced systems use serial communications such as SPI, I2C and UART (more on these next semester); PWM is still used due to how simple it is to implement.

For a servo motor, we'll send out a pulse of 1-2 milliseconds 50 times a second. The motor will interpret the length of the pulse as an angle- 1ms will be 0 degrees, 1.5ms will be 90, 2ms will be 180 and so on (in practice the servos often have their actual limits at 0.5-2.5ms- you'll want to experiment with this to get the desired range of motion).

Connect the orange signal pin of the servo to pin 15 on the Sumocontroller, red voltage pin to the positive rail and brown ground pin to the ground rail. 

Connect Vin and GND on the Sumocontroller to the positive and ground rails respectively. 

Lastly, connect the positive and negative rail to the VirtualBench power supply (red and black wires going off-camera in the photo below).

![image](https://github.com/user-attachments/assets/a644199d-735a-4363-970e-002eaa629649)

The code below should make the servo move between two positions:
## Step 6: Making the Servo Move
```cpp
/*
  The datasheet for these servos recommends 50Hz signal

  Period of waveform:
  1/50 = 20ms

  minimum pulse = 1000us
  max pulse = 2000us
  So max duty cycle is 10%
  Min duty cycle is 5%

  We've picked a 14 bit timer, so 2^14= 16384
  So max signal is 0.1*16384 = 1638
  Min signal is 0.05*16384 = 820

  This gives us ~800 steps- in practice, far more accuracy than the servo can deliver

  However, these servo motor makers just keep on lying to us- the min and max pulses are completely wrong. I don't know why everyone says they're 1-2ms.
  By tweaking the min and max values, you can get a whole 180 degrees out of these. This math will be left to you.
*/

const int frequency = 50;
//const int minPulse = 820;
//const int maxPulse = 1638;
const int servoPin1 = 15;
const int resolution = 14;

int angleDuty;
int angle;

void setup() {
    pinMode(servoPin1, OUTPUT);
    ledcAttach(servoPin1, frequency, resolution);
}

void loop() {
  angleDuty = 820; //The map function scales the input variable from the first range to the second
  ledcWrite(servoPin1, angleDuty);
  delay(1000);
  
  angleDuty = 1638;
  ledcWrite(servoPin1, angleDuty);
  delay(1000);
}

```

## OOP
Now, whipping out a calculator to know to set the duty to 157.567 in order to go to 30.986 degrees is not very practical. On top of that, having multiple servos and motors determined by channel numbers can get convoluted fast- is channel 7 your left wheel or your grabber?

This is where Object Oriented Programming (OOP) can help. By creating a class, each motor or servo can have a set of values and functions associated with it- setSpeed(), frequency, goToAngle() and so on.

 ## Step 7: Using OOP to drive a servo With Style
 
Below I've provided you with the skeleton of a class, and some code snippets to perform each function. Combine these to make the servo move- you shouldn't need to alter setup or loop.

There's also one difference between the code and wiring diagram for you to find before the servo will move- look at how the class configures the output or use a probe to find it.

```cpp

class Servo{

  public:
  Servo(int _pin, int _minPulseMicros, int _maxPulseMicros){

  }

  Servo(int _pin){

  }

  void writeAngle(int _angle){

  }

};

Servo newServo(13, 500, 2500);

void setup() {
  Serial.begin(115200);

}

void loop() {
  newServo.writeAngle(0);
  delay(500);
  newServo.writeAngle(180);
  delay(500);
}
```

Angle setting code

```cpp
    int angleDuty = map(_angle, 0,180, minPulse, maxPulse); //The map function scales the input variable from the first range to the second
    ledcWrite(pin, angleDuty);
```

local variables

```cpp
  const int frequency = 50;
  const int resolution = 14;
  int minPulse;
  int maxPulse;
  int pin;
```

Startup calculations with default 1-2ms pulses:

```cpp
    int periodus = 1000000/50; //1 sec = 1 000 000 micros
    int minPulse = float(1<<resolution)*(float(1000)/float(periodus));
    int maxPulse = float(1<<resolution)*(float(2000)/float(periodus));
    pin = _pin;
    pinMode(_pin, OUTPUT);
    ledcAttach(_pin, frequency, resolution);
```

Startup calculations with custom pulses in microseconds:

```cpp
    int periodus = 1000000/50; //1 sec = 1 000 000 micros
    minPulse = float(1<<resolution)*(float(_minPulseMicros)/float(periodus));
    maxPulse = float(1<<resolution)*(float(_maxPulseMicros)/float(periodus));
    pin = _pin;
    pinMode(_pin, OUTPUT);
    ledcAttach(_pin, frequency, resolution);
```

# Finished
Next week is a catchup week- don't worry if you can't make this session, since many of you may be away in that week. Although there won't be any new content, we will be handing out some parts that you can use to assemble your prototype robot alongside videos showing you how. Our Communications workshop will also provide you enough time to do so, so don't worry if you aren't in Birmingham next week. The parts we hand out are also very weak and underbuilt, so you'll really want to upgrade them- work on your Fusion 360 skills and get your PPMS accounts sorted!

