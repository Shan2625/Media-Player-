# Media-Player-
An automated media player for the Raspberry Pi that displays scheduled playlists of images and videos. The player can be controlled manually via three GPIO buttons to switch between different playlists, and it is designed for continuous, stable operation on a display like a TV.


# Raspberry Pi Media Display — Code Overview

This Python script is a media player designed for the Raspberry Pi. It plays images and videos in fullscreen mode and supports control via GPIO buttons. Additionally, it features a built-in time-based scheduler that automatically switches between playlists for morning, afternoon, and evening.

---

## Code Structure

### 1. Initialization
- Sets up GPIO pins using BCM numbering for three buttons:
  - Image button
  - Video button
  - Mixed playlist button
- Initializes `pygame` for fullscreen display and hides the mouse cursor.
- Initializes global state variables such as screen mode, playback flags, and playlist paths.

### 2. Scheduler
- If `ENABLE_SCHEDULER = True`, the program checks the current time and loads the appropriate playlist:
  - Morning: 08:00+
  - Afternoon: 13:00+
  - Evening: 18:00+
- The scheduler playlist begins automatically at launch if enabled.

### 3. Playlist Loading
- The `load_playlist()` function reads a plain-text playlist file.
- Each line defines either an image or video and (optionally) the display duration for images.
- Filters playlists by media type when needed.

### 4. Image Display (`display_image`)
- Loads an image using `pygame`, scales it to fit the screen while maintaining aspect ratio, and displays it.
- Supports landscape and portrait orientation by rotating the image if needed.

### 5. Video Playback (`play_single_video`)
- Uses `python-vlc` to play videos embedded within the Pygame window.
- Videos are rendered using software via `--vout=x11` to avoid hardware compatibility issues.
- Cleans up the VLC instance after each video completes.

### 6. Playlist Playback (`playlist_loop`)
- Loops through a list of playlist items (images/videos).
- Displays each item, waits the specified duration for images, or plays videos to completion.
- Listens for restart signals and gracefully loops the list.

### 7. GPIO Button Control
- The main loop checks for GPIO button input:
  - **Image Button:** Starts or cycles image mode (manual or auto-loop).
  - **Video Button:** Plays all videos in loop mode.
  - **Playlist Button:** Plays the full mixed playlist (images and videos).
- When a button is pressed, any running playlist thread is stopped and replaced.

### 8. Auto Image Looping
- When in image-only mode, images auto-advance after their duration unless interrupted by a button press.

### 9. Cleanup
- Pressing the `ESC` key exits the program.
- On exit, all running threads are stopped, GPIO is cleaned up, and the display is reset.

---

## Summary

The script is modular, combining Pygame for images, VLC for video, and GPIO for physical control. It supports scheduled playback and allows for flexible media management via simple playlist files.


FUll code under "Code" File
