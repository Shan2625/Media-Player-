
Raspberry Pi Media Display Player

![alt text](https://img.shields.io/badge/License-MIT-yellow.svg)

A Python-based fullscreen media player for Raspberry Pi that plays images and videos in scheduled loops or via GPIO button control. It is designed for hands-free digital signage with minimal setup.

# ✨ Features :

- Image and Video Playback: Plays JPG, PNG, and MP4 files seamlessly in a single, fullscreen window.

- GPIO Button Control: Switch between image-only, video-only, and mixed-media playlists using physical buttons.

- Scheduled Playback: Automatically starts playlists based on the time of day (morning, afternoon, evening).

- Customizable Playlists: Create simple text files to manage your media and display durations.

- Display Orientation: Toggle between portrait and landscape modes.

- Looping Playback: All playlists loop indefinitely for continuous display.

- Easy Exit: Press the ESC key to cleanly exit the application.

- Auto-start on boot 

# 🚀 Getting Started :

Prerequisites:

A Raspberry Pi with Raspberry Pi OS.

Python 3 installed.

Software Installation

Clone or download this repository to your Raspberry Pi.

Install the required Python packages:
```
pip3 install pygame python-vlc RPi.GPIO
```
Install the necessary system libraries:
You can find them in : 📋 [Dependencies Installation Guide](Docs/Dependencies.md)



# 🛠️ Hardware Setup :

This project supports an optional Real-Time Clock (RTC) module and GPIO buttons for enhanced functionality.

RTC Module: For accurate timekeeping, especially when offline. 


GPIO Buttons: For manual playlist selection.


Hardware required can be found in : [Hardware requirements](Docs/Hardware.md)

Note: Detailed instructions for setting up:

RTC Module can be found in :[RTC Setup](Set_Up/RTC_Setup.md)

GPIO Buttons can be found in :[GPIO Buttons Setup](Set_Up/GPIO_Buttons_Setup.md)


# ⚙️ Usage :

Place Your Media: Add your image and video files to the project folder.

Create Playlists: Create plain text files (e.g., morning, afternoon, evening) in the project directory. Each file should contain the absolute paths to your media files, one per line. For images, you can specify a display duration in seconds:

Playlist Formats can be found in: [Playlists Format](Examples/PlaylistsFormat.txt)


Run the Player:

python3 /home/pi/media_display_project/media_display.py


# 🏃🏻 Running on Boot :

To automatically start the media player on boot, open your crontab:


```crontab -e```

And add the following line at the end of the file:

 Auto-start media display application :
 ```
@reboot sleep 3 && hwclock --hctosys (Sync system time from hardware clock on boot (More on RTC Setup))

@reboot sleep 7 && sudo -u pi bash -c "export DISPLAY=:0 && source /home/pi/EGL314Shan/bin/activate && cd /home/pi/media_display_project && python3 /home/pi/media_display_project/media_display.py"
```
---

## 🔧 Configuration

### **Scheduler**

The script can automatically play a specific playlist based on the time of day:
*   **Morning**: After 08:00
*   **Afternoon**: After 13:00
*   **Evening**: After 18:00

You can enable or disable this feature by editing the `ENABLE_SCHEDULER` variable in the `media_display.py` script. 

Python code can be found in : [Main code](Main.py)

### **GPIO Buttons**

The default GPIO button configuration is as follows (BCM pin numbering):
*   **GPIO 17**: Image playlist
*   **GPIO 27**: Video playlist
*   **GPIO 22**: Mixed-media playlist

These pins are configurable within the script.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! 

---

## 📝 License

This project is licensed under the MIT License.

Click [License](LICENSE.md) to access!
