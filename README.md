# Midnight Player

![Version](https://img.shields.io/badge/version-1.0-blue)
![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![License: GPLv3](https://img.shields.io/badge/License-GPLv3-red.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)

Midnight Player is a modern, feature-rich audio player designed for a seamless music playback experience. It provides functionalities like playlist management, playback speed adjustment, and a dark/light theme.

## Features

- **Audio Playback**: Supports various audio formats including MP3, WAV, FLAC, OGG, M4A, AAC, and WMA.
- **Playlist Management**: Create and manage playlists with ease.
- **Playback Speed Control**: Adjust playback speed between 0.5x and 2x.
- **Dark and Light Themes**: Choose between dark and light themes for an optimal UI experience.
- **Cross-Platform**: Available for Windows, Ubuntu (DEB), and RPM-based Linux distributions.

## Installation

### Windows Installer (EXE)

1. Download the installer from the [Releases](https://github.com/Niamorro/Midnight-Player/releases) section.
2. Run the installer and follow the on-screen instructions.

### Ubuntu (DEB)

1. Download the `.deb` package from the [Releases](https://github.com/Niamorro/Midnight-Player/releases) section.
2. Install it using the following commands:
    ```bash
    sudo dpkg -i midnight-player_<version>.deb
    sudo apt-get install -f
    ```

### RPM-based Linux (RPM)

1. Download the `.rpm` package from the [Releases](https://github.com/Niamorro/Midnight-Player/releases) section.
2. Install it using the following command:
    ```bash
    sudo rpm -i midnight-player-<version>.rpm
    ```

### From Source

1. Ensure you have Python 3.7+ and pip installed.
2. Clone the repository:
    ```bash
    git clone https://github.com/Niamorro/Midnight-Player
    cd Midnight-Player
    ```
3. Install the required packages:
    ```bash
    pip install -r requirements.txt
    ```
4. Run the application:
    ```bash
    python main.py
    ```

## Usage

1. Launch the application.
2. Use the `File` menu to open audio files or folders.
3. Create and manage playlists via the `Add Playlist` and `Remove Playlist` options.
4. Control playback speed using the dropdown menu.
5. Adjust the volume and navigate through tracks using the sliders.

## How It Works

### Audio Processing Pipeline

1. **File Selection:**  
   The user selects an audio file from the **File** menu. Supported formats include MP3, WAV, FLAC, OGG, M4A, AAC, and WMA.

2. **FFmpeg Decoding:**  
   The selected file is passed to `ffmpeg` via a subprocess to extract raw audio data. The command used:
   ```bash
   ffmpeg -v quiet -i <file_path> -f f32le -acodec pcm_f32le -ac 2 -ar <samplerate> -
   ```

3. **Data Processing:**  
   - **Read Audio Data:**  
     The audio data is read in blocks and stored as a NumPy array for efficient processing.
   - **Apply Volume Adjustment:**  
     The volume adjustment is applied by multiplying the audio array by a volume coefficient.
   - **Playback Speed Adjustment:**  
     The playback speed (e.g., 2x) is managed via `sounddevice` by modifying the samplerate.

4. **Playback:**  
   - **Output Stream:**  
     The processed audio data is streamed to the audio output using the `sounddevice` library.
   - **Playback Controls:**  
     Controls such as play/pause, next/previous track, and seek are handled via the `AudioTrigger` class.

### Playback Management

- **Play/Pause:**  
  Uses the `AudioTrigger` class to start/stop audio streaming.

- **Next/Previous Track:**  
  Updates the current track index and loads the next/previous track in the playlist.

- **Seek:**  
  Adjusts the playback position by recalculating the position index based on the slider value.

### Track Queue Management

- **Track Queue Widget:**  
  Displays the current playlist or folder contents.

- **Playlist Widget:**  
  Allows the user to add and remove playlists.

- **Track Info Widget:**  
  Shows metadata and artwork for the currently playing track.

## Screenshots

### Dark Theme

### Light Theme

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request.

## License

This project is licensed under the GPLv3 License. See the [LICENSE](LICENSE) file for details.