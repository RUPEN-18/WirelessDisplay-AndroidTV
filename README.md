# WirelessDisplay-AndroidTV

A low-latency wireless screen-casting system for streaming a Windows desktop to an Android TV over a local network.

This project was developed during my internship at **Larsen & Toubro (L&T)** as part of my work involving networking, multimedia streaming, Windows systems, and Android development.

The system consists of a **Windows sender application** and an **Android TV receiver application**. The sender captures the Windows desktop, encodes the video stream, and transmits it over the local network to the Android TV receiver for real-time playback.

---

## Project Overview

WirelessDisplay-AndroidTV was designed to provide a lightweight local-network screen-casting solution without depending on cloud-based streaming services.

The system follows a sender-receiver architecture:

```text
Windows PC
    │
    │ Desktop Capture
    ▼
FFmpeg / Encoder
    │
    │ H.264 Video
    ▼
TCP/IP Network
    │
    ▼
Android TV Receiver
    │
    │ Decode & Playback
    ▼
Android TV Display
```

The sender application provides controls for discovering receiver devices, manually connecting to a receiver, configuring streaming quality, starting or stopping a casting session, and monitoring the current stream status.

---

## Screenshots

### Sender Application UI

![Wireless Display Sender UI](assets/ui-sender.png)

Main sender interface for receiver discovery, streaming configuration, status monitoring, and wireless screen casting.

---

## Key Features

- Real-time Windows desktop screen casting
- Android TV receiver application
- Local network streaming
- Automatic receiver discovery
- Manual receiver IP connection
- H.264 video encoding
- TCP-based video transmission
- Low-latency streaming mode
- Multiple streaming quality profiles
- Stream status monitoring
- Resolution monitoring
- FPS monitoring
- Encoder information display
- Session timer
- Start and stop casting controls
- FFmpeg-based desktop capture
- Hardware encoder support where available

---

## Streaming Profiles

The sender interface supports different streaming configurations depending on the required quality and latency.

### High Quality

Designed for scenarios where image quality is more important than latency.

### Balanced

Provides a balance between stream quality, network bandwidth, and responsiveness.

### Low Latency

Optimized for fast real-time screen sharing with reduced buffering and minimal delay.

---

## Technologies Used

### Windows Sender

- Python / Desktop Application
- FFmpeg
- GDIGRAB screen capture
- H.264 video encoding
- NVIDIA NVENC hardware acceleration
- TCP/IP networking
- UDP receiver discovery
- Windows networking APIs

### Android TV Receiver

- Android Studio
- Android SDK
- Kotlin / Java
- ExoPlayer / Android Media3
- TCP socket communication
- Android TV interface
- Network stream playback

### Video & Networking

- H.264
- MPEG Transport Stream
- TCP
- UDP
- Local Area Network
- Wi-Fi / Ethernet

---

## How It Works

### 1. Receiver Discovery

The Windows sender searches the local network for available Android TV receiver devices.

The receiver can respond to discovery requests so that the sender can automatically identify available displays.

A manual IP connection option is also provided when automatic discovery is unavailable.

### 2. Screen Capture

The Windows desktop is captured using FFmpeg.

FFmpeg's Windows desktop capture functionality allows the system to continuously obtain frames from the active display.

### 3. Video Encoding

Captured frames are encoded using H.264.

Where supported, hardware encoding such as **NVIDIA NVENC** can be used to reduce CPU usage and improve real-time performance.

### 4. Network Streaming

The encoded video stream is transmitted over the local network.

The system uses network socket communication between the Windows sender and Android TV receiver.

### 5. Android TV Playback

The Android TV receiver accepts the incoming stream and passes it to the media playback system.

The received video is then displayed on the television with minimal buffering.

---

## Sender Application

The Windows sender interface provides several important controls.

### Receiver Devices

Displays available Android TV receivers detected on the local network.

### Manual Connect

Allows the user to enter the receiver's local IP address and connect directly.

Example:

```text
192.168.1.xxx
```

### Stream Status

Displays information such as:

```text
Video Status
Audio Status
Resolution
Frames Per Second
```

### Streaming Profile

Users can select between:

```text
HIGH QUALITY
BALANCED
LOW LATENCY
```

### Encoder Status

Displays information about the active encoder.

Example:

```text
NVIDIA NVENC
```

### Session Information

Displays:

- Streaming state
- Session duration
- Network status
- Encoder status

---

## Example Streaming Pipeline

A simplified FFmpeg pipeline can look like:

```bash
ffmpeg -f gdigrab -framerate 60 -i desktop \
-c:v libx264 \
-preset ultrafast \
-tune zerolatency \
-f mpegts \
tcp://RECEIVER_IP:PORT
```

