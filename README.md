# WirelessDisplay-AndroidTV

Android TV wireless display receiver developed during my internship at **Larsen & Toubro (L&T)** for real-time screen casting from a Windows computer to an Android TV over a local network.

The project uses **FFmpeg** on the Windows sender side and an **Android TV receiver application** built to receive and play the incoming stream with low latency.

## Overview

WirelessDisplay-AndroidTV enables a Windows PC or laptop to capture its screen and stream it directly to an Android TV over TCP/IP.

The system was designed as a lightweight alternative for local-network screen sharing without relying on cloud-based streaming services.

## Features

- Real-time Windows screen casting
- Android TV receiver application
- 1080p video streaming support
- TCP-based network communication
- FFmpeg screen capture and encoding
- Low-latency H.264 streaming
- MPEG-TS transport stream
- Android TV video playback
- Local network operation
- Support for Windows-to-TV streaming
- Simple receiver interface
- Expandable architecture for audio streaming and additional controls

## System Architecture

```text
Windows PC / Laptop
        |
        | Screen Capture
        v
      FFmpeg
        |
        | H.264 Encoding
        | MPEG-TS Stream
        v
   TCP/IP Network
        |
        v
Android TV Receiver
        |
        | Stream Processing
        v
   Video Playback
        |
        v
     Android TV
```

## Technologies Used

### Windows Sender

- FFmpeg
- GDIGRAB
- H.264 / x264
- MPEG-TS
- TCP/IP

### Android TV Receiver

- Android Studio
- Kotlin / Java
- Android SDK
- ExoPlayer / Media3
- TCP Socket Communication

## Project Workflow

1. The Windows system captures the desktop using FFmpeg.
2. The captured frames are encoded using H.264.
3. The encoded video is packaged using MPEG-TS.
4. The stream is transmitted over TCP through the local network.
5. The Android TV application listens for the incoming stream.
6. The receiver processes the stream and displays it on the television.

## Example FFmpeg Streaming Concept

A typical sender configuration can use:

```bash
ffmpeg -f gdigrab -framerate 60 -i desktop \
-c:v libx264 \
-preset ultrafast \
-tune zerolatency \
-f mpegts tcp://ANDROID_TV_IP:PORT
```

The actual IP address and port should be changed according to the local network configuration.

## Requirements

### Sender

- Windows 10 or Windows 11
- FFmpeg installed
- Wi-Fi or Ethernet network connection

### Receiver

- Android TV
- Android TV emulator for development/testing
- Android application installed
- Sender and receiver connected to the same network

## Running the Android TV Application

Clone the repository:

```bash
git clone https://github.com/RUPEN-18/WirelessDisplay-AndroidTV.git
```

Open the project using **Android Studio**.

Allow Gradle to synchronize the required dependencies.

Then:

1. Connect an Android TV device or start an Android TV emulator.
2. Build the application.
3. Install and launch the receiver.
4. Start the FFmpeg stream from the Windows computer.
5. Enter the correct Android TV IP address and configured TCP port on the sender side.

## Development & Testing

The system was tested using:

```text
Windows PC
     ↓
FFmpeg Screen Capture
     ↓
TCP Network Stream
     ↓
Android TV / Android TV Emulator
     ↓
Real-Time Display
```

During development, the receiver was tested with 1080p streaming and optimized for low-latency playback.

## Repository Structure

```text
WirelessDisplay-AndroidTV/
│
├── app/
│   └── Android TV application source
│
├── gradle/
│   └── Gradle configuration
│
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
├── .gitignore
└── README.md
```

Generated Android Studio and Gradle files are excluded from the repository.

## Potential Improvements

Future development could include:

- System audio streaming
- Automatic device discovery
- Improved latency optimization
- Adaptive bitrate streaming
- Resolution selection
- Frame-rate controls
- Hardware-accelerated encoding
- Multiple receiver support
- Automatic reconnection
- Streaming statistics
- Better Android TV interface
- Secure/authenticated connections

## Internship Project

This project was developed as part of my internship work at **Larsen & Toubro (L&T)**.

The repository is intended to demonstrate the technical implementation and skills gained while working with:

- Computer networks
- TCP/IP communication
- Android development
- Video streaming
- FFmpeg
- Multimedia encoding
- Client-server architecture

## Author

**Rupendran Manigandan**

B.E. Computer Science and Engineering  
Artificial Intelligence & Robotics  
Sathyabama Institute of Science and Technology

GitHub: **RUPEN-18**

## Disclaimer

This repository represents an educational and portfolio implementation developed during an internship learning project.

It should not be interpreted as an official Larsen & Toubro product, repository, or software release. All trademarks and company names belong to their respective owners.
