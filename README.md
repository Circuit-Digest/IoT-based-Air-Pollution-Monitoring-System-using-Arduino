# IoT Air Pollution Monitoring System using Arduino

![IoT Air Pollution Monitoring System](https://circuitdigest.com/sites/default/files/projectimage_mic/Iot-air-quality-monitoring-system-using-arduino.jpg)

## Project Overview

This project develops an IoT-based Air Pollution Monitoring System that continuously monitors air quality over a web server using the internet and triggers an alarm when air quality levels drop below safe thresholds. The system detects harmful gases like CO2, smoke, alcohol, benzene, and NH3, displaying air quality measurements in PPM (Parts Per Million) on both an LCD display and a web interface for remote monitoring.

**Project Source:** [IoT Air Pollution Monitoring using Arduino - Circuit Digest](https://circuitdigest.com/microcontroller-projects/iot-air-pollution-monitoring-using-arduino)
**Projects:**[Arduino Projects](https://circuitdigest.com/arduino-projects)

## Features

- **Real-time Air Quality Monitoring**: Continuously monitors air quality in PPM
- **Web-based Remote Access**: Monitor pollution levels from anywhere using a computer or mobile device
- **Multi-level Alert System**: 
  - Fresh Air (≤1000 PPM)
  - Poor Air - Open Windows (1000-2000 PPM) 
  - Danger! Move to Fresh Air (≥2000 PPM)
- **Audio Alert**: Buzzer alarm when pollution exceeds safe levels
- **LCD Display**: Local display of current air quality readings
- **IoT Connectivity**: ESP8266 WiFi module for internet connectivity

## Components Required

| Component | Quantity | Description |
|-----------|----------|-------------|
| MQ135 Gas Sensor | 1 | Air quality sensor for detecting harmful gases |
| Arduino Uno | 1 | Main microcontroller |
| ESP8266 WiFi Module | 1 | Internet connectivity |
| [**16x2 LCD Display**](https://circuitdigest.com/microcontroller-projects/interfacing-16x2-lcd-with-arduino) | 1 | Local display unit |
| Buzzer | 1 | Audio alarm |
| 10K Potentiometer | 1 | LCD contrast control |
| 1K Ohm Resistors | 2 | Voltage divider for ESP8266 |
| 220 Ohm Resistor | 1 | LCD backlight current limiting |
| Breadboard | 1 | Circuit prototyping |
| Jumper Wires | As needed | Connections |

## Circuit Connections

### ESP8266 to Arduino
- **VCC & CH_PD**: 3.3V pin of Arduino
- **TX**: Pin 10 of Arduino
- **RX**: Pin 9 of Arduino (through voltage divider using 1K resistors)
- **GND**: Ground

### MQ135 Gas Sensor to Arduino
- **VCC**: 5V
- **GND**: Ground
- **Analog Pin**: A0

### LCD to Arduino (16x2)
- **Pin 1 (VSS)**: Ground
- **Pin 2 (VDD)**: 5V
- **Pin 3 (V0)**: Middle pin of 10K potentiometer
- **Pin 4 (RS)**: Pin 12
- **Pin 5 (Enable)**: Pin 11
- **Pin 6 (RW)**: Ground
- **Pin 11 (D4)**: Pin 5
- **Pin 12 (D5)**: Pin 4
- **Pin 13 (D6)**: Pin 3
- **Pin 14 (D7)**: Pin 2
- **Pin 15 (A)**: 5V through 220Ω resistor
- **Pin 16 (K)**: Ground

### Buzzer
- **Positive**: Pin 8 of Arduino
- **Negative**: Ground

## Software Requirements

### Libraries Needed
1. **MQ135 Library**: Download from [GitHub - MQ135 Library](https://github.com/GeorgK/MQ135)
2. **SoftwareSerial**: Built-in Arduino library
3. **LiquidCrystal**: Built-in Arduino library

### Installation Steps
1. Download and install the MQ135 library in your Arduino IDE
2. Copy the provided code to Arduino IDE
3. Before uploading, calibrate the MQ135 sensor (see calibration section)

## Sensor Calibration

### Step 1: Get RZERO Value
Upload this calibration code and let it run for 12-24 hours:

```cpp
#include "MQ135.h"

void setup() {
  Serial.begin(9600);
}

void loop() {
  MQ135 gasSensor = MQ135(A0);
  float rzero = gasSensor.getRZero();
  Serial.println(rzero);
  delay(1000);
}
```

### Step 2: Update Library
After obtaining the RZERO value, update the MQ135.h library file:
```cpp
#define RZERO [Your_RZERO_Value]  // Replace with your calibrated value
```

## Air Quality Levels

| PPM Range | Status | Action | Display Message |
|-----------|--------|--------|-----------------|
| ≤ 1000 | Safe | None | "Fresh Air" |
| 1001-2000 | Poor | Buzzer ON | "Poor Air, Open Windows" |
| > 2000 | Dangerous | Buzzer ON | "Danger! Move to Fresh Air" |

## How It Works

1. **Gas Detection**: MQ135 sensor detects harmful gases and outputs voltage levels
2. **Data Processing**: Arduino converts sensor readings to PPM using the MQ135 library
3. **Local Display**: LCD shows current air quality readings and status
4. **Web Interface**: ESP8266 creates a web server accessible via IP address
5. **Alert System**: Buzzer activates when pollution exceeds safe thresholds
6. **Remote Monitoring**: Users can access real-time data through web browser

## Web Interface Access

1. Upload the code to Arduino
2. Open Serial Monitor to get the IP address (typically 192.168.4.1)
3. Connect your device to the ESP8266's WiFi network
4. Enter the IP address in your web browser
5. Refresh the page to see updated air quality readings

## Usage Instructions

1. **Assembly**: Connect all components according to the circuit diagram
2. **Calibration**: Calibrate the MQ135 sensor as described above
3. **Upload Code**: Upload the complete project code to Arduino
4. **Network Setup**: Connect to ESP8266's WiFi network
5. **Monitor**: Access the web interface using the provided IP address

## Troubleshooting

### Common Issues and Solutions

**ESP8266 Connection Problems:**
- Check voltage levels (ESP8266 requires 3.3V)
- Verify voltage divider circuit for RX pin
- Ensure correct baud rate (usually 115200)

**Sensor Calibration Issues:**
- Allow 12-24 hours for proper calibration
- Ensure clean air environment during calibration
- Update RZERO value in MQ135.h library file

**Web Interface Not Loading:**
- Verify ESP8266 WiFi connection
- Check IP address in Serial Monitor
- Ensure device is connected to ESP8266's network

## Code Structure

The main code includes:
- **Sensor initialization and calibration**
- **WiFi setup and web server creation**
- **HTML webpage generation**
- **LCD display management**
- **Alert system control**
- **Data transmission functions**

## Applications

- **Home Air Quality Monitoring**
- **Office Environment Control**
- **Industrial Safety Systems**
- **Educational Projects**
- **Environmental Research**

## Future Enhancements

- **SMS/Email Notifications**: Add GSM module for remote alerts
- **Data Logging**: Store historical air quality data
- **Multiple Sensor Support**: Add temperature, humidity sensors
- **Mobile App**: Develop dedicated mobile application
- **Cloud Integration**: Upload data to cloud platforms

## Safety Considerations

- Ensure proper ventilation when testing with actual pollutants
- Use the system as a monitoring tool, not a replacement for professional air quality equipment
- Regular calibration recommended for accurate readings

## Contributing

Feel free to contribute to this project by:
- Reporting bugs or issues
- Suggesting improvements
- Adding new features
- Sharing your implementation experiences

## License

This project is based on the tutorial from Circuit Digest. I'd like you to please refer to their website for licensing information.

---

**Project Tutorial Source**: [Circuit Digest - IoT Air Pollution Monitoring](https://circuitdigest.com/microcontroller-projects/iot-air-pollution-monitoring-using-arduino)

**Author**: Circuit Digest Team
**Difficulty Level**: Intermediate
**Estimated Time**: 4-6 hours (excluding calibration time)