For systems with supported NVIDIA GPUs, hardware encoding can also be used.

Conceptually:

```text
Desktop
   ↓
Screen Capture
   ↓
H.264 Encoder
   ↓
MPEG-TS
   ↓
TCP Network Stream
   ↓
Android TV
```

---

## Network Architecture

Both devices should normally be connected to the same local network.

```text
┌───────────────────────┐
│      Windows PC       │
│                       │
│ Wireless Display      │
│ Sender                │
└──────────┬────────────┘
           │
           │ Wi-Fi / Ethernet
           │
           ▼
┌───────────────────────┐
│    Local Network      │
│   Router / Access     │
│       Point           │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│      Android TV       │
│                       │
│ Wireless Display      │
│ Receiver              │
└───────────────────────┘
```

---

## Requirements

### Windows Sender

- Windows 10 or Windows 11
- FFmpeg
- Network connection
- Wi-Fi or Ethernet
- Compatible GPU recommended for hardware acceleration

Optional:

- NVIDIA GPU with NVENC support

### Android TV Receiver

- Android TV device or Android TV emulator
- Network connection
- Receiver application installed
- Sender and receiver connected to the same local network

### Development Environment

- Android Studio
- Android SDK
- Gradle
- Git

---

## Running the Project

Clone the repository:

```bash
git clone https://github.com/RUPEN-18/WirelessDisplay-AndroidTV.git
```

Move into the repository:

```bash
cd WirelessDisplay-AndroidTV
```

Open the Android receiver project using Android Studio.

Allow Gradle to synchronize all required dependencies.

Then:

1. Start the Android TV receiver application.
2. Connect the Windows PC and Android TV to the same network.
3. Launch the Windows sender application.
4. Allow receiver discovery to locate the Android TV.
5. If necessary, enter the receiver IP manually.
6. Select the preferred streaming profile.
7. Click **Start Casting**.
8. The Windows desktop stream should appear on the Android TV.

---

## Repository Structure

```text
WirelessDisplay-AndroidTV/
│
├── AndroidTVReceiver_FINAL_FIXED/
│   ├── app/
│   ├── gradle/
│   ├── build.gradle.kts
│   ├── settings.gradle.kts
│   ├── gradle.properties
│   ├── gradlew
│   └── gradlew.bat
│
├── assets/
│   └── ui-sender.png
│
├── README.md
└── .gitignore
```

Generated Gradle and Android Studio build files are excluded from version control.

---

## Git Ignore Configuration

The repository excludes temporary and machine-specific files such as:

```text
.gradle/
.idea/
build/
**/build/
local.properties
*.iml
captures/
.externalNativeBuild/
.cxx/
*.log
```

This keeps the repository focused on the actual source code.

---

## Performance Goals

The project was designed with the following priorities:

- Low streaming latency
- Smooth frame delivery
- Stable local-network communication
- Reduced buffering
- Hardware-accelerated video encoding
- Simple Android TV playback
- Easy receiver discovery

---

## Challenges Addressed

During development, several practical problems were explored, including:

- Windows desktop capture
- Real-time H.264 encoding
- Network video transmission
- Android TV playback
- Device discovery
- IP-based manual connection
- Stream latency
- Frame-rate optimization
- Encoder performance
- Receiver connection handling

---

## Future Improvements

Possible future developments include:

- System audio streaming
- Automatic bitrate adjustment
- Adaptive resolution
- Multi-monitor selection
- Automatic reconnection
- Improved receiver discovery
- Multiple Android TV receivers
- Stream encryption
- Authentication between sender and receiver
- Hardware decoding optimization
- Network quality monitoring
- Bitrate controls
- Custom resolution selection
- Recording support
- Full-screen receiver controls

---

## Learning Outcomes

This project provided practical experience with:

- Computer networking
- TCP/IP communication
- UDP discovery
- Client-server architecture
- Android development
- Android TV applications
- FFmpeg
- Video encoding
- Real-time multimedia streaming
- Windows desktop capture
- Hardware acceleration
- Git and GitHub
- Software debugging and testing

---

## Internship Project

This project was developed during my internship at **Larsen & Toubro (L&T)** as part of my practical learning and project development work.

It helped me apply concepts involving networking, operating systems, multimedia processing, software development, and real-time communication to a working application.

---

## Author

**Rupendran Manigandan**

B.E. Computer Science and Engineering  
Artificial Intelligence & Robotics  
Sathyabama Institute of Science and Technology

GitHub: **RUPEN-18**

---

## Disclaimer

This repository is maintained as an educational and portfolio project based on work completed during an internship.

It is **not an official Larsen & Toubro software product or official L&T GitHub repository**.

All company names, logos, trademarks, and other intellectual property belong to their respective owners.