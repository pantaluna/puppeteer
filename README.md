# ESP32 ESP-IDF MJD AM2320 meteo sensor component
This is an ESP-IDF component for the ESP32 chip.

## Highlights
- Sensor AM2320 of Aosong.
- 1-Wire custom protocol.
- Using the ESP-IDF RMT driver.

## Data Sheet
C:\myiot\doc\Aosong AM2320 Temperature And Humidity Sensor\

<https://akizukidenshi.com/download/ds/aosong/AM2320.pdf>

## WIRING INSTRUCTIONS
### MCU
a. MCU Adafruit HUZZAH32
- UART Serial COM3
- Pin #13 = Blue LED on the PCB
- Pin #14 = AM2320 sensor data pin (Huzzah32 GPIO#14: bottomright -2)

b. MCU Lolin32 Lite
- UART Serial COM5
- Pin #22 = Blue LED on the PCB
- Pin #19 = AM2320 sensor data pin (Lolin32lite GPIO#13: topright +2)

### Sensor AM2320 for the custom 1-WIRE protocol (not the I2C protocol)
- Connect pin 1 (VCC) of the sensor to the MCU pin VCC 3V.
- Connect pin 2 (SDA) of the sensor to the MCU pin DATA (whatever pin you selected above).
- Connect pin 3 (GND) of the sensor to the MCU pin GND.
- Connect pin 4 (SCL) of the sensor to the MCU pin GND. @important This signals to the sensor to use the 1-WIRE protocol, and not the I2C protocol).
- Connect a 5K PULL-UP resistor from the sensor pin 2 (SDA) of the sensor to the MCU pin VCC 3.3V  \
  @important You will often get checksum errors without this pullup resistor.


- OPTIONAL: connect a 100nF capacitor between pin VDD and pin GND of each sensor for power filtering.  \  
  @doc <http://www.williamson-labs.com/480_byp.htm  \>  
  @purpose Restore this nearly ideal power supply--zero ohms output impedance.

## Aosong AM2320 known ISSUES
*NONE

## Aosong AM2320 sensor FAQ
- OK 3.3V
- Burden: an external pull-up resistor is required.
- Metrics: temperature (unit Celsius in float), humidity (unit Percentage in float).
- Supports temperature range -40..+80 degrees Celsius (the DHT11 sensor does no negative degrees Celsius).
- Uses a custom 1-Wire protocol. The I2C protocol of the device is a custom one (the standard ESP32 I2C driver does NOT work!).
- The startup time of the sensor after power-on is 1 second.
- Recommended minimum reading time interval: 1x / minute.
