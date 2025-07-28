# Raspberry Pi Media Display Player

This repository contains the source code for the Raspberry Pi Media Display Player — a Python-based fullscreen media player that plays images and videos in scheduled loops or via GPIO button control. It is designed specifically for Raspberry Pi devices, enabling hands-free digital signage with minimal setup.

Introduction  •  Installation  •  Usage  •  Documentation  •  Issue?

## Introduction

This project provides a Python script to run a fullscreen media display system that:

- Plays images (JPG, PNG) with configurable display durations.
- Plays videos (MP4) using smooth VLC playback embedded in a single display window.
- Supports physical button input via Raspberry Pi GPIO to switch modes:
  - Image-only playlist
  - Video-only playlist (loads from multiple video lists)
  - Mixed image and video playlist
- Offers scheduled playback based on time of day (morning, afternoon, evening).
- Allows fullscreen portrait/landscape orientation toggle and clean program exit with the ESC key.
- Supports looping playback for all playlists, with no user interaction required.

The script is ideal for retail displays, exhibitions, kiosks, or public information panels.

## Installation

Clone or download the repository to your Raspberry Pi. Make sure you have Python 3 installed.

Install the required Python packages:

pip3 install pygame python-vlc RPi.GPIO



Install required system libraries:

sudo apt update
sudo apt install python3-vlc vlc libvlc-dev python3-pygame x11-utils alsa-utils


Ensure VLC is properly configured to use software rendering to avoid hardware acceleration issues on the Pi.

## Usage

Place your media files (images and videos) inside the project folder. Create your playlists as plain text files without extensions, for example:

/home/pi/media_display_project/morning
/home/pi/media_display_project/afternoon
/home/pi/media_display_project/evening
/home/pi/media_display_project/Video1
/home/pi/media_display_project/Video2



Each file should contain absolute paths to the media items, one per line. For images, you can specify duration (in seconds) like this:

/home/pi/media_display_project/image1.jpg, 8
/home/pi/media_display_project/image2.jpg

Videos do not require duration entries.

To start the player:

python3 /home/pi/media_display_project/media_display.py



If using a virtual environment:

source ~/venv/bin/activate
python3 /home/pi/media_display_project/media_display.py

To make the script run on boot, add the following to `crontab -e`:

@reboot /usr/bin/python3 /home/pi/media_display_project/media_display.py

## Documentation

### GPIO Button Configuration

This project uses 3 GPIO buttons, connected to the following BCM pins:

- GPIO 17: Image playlist button
- GPIO 27: Video playlist button (loads Video1 and Video2 files)
- GPIO 22: Full playlist button (mixed media)

Each button should connect between the respective GPIO pin and ground. Internal pull-up resistors are enabled in software.

### Scheduler Functionality

The script checks the system time on startup and automatically begins one of the three predefined playlists:

- Morning: after 08:00
- Afternoon: after 13:00
- Evening: after 18:00

Scheduler mode can be enabled or disabled by editing the line:

ENABLE_SCHEDULER = True

Once a scheduled playlist starts, it loops until interrupted by a button press.

### Display and Orientation

Media is shown fullscreen. The script centers content with black padding and supports toggling between portrait and landscape orientation.

### Exiting

Press the ESC key to cleanly exit the program.
