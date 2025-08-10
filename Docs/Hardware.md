# Hardware Requirements for a Raspberry Pi Project

This project is designed to run on a **Raspberry Pi 4 Model B** and is controlled using physical buttons connected to its GPIO pins. Here's a structured breakdown of the required and recommended hardware, along with the specific GPIO pin assignments.

## Required Components

### Core Computing Unit
- **Raspberry Pi 4 Model B**: The core computing unit for running the media display application

### Storage
- **MicroSD Card (16GB or larger)**: Used for the operating system (Raspberry Pi OS) and to store all your media files

### Display
- **HDMI Display (TV or Monitor)**: A screen for displaying the media output

### Control Interface  
- **3 Momentary Push Buttons**: These buttons are used to switch between image, video, and playlist modes
- **Male-to-Female Jumper Wires**: For connecting the push buttons to the Raspberry Pi's GPIO pins and ground
- **Breadboard**: To test and prototype the GPIO button connections

### Power and Audio
- **Power Supply (5V 3A)**: A reliable power source for the Raspberry Pi
- **External Speakers**: Needed for audio playback if you're using video media

### Timekeeping Module
- **RTC Module DS3231**: To keep track of time for the Raspberry Pi, ensuring accurate scheduling even without internet connectivity

## GPIO Pin Assignments (BCM Numbering)

This project uses internal pull-up resistors, so no external resistors are needed for the buttons. When a button is pressed, its corresponding GPIO pin is pulled to a low state.

### Button Connections

| Function | GPIO Pin | Physical Pin | Connection |
|----------|----------|--------------|------------|
| **Image Mode Button** | GPIO 17 | Pin 11 | Connect one side of the button to GPIO pin 17 and the other side to a ground (GND) pin |
| **Video Mode Button** | GPIO 27 | Pin 13 | Connect one side of the button to GPIO pin 27 and the other side to a ground (GND) pin |
| **Playlist Mode Button** | GPIO 22 | Pin 15 | Connect one side of the button to GPIO pin 22 and the other side to a ground (GND) pin |

### RTC Module Connections

| DS3231 Pin | Raspberry Pi Pin | Description |
|------------|------------------|-------------|
| **VCC** | Pin 1 (3.3V) | Power supply |
| **GND** | Pin 6 (Ground) | Ground connection |
| **SDA** | Pin 3 (GPIO 2) | I2C data line |
| **SCL** | Pin 5 (GPIO 3) | I2C clock line |

## Optional Components

### Additional Control Options
- **Additional Push Buttons**: For volume control, shutdown, or other custom functions
- **10kΩ Resistors**: If you prefer to use external pull-down resistors instead of internal pull-up resistors

### Enclosure and Protection
- **Raspberry Pi Case**: To protect the Pi from dust and physical damage
- **GPIO Breakout Board**: For easier and more organized GPIO connections

### Enhanced Audio/Visual
- **HDMI Cable**: For connecting to display (if not included with display)
- **3.5mm Audio Cable**: Alternative audio connection method
- **USB Keyboard/Mouse**: For initial setup and troubleshooting

## Recommended Specifications

### MicroSD Card
- **Capacity**: 32GB or larger recommended for storing multiple media files
- **Speed Class**: Class 10 or UHS-I for better performance
- **Brand**: SanDisk, Samsung, or other reputable brands

### Display Requirements
- **Resolution**: 1920x1080 (Full HD) or higher
- **Input**: HDMI compatible
- **Size**: 24" or larger for optimal viewing experience

### Power Supply
- **Output**: 5V DC, 3A minimum
- **Connector**: USB-C for Raspberry Pi 4
- **Quality**: Official Raspberry Pi power supply recommended

## Assembly Notes

### Button Wiring
- All buttons use the same wiring pattern: one terminal to designated GPIO pin, other terminal to any available GND pin
- No external resistors needed due to internal pull-up configuration
- Connections should be secure to prevent intermittent operation

### RTC Module Installation
- The DS3231 module should be connected before the first boot for proper initialization
- Ensure correct I2C connections to prevent communication errors
- The module includes a backup battery for maintaining time during power outages

### General Guidelines
- Always power off the Raspberry Pi before making GPIO connections
- Use quality jumper wires to ensure reliable connections
- Consider using a breadboard for temporary connections during testing
- Secure all connections to prevent accidental disconnection during operation

## Power Consumption Estimate

| Component | Typical Power Draw |
|-----------|-------------------|
| Raspberry Pi 4 Model B | 3W (idle) - 6.4W (load) |
| HDMI Display | 20W - 100W (varies by size) |
| External Speakers | 5W - 20W (varies by model) |
| RTC Module DS3231 | <1W |
| **Total System** | **28W - 127W** |

## Compatibility Notes

- This project is specifically designed for **Raspberry Pi 4 Model B**
- GPIO pin assignments are compatible with all Raspberry Pi models, but performance may vary
- The DS3231 RTC module is compatible with all Raspberry Pi models with I2C support
- External speakers should be compatible with 3.5mm audio jack or HDMI audio output
