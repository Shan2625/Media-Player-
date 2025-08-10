
## System Dependencies

### 1. Update System Packages
```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Python 3 and Package Manager
```bash
sudo apt install -y python3 python3-pip python3-dev
```

### 3. VLC Media Player and Libraries
```bash
sudo apt install -y vlc vlc-plugin-base
sudo apt install -y libvlc-dev
```

### 4. SDL Development Libraries (for Pygame)
```bash
sudo apt install -y libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev
```

### 5. Additional System Libraries
```bash
sudo apt install -y libfreetype6-dev libportmidi-dev libjpeg-dev zlib1g-dev
sudo apt install -y libavformat-dev libavcodec-dev libavdevice-dev libavutil-dev libswscale-dev libswresample-dev libavfilter-dev
```

### 6. I2C Tools (for RTC Module)
```bash
sudo apt install -y i2c-tools
```

## Python Libraries

### 1. Install Core Python Dependencies
```bash
pip3 install pygame
pip3 install python-vlc
pip3 install RPi.GPIO
```

### 2. Alternative Installation with Specific Versions (Recommended)
```bash
pip3 install pygame==2.1.2
pip3 install python-vlc==3.0.16120
pip3 install RPi.GPIO==0.7.1
```

## Verify Installation

### 1. Test Pygame Installation
```bash
python3 -c "import pygame; print('Pygame version:', pygame.version.ver)"
```

### 2. Test VLC Python Bindings
```bash
python3 -c "import vlc; print('VLC Python bindings installed successfully')"
```

### 3. Test GPIO Library
```bash
python3 -c "import RPi.GPIO as GPIO; print('RPi.GPIO installed successfully')"
```

### 4. Test All Imports from Your Code
```bash
python3 -c "
import pygame
import os
import time
import RPi.GPIO as GPIO
import threading
import vlc
print('All required libraries imported successfully!')
"
```


## Virtual Environment Setup (Optional but Recommended)

### 1. Install Virtual Environment
```bash
sudo apt install -y python3-venv
```

### 2. Create Virtual Environment
```bash
python3 -m venv /home/pi/EGL314Shan
```

### 3. Activate Virtual Environment
```bash
source /home/pi/EGL314Shan/bin/activate
```

### 4. Install Dependencies in Virtual Environment
```bash
pip install pygame python-vlc RPi.GPIO
```

### 5. Deactivate Virtual Environment
```bash
deactivate
```

## System Configuration

### 1. Enable GPIO
```bash
sudo raspi-config
# Navigate to: Interface Options -> GPIO -> Yes
```

### 2. Enable I2C (for RTC)
```bash
sudo raspi-config  
# Navigate to: Interface Options -> I2C -> Yes
```

### 3. Add User to GPIO Group
```bash
sudo usermod -a -G gpio pi
```

## Audio Configuration

### 1. Install Audio Libraries
```bash
sudo apt install -y alsa-utils pulseaudio pulseaudio-utils
```

### 2. Configure Audio Output
```bash
# For HDMI audio
sudo raspi-config
# Navigate to: Advanced Options -> Audio -> Force HDMI
```

## Common Issues and Solutions

### Issue 1: VLC Not Found
```bash
# Solution: Ensure VLC is properly installed
sudo apt install --reinstall vlc
```

### Issue 2: Pygame Installation Fails
```bash
# Solution: Install additional dependencies
sudo apt install -y python3-dev libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev
```

### Issue 3: GPIO Permission Denied
```bash
# Solution: Add user to gpio group and reboot
sudo usermod -a -G gpio $USER
sudo reboot
```

### Issue 4: VLC Python Bindings Import Error
```bash
# Solution: Reinstall python-vlc
pip3 uninstall python-vlc
pip3 install python-vlc
```

# Install Python libraries
pip3 install pygame==2.1.2 python-vlc==3.0.16120 RPi.GPIO==0.7.1



## Final Verification

After installation, test your complete setup:
```bash
python3 /home/pi/media_display_project/media_display.py
```

This should run your media display project without any import errors or missing dependencies.
