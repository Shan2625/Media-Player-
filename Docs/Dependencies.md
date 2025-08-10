# Dependencies and Libraries for Media Display Project

This guide covers all the system dependencies and Python libraries required to run the Media Display Project on Raspberry Pi 4 Model B.

## Prerequisites

- Raspberry Pi 4 Model B with Raspberry Pi OS
- Internet connection for downloading packages
- At least 2GB free space on SD card

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

### Alternative Installation with Specific Versions (Recommended)

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

### 4. Test All Imports from the Code

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

## Virtual Environment Setup (Recommended)

### 1. Install Virtual Environment

```bash
sudo apt install -y python3-venv
```

### 2. Create Virtual Environment

```bash
python3 -m venv /home/pi/EGL314Shan
```
*Note: Change the path name to your preference*

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
```
Navigate to: **Interface Options** → **GPIO** → **Yes**

### 2. Enable I2C (for RTC Module)

```bash
sudo raspi-config
```
Navigate to: **Interface Options** → **I2C** → **Yes**

### 3. Add User to GPIO Group

```bash
sudo usermod -a -G gpio pi
```

## Audio Configuration

### Configure Audio Output for HDMI

```bash
sudo raspi-config
```
Navigate to: **Advanced Options** → **Audio** → **Force HDMI**

### Alternative Audio Configuration

```bash
# For 3.5mm jack output
sudo raspi-config
# Navigate to: Advanced Options → Audio → Force 3.5mm jack
```

## One-Line Installation Script

For quick setup, you can create and run this installation script:

```bash
#!/bin/bash
# Quick installation script
sudo apt update && sudo apt upgrade -y
sudo apt install -y python3 python3-pip python3-dev python3-venv
sudo apt install -y vlc vlc-plugin-base libvlc-dev
sudo apt install -y libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev
sudo apt install -y libfreetype6-dev libportmidi-dev libjpeg-dev zlib1g-dev
sudo apt install -y i2c-tools alsa-utils
pip3 install pygame==2.1.2 python-vlc==3.0.16120 RPi.GPIO==0.7.1
sudo usermod -a -G gpio pi
echo "Installation complete! Please reboot your system."
```

Save as `install_dependencies.sh`, make executable, and run:
```bash
chmod +x install_dependencies.sh
./install_dependencies.sh
sudo reboot
```

## Final Verification

After installation and reboot, test your complete setup:

```bash
python3 /home/pi/Media-Player-/media_display.py
```

This should run your media display project without any import errors or missing dependencies.

## Common Issues and Solutions

### Issue 1: VLC Not Found
```bash
sudo apt install --reinstall vlc libvlc-dev
```

### Issue 2: Pygame Installation Fails
```bash
sudo apt install -y python3-dev libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev
pip3 install --upgrade pip
pip3 install pygame
```

### Issue 3: GPIO Permission Denied
```bash
sudo usermod -a -G gpio $USER
sudo reboot
```

### Issue 4: Audio Not Working
```bash
# Test audio output
speaker-test -t wav
# Configure audio
sudo raspi-config
```

## Memory and Storage Requirements

- **RAM**: 2GB minimum, 4GB recommended
- **Storage**: 2GB free space for dependencies
- **Additional**: Space for your media files

## Performance Notes

After installation, the system will use approximately:
- **150MB RAM** during normal operation
- **300MB RAM** during video playback
- **15-30% CPU** during media display
