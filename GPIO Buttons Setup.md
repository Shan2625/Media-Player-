# GPIO Buttons Hardware Setup Guide for Raspberry Pi 4 Model B

## Hardware Components Required

For each button, you'll need:
- Push button/momentary switch (tactile switch)
- Jumper wires (male-to-female recommended)
- Breadboard (optional, for easier connections)

## Hardware Connection Methods

### Using Internal Pull-up Resistors (Recommended)

This method uses the Raspberry Pi's built-in pull-up resistors, so no external resistors are needed.

```
Connection for each button:
Button Terminal 1  →  GPIO Pin
Button Terminal 2  →  GND (Ground Pin)
```

## GPIO Pin Assignments

### Current Project Configuration (From My Code)

```
Function          GPIO Pin    Physical Pin    Button Connections
IMAGE_BUTTON      GPIO 17     Pin 11         Button → GPIO 17 + Button → GND
VIDEO_BUTTON      GPIO 27     Pin 13         Button → GPIO 27 + Button → GND
PLAYLIST_BUTTON   GPIO 22     Pin 15         Button → GPIO 22 + Button → GND
```

## Software Setup

### 1. Install Required Libraries

```bash
sudo apt update
sudo apt install python3-pip
pip3 install RPi.GPIO
```

### 2. Enable GPIO Access

Add your user to the gpio group:
```bash
sudo usermod -a -G gpio pi
```

### 3. Basic Button Test Script

Create a test file to verify button functionality:

```bash
 button_test.py
```

Add the following code:

```python
#!/usr/bin/env python3
import RPi.GPIO as GPIO
import time

# GPIO pin assignments (matching your media display project)
IMAGE_BUTTON = 17
VIDEO_BUTTON = 27
PLAYLIST_BUTTON = 22

def setup_buttons():
    """Initialize GPIO pins for the three buttons"""
    GPIO.setmode(GPIO.BCM)
    GPIO.setwarnings(False)
    
    # Setup buttons with internal pull-up resistors
    GPIO.setup(IMAGE_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    GPIO.setup(VIDEO_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    GPIO.setup(PLAYLIST_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
    
    print(f"Setup IMAGE_BUTTON on GPIO {IMAGE_BUTTON} (Pin 11)")
    print(f"Setup VIDEO_BUTTON on GPIO {VIDEO_BUTTON} (Pin 13)")
    print(f"Setup PLAYLIST_BUTTON on GPIO {PLAYLIST_BUTTON} (Pin 15)")

def test_buttons():
    """Test the three buttons with debouncing"""
    print("\nButton test running. Press buttons to test. Ctrl+C to exit.")
    print("Expected behavior: Button press detected when button is released")
    print("-" * 60)
    
    try:
        while True:
            # Check IMAGE button
            if GPIO.input(IMAGE_BUTTON) == GPIO.LOW:
                print("[BUTTON] IMAGE BUTTON (GPIO 17) pressed!")
                while GPIO.input(IMAGE_BUTTON) == GPIO.LOW:
                    time.sleep(0.1)  # Wait for button release (debouncing)
                print("         IMAGE BUTTON released")
            
            # Check VIDEO button  
            elif GPIO.input(VIDEO_BUTTON) == GPIO.LOW:
                print("[BUTTON] VIDEO BUTTON (GPIO 27) pressed!")
                while GPIO.input(VIDEO_BUTTON) == GPIO.LOW:
                    time.sleep(0.1)  # Wait for button release (debouncing)
                print("         VIDEO BUTTON released")
            
            # Check PLAYLIST button
            elif GPIO.input(PLAYLIST_BUTTON) == GPIO.LOW:
                print("[BUTTON] PLAYLIST BUTTON (GPIO 22) pressed!")
                while GPIO.input(PLAYLIST_BUTTON) == GPIO.LOW:
                    time.sleep(0.1)  # Wait for button release (debouncing)
                print("         PLAYLIST BUTTON released")
            
            time.sleep(0.05)  # Small delay to prevent excessive CPU usage
            
    except KeyboardInterrupt:
        print("\nTest interrupted by user")

def main():
    """Main function to test the three media display buttons"""
    print("=== Media Display Project - Button Test ===")
    print("Testing buttons used in your media display project:")
    print("- IMAGE_BUTTON: GPIO 17 (Pin 11)")
    print("- VIDEO_BUTTON: GPIO 27 (Pin 13)")  
    print("- PLAYLIST_BUTTON: GPIO 22 (Pin 15)")
    print()
    
    setup_buttons()
    test_buttons()
    
    print("\nCleaning up GPIO...")
    GPIO.cleanup()
    print("GPIO cleanup complete. Test finished.")

if __name__ == "__main__":
    main()


## Integration with My Media Display Project

Based on my existing code, here's how the GPIO buttons are already implemented:

### Current Button Configuration in Your Project

```python
# === GPIO setup === (from your working code)
IMAGE_BUTTON = 17    # GPIO pin for image playlist
VIDEO_BUTTON = 27    # GPIO pin for video playlist  
PLAYLIST_BUTTON = 22 # GPIO pin for main playlist

GPIO.setmode(GPIO.BCM)
GPIO.setup(IMAGE_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(VIDEO_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(PLAYLIST_BUTTON, GPIO.IN, pull_up_down=GPIO.PUD_UP)
```

### Hardware Connections for my Project

```
Function          GPIO Pin    Physical Pin    Connection
IMAGE_BUTTON      GPIO 17     Pin 11         Button → GPIO 17 + Button → GND
VIDEO_BUTTON      GPIO 27     Pin 13         Button → GPIO 27 + Button → GND  
PLAYLIST_BUTTON   GPIO 22     Pin 15         Button → GPIO 22 + Button → GND
```

