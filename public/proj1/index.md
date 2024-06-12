# DIY: Arduino DHT Humidity Sensor Project


## **DIY: Arduino DHT Humidity Sensor Project**

If you're interested in monitoring temperature and humidity, this Arduino project using the DHT22 sensor is perfect for you. Whether you're building a weather station, a clock, or a measurement device for a computer or car, this project will guide you through the setup and code needed to get accurate readings.

### **Relative Humidity** 

The relative humidity (RH) is a measure of the amount of moisture in the air compared to the maximum amount of moisture the air can hold at a specific temperature. It is expressed as a percentage.

The formula to calculate relative humidity is:

$$RH = \left(\frac{{\text{actual vapor pressure}}}{{\text{saturation vapor pressure}}}\right) \times 100\%$$

where:
- $RH$: Relative Humidity (in percentage)
- Actual vapor pressure: The pressure exerted by the water vapor present in the air.
- Saturation vapor pressure: The maximum pressure exerted by water vapor at a given temperature. It represents the point where the air is saturated with moisture.


### **Components Needed**

1. Arduino (Keyestudio Uno used in this example)
2. DHT22/AM2302 Humidity and Temperature Sensor
3. 3 Jumper Wires
4. 10KΩ resistor
5. Breadboard
6. USB Data Cable (depends on the Arduino model)


<!-- <div style="display: flex; justify-content: space-around;">
  <div>
    <img src="/images/proj3.jpg" alt="board" style="width: 75%;">
  </div>
  <div>
    <img src="/images/proj31.jpg" alt="schematic" style="width: 100%;">
  </div>
</div> -->


| ![board](/images/proj3.jpg) | ![schematic](/images/proj31.jpg) |
|:---------------------------:|:--------------------------------:|
|            Board            |            Schematic             |


### **Building the Circuit**

The circuit is simple and quick to assemble on a breadboard. Here are the steps:

1. **Remove Power**: Ensure the Arduino is powered off before starting.
2. **Insert Sensor**: Fit the DHT22 sensor vertically across four separate rows on the breadboard.
3. **Connect Pins**:
    - Pin 1 (VCC) to 5V on the Arduino
    - Pin 2 (DATA) to digital pin 2 on the Arduino
    - Pin 4 (GND) to Ground on the Arduino
4. **Add Resistor**: Place a 10KΩ resistor between Pin 1 (VCC) and Pin 2 (DATA) on the sensor.

That's all for the hardware setup!

### **The Code**

We'll use the DHTtester example from Adafruit's DHT sensor library, which supports DHT11, DHT21, and DHT22 sensors. You can download the library from [Adafruit's GitHub page](https://github.com/adafruit/DHT-sensor-library). Once downloaded, open the Arduino IDE and use the following code:

```arduino
// Example testing sketch for various DHT humidity/temperature sensors
#include "DHT.h"
#define DHTPIN 2     // what digital pin we're connected to

// Uncomment whatever type you're using!

//#define DHTTYPE DHT11   // DHT 11

//#define DHTTYPE DHT22   // DHT 22  (AM2302), AM2321

//#define DHTTYPE DHT21   // DHT 21 (AM2301)

// Connect pin 1 (on the left) of the sensor to +5V

// NOTE: If using a board with 3.3V logic like an Arduino Due connect pin 1
// to 3.3V instead of 5V!

// Connect pin 2 of the sensor to whatever your DHTPIN is
// Connect pin 4 (on the right) of the sensor to GROUND
// Connect a 10K resistor from pin 2 (data) to pin 1 (power) of the sensor

// Initialize DHT sensor.

// Note that older versions of this library took an optional third parameter to
// tweak the timings for faster processors.  This parameter is no longer needed
// as the current DHT reading algorithm adjusts itself to work on faster procs.

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("DHTxx test!");
  dht.begin();
}

void loop() {
  // Wait a few seconds between measurements.
  delay(2000);
  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float t = dht.readTemperature();
  // Read temperature as Fahrenheit (isFahrenheit = true)
  float f = dht.readTemperature(true);
  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  
  // Compute heat index in Fahrenheit (the default)
  float hif = dht.computeHeatIndex(f, h);
  // Compute heat index in Celsius (isFahreheit = false)
  float hic = dht.computeHeatIndex(t, h, false);
  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print(" *C ");
  Serial.print(f);
  Serial.print(" *F\t");
  Serial.print("    Heat index: ");
  Serial.print(hic);
  Serial.print(" *C ");
  Serial.print(hif);
  Serial.println(" *F");
}
```

### **Code Explanation**

1. **Library Import**: The code begins by including the DHT sensor library.
2. **Define Pins**: It defines the data pin and the type of DHT sensor being used.
3. **Setup**: In the `setup` function, the code initializes serial communication at 9600 baud rate and starts the DHT sensor.
4. **Loop**: The `loop` function runs continuously, waiting for 2 seconds between each reading. It reads humidity and temperature from the sensor, calculates the heat index, and prints the results to the serial monitor.

### **Conclusion**

You've now set up a simple yet effective humidity and temperature sensor using an Arduino and a DHT22 sensor. This project is a great starting point for creating more complex systems like weather stations or environmental monitors. With minimal components and straightforward code, you'll have accurate readings displayed on your serial monitor in no time. Happy tinkering!


### **References:**
{{< admonition info "Sources" >}}
1. https://www.electorials.com/project-005-arduino-dht-humidity-sensor-project.html
2. https://www.mouser.com/datasheet/2/758/DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf
3. https://www.circuitbasics.com/how-to-set-up-the-dht11-humidity-sensor-on-an-arduino/
{{< /admonition >}}
