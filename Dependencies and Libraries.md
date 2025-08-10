
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

### Install Core Python Dependencies
```bash
pip3 install pygame
pip3 install python-vlc
pip3 install RPi.GPIO
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


## Virtual Environment Setup 

### 1. Install Virtual Environment
```bash
sudo apt install -y python3-venv
```

### 2. Create Virtual Environment (Change name to your preference)
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

### Configure Audio Output
```bash
# For HDMI audio
sudo raspi-config
# Navigate to: Advanced Options -> Audio -> Force HDMI
```

## Final Verification

After installation, test your complete setup:
```bash
python3 /home/pi/media_display_project/media_display.py
```

This should run your media display project without any import errors or missing dependencies.
