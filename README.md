# 3DPAWS - Hawaii
This is a detailed account of how the Nugent Lab at the University of Hawai'i has constructed the National Center for Atmospheric Research's (NCAR's) 3D Printed Automatic Weather Station (3D-PAWS). In addition to the original PowerPoints, we've provided wiring diagrams for the instruments requiring soldering and some additional instructions for construction. The Nugent Lab does not claim any of the original ideas or conceptions for the project, this repository simply serves as an unofficial extension of the project documenting additional information gained during our lab's experience during construction.  

# Data streaming
Data streaming for all stations affiliated with 3DPAWS Hawaii can be found at this link {http://ec2-52-200-190-240.compute-1.amazonaws.com/about}

## Main Instruments
Five main instruments need to be constructed for the weather station. 
- Anemometer (Analog)
- Wind Vane (I2C)
- Radiation Shield (I2C)
- Light Sensor (I2C)
- Rain Gauge (Analog) 

These instruments all utilize Qwiic or M5-Stack cables - plug-and-play cables - significantly reducing the amount of soldering required for this project.  If you purchase the Qwiic cables, you'll have to purchase qwiic-to-M5 adapters as well as several qwiic junctions, as motherboard that these instruments are plugged into utilizes M5 stack ports. For this reason, we recommend purchasing mainly M5 stack cables. The radiation shield (re-stated below) requires a few short qwiic cables between the sensors, but aside from this the rest of the sensors can use M5 stack.  

Of the five instruments, two of them transmit data over digital channels while the remaining instruments utilize the popular I2C digital connections. Digital sensors and I2C sensors represent two different methods of interfacing sensors with microcontrollers. As a group without a formal education in electronic construction, we've provided the small summary of these two sensors below as a learning place for other novices as well. 

### Digital Sensors

1. **Output**: Digital sensors typically produce a discrete, digital output that communicates the measurement in binary form, using a series of 0s and 1s - either ON or OFF. This output changes state when the sensor field intensity (in our case, the magnetic field intensity) crosses a certain predefined threshold and can be based on specific protocols like I2C, SPI, or UART. Unlike analog sensors (not present in this project), the output is already digital, meaning the microcontroller can read and process it directly. 
2. **Application**: Suited for applications where the presence or absence of a variable provides key information needed. For the magnetic sensor used in this project (the Honeywell Hall Effects Magnetic Sensor), common uses include speed detection, proximity switching, and position sensing where only the detection of a magnetic field (above a certain threshold) is required, not its precise strength.  
3. **Example**: This sensor is used in the anemometer instrument to determine the rotational speed of the instrument. The cup anemometer contains two magnets on opposite sides of the rotating cup. Every time the cup spins, the Honeywell sensor is triggered by a magnet every 1$\pi$ radian. Based on the frequency of triggers, we can determine the rotational speed of the anemometer and convert this to wind speed. The sensor itself is very simple - providing binary "on" and "off" outputs to use every time it sense a magnet, BUT this information can be translated into something incredibly useful!  

### I2C Sensors

1. **Output**: I2C sensors communicate using the I2C (Inter-Integrated Circuit) protocol - a digital, serial communication protocol. Connecting I2C sensors to microcontrollers is done through two wires: SDA (Serial Data Line) and SCL (Serial Clock Line), allowing for multiple sensors to be connected on the same bus with unique addresses.

2. **Application**: The wiring allows for communication with several devices over the same lines, making I2C sensors extremely popular in the low-cost electronic community. I2C sensors can be more complex than analog and digital sensors, as they incorporate digital interfaces and processing capabilities within the sensor itself. This can lead to higher precision and noise immunity, as well as additional features like calibration data or multiple measurement types from the same sensor.

3. **Examples**: This type of sensor is used repeatedly throughout the project. The radiation shield has 3(!): the digital temperature, humidity, and pressure sensors. These I2C sensors communicate measurements directly to our microcontrollers and therefore don't require any conversion of binary signals like the anemometer.

   

