# ARDUINO INFRARED PROXIMITY SENSOR PROJECT


## **DIY: Arduino Infrared Proximity Sensor Project**

Looking to dive into DIY electronics projects? Look no further than this Arduino Infrared Proximity Sensor project. With just a few components and some basic code, you can create a versatile sensor that has applications in reverse sensors, robots, touch-less switches, and more.

### **Hardware Setup**

The hardware setup for this project couldn't be simpler. You'll need an Arduino board (such as the Keyestudio Uno), a Sharp Infrared Range Sensor (2Y0A21), three jumper wires, and a USB data cable. Connect the positive pin of the sensor to 5V on the Arduino, the ground pin to GND, and the data pin to digital pin 1. That's it - your hardware setup is complete!


| ![board](/images/proj1.jpg) | ![schematic](/images/proj12.jpg) |
|:--------------------------:|:-------------------------------:|
|            Board           |            Schematic            |


<!-- ![board](/images/proj1.jpg)
![schematic](/images/proj12.jpg) -->
### **About the Code**

While the code for this project may seem short, it's worth understanding how it works. The code starts by defining the pin number (digital pin 1) for the IR sensor. In the void setup section, serial communication is initialized at a baud rate of 9600. Moving on to the void loop section, the code calculates the distance measured by the sensor using a series of mathematical calculations.

```arduino
int IRpin = 1;                                    
void setup() {
  Serial.begin(9600);                             
}
void loop() {
  float volts = analogRead(IRpin)*0.0048828125;   
  float distance = 65*pow(volts, -1.10);   
  Serial.print(distance);     
  Serial.println(" cm");
  delay(100);                                     
}
```
### **Explanation of Code**

The code calculates the voltage reading from the sensor and then converts it to distance using a formula that incorporates the sensor's characteristics. It then prints the calculated distance to the serial monitor, along with the unit of measurement (cm). The loop repeats every 100 milliseconds, providing real-time distance data.

### **Conclusion**

With just a few components and a bit of code, you can create a useful Arduino Infrared Proximity Sensor that has a wide range of applications. Whether you're a beginner looking to dip your toes into DIY electronics or an experienced hobbyist seeking a quick and easy project, this Arduino project is sure to delight. So gather your components, follow the simple instructions, and start sensing the world around you in no time!

### **References:**
{{< admonition info "Sources" >}}
1. https://www.electorials.com/project-006-arduino-infrared-proximity-proximity-sensor-project.html
2. https://global.sharp/products/device/lineup/data/pdf/datasheet/gp2y0a21yk_e.pdf
3. https://circuitdigest.com/microcontroller-projects/interfacing-ir-sensor-module-with-arduino
{{< /admonition >}}



