# DS3231 RTC Module Setup Guide for Raspberry Pi 4 Model B

## Hardware Connection

Connect the DS3231 module to your Raspberry Pi's GPIO pins:

```
DS3231 Pin    →    Raspberry Pi Pin
VCC           →    Pin 1 (3.3V)
GND           →    Pin 6 (Ground)
SDA           →    Pin 3 (GPIO 2)
SCL           →    Pin 5 (GPIO 3)
```

## Software Setup

### 1. Enable I2C Interface

 Using raspi-config:
```bash
sudo raspi-config
```
Navigate to: Interfacing Options → I2C → Yes → OK → Finish

### 2. Install I2C Tools

```bash
sudo apt update
sudo apt install -y i2c-tools
```

### 3. Verify Connection

```bash
sudo i2cdetect -y 1
```
You should see the DS3231 detected at address `0x68`.

### 4. Configure the RTC Module

Add RTC overlay to boot configuration:
```bash
echo "dtoverlay=i2c-rtc,ds3231" | sudo tee -a /boot/config.txt
```

### 5. Disable Fake Hardware Clock

```bash
sudo apt remove fake-hwclock
sudo update-rc.d -f fake-hwclock remove
sudo systemctl disable fake-hwclock
```

### 6. Set Up Hardware Clock Service

Edit the hardware clock configuration:
```bash
sudo nano /lib/udev/hwclock-set
```

Comment out these lines (add # at the beginning):
```bash
#if [ -e /run/systemd/system ] ; then
#    exit 0
#fi
```

### 7. Reboot and Test

```bash
sudo reboot
```

After reboot, verify RTC functionality:
```bash
sudo hwclock -r
date
```

## Crontab Integration

Add these lines to your crontab (`crontab -e`):

```bash
# Sync system time from hardware clock on boot
@reboot sleep 3 && hwclock --hctosys

# Start media display application
@reboot sleep 7 && sudo -u pi bash -c "export DISPLAY=:0 && source /home/pi/EGL314Shan/bin/activate && cd /home/pi/media_display_project && python3 /home/pi/media_display_project/media_display.py"
```

## Useful Commands

### Read hardware clock:
```bash
sudo hwclock -r
```

### Set hardware clock from system time:
```bash
sudo hwclock -w
```

### Sync system time from hardware clock:
```bash
sudo hwclock -s
```

### Check system time:
```bash
date
```

### Manual time synchronization (if needed):
```bash
sudo hwclock --hctosys
```

## Troubleshooting

### Check if I2C is enabled:
```bash
lsmod | grep i2c
```

### Check RTC device:
```bash
ls /dev/rtc*
```

### Check system logs for RTC errors:
```bash
sudo dmesg | grep rtc
```

### Verify RTC is working:
```bash
sudo cat /sys/class/rtc/rtc0/date
sudo cat /sys/class/rtc/rtc0/time
```

## Notes

- The DS3231 module maintains accurate timekeeping even when the Raspberry Pi is powered off
- The first crontab entry ensures system time is synchronized from the RTC on every boot
- This setup is essential for applications requiring accurate timing without internet connectivity
- The 3-second delay in the first crontab entry allows the RTC to initialize properly before synchronization

## File Structure

After setup, you should have:
- `/dev/rtc0` - RTC device file
- `/boot/config.txt` - Contains `dtoverlay=i2c-rtc,ds3231`
- Crontab entries for automatic time synchronization and application startup
