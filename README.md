# Assist Vision

![Project Status](https://img.shields.io/badge/status-prototype-orange)
![Platform](https://img.shields.io/badge/platform-ESP32%20%2B%20Android-blue)
![Communication](https://img.shields.io/badge/communication-ESP--NOW%20%7C%20Bluetooth-success)
![License](https://img.shields.io/badge/license-All%20Rights%20Reserved-red)

## 1) Project Title
**Assist Vision** — Wearable Assistive Navigation System for Visually Impaired Users.

## 2) Project Description
Assist Vision is a wearable assistive technology prototype designed to improve environmental awareness for visually impaired users through multi-sensor fusion and audio guidance.  
The system combines obstacle sensing, visual event detection, directional sound awareness, and emergency support features across embedded hardware and an Android mobile application.

## 3) Features
- Ultrasonic obstacle detection for near-range hazards
- Visual detection via ESP32-CAM module
- Sound direction awareness using dual microphones
- ESP-NOW communication between ESP32-CAM and ESP32 DevKit V1
- Bluetooth Classic communication between ESP32 DevKit V1 and Android app
- Real-time Text-To-Speech (TTS) alerts
- Alert prioritization engine for safer, clearer guidance
- Emergency panic button trigger
- Emergency contact notification workflow
- Battery-powered wearable operation

## 4) Hardware Requirements
| Component | Purpose |
|---|---|
| ESP32 DevKit V1 | Main controller and sensor fusion node |
| ESP32-CAM AI Thinker | Visual detection module |
| Ultrasonic Sensor | Obstacle distance detection |
| Dual Microphones | Sound direction detection |
| Emergency Push Button | Immediate panic/emergency trigger |
| Battery Pack / Power Module | Portable wearable power source |

## 5) Software Requirements
| Software | Use |
|---|---|
| Arduino IDE / PlatformIO | ESP32 firmware development |
| ESP32 Board Package | Compiling/flashing ESP32 devices |
| Android Studio | Android app development |
| Android SDK | App build and deployment |
| Bluetooth Classic APIs | Device-to-phone communication |
| Text-To-Speech (TTS) Engine | Voice alert output |

## 6) System Architecture Diagram
```text
ESP32-CAM (Visual Detection)
          |
       ESP-NOW
          |
ESP32 DevKit V1 (Main Controller + Sensor Fusion)
          |
   Bluetooth Classic
          |
Android Application
   |               |
Text To Speech   Emergency Contact System
          |
     User Interface
```

## 7) Wiring Overview
| Module | Typical Connection (ESP32 DevKit V1) | Notes |
|---|---|---|
| Ultrasonic Sensor (Trig/Echo) | Any GPIO digital pins | Use safe voltage logic levels |
| Dual Microphones | ADC-capable GPIO pins | Calibrate threshold and direction logic |
| Emergency Push Button | GPIO input + pull-up/down | Debounce in firmware |
| ESP32-CAM | Wireless via ESP-NOW | Separate board, no direct wire required |
| Android Device | Bluetooth Classic pairing | Runtime control and audio output |

## 8) Installation Guide
1. Assemble hardware modules into wearable enclosure.
2. Flash firmware to:
   - ESP32 DevKit V1 (main logic)
   - ESP32-CAM AI Thinker (visual detection sender)
3. Install Android app on target phone.
4. Pair Android device with ESP32 DevKit V1 over Bluetooth Classic.
5. Calibrate sensors (distance thresholds, microphone sensitivity, alert priorities).
6. Perform controlled indoor validation before field usage.

## 9) ESP32 Setup
1. Install Arduino IDE (or PlatformIO) and ESP32 board definitions.
2. Select correct board:
   - **ESP32 Dev Module** for DevKit V1
   - **AI Thinker ESP32-CAM** for camera module
3. Configure Wi-Fi/ESP-NOW peer information and channel settings.
4. Upload firmware to each board.
5. Verify serial output and packet flow between modules.

## 10) Android App Setup
1. Open Android project in Android Studio.
2. Enable required permissions (Bluetooth, notifications, audio, etc.).
3. Build and install APK on test device.
4. Pair with ESP32 DevKit V1 over Bluetooth Classic.
5. Validate:
   - incoming alerts
   - TTS playback
   - emergency contact flow

## 11) Bluetooth Communication Flow
```text
ESP32 DevKit V1
  -> Formats alert packets (priority + type + metadata)
  -> Sends packets over Bluetooth Classic
Android App
  -> Parses packet
  -> Applies user settings/profile
  -> Triggers TTS + UI notification + emergency actions (if needed)
```

## 12) ESP-NOW Communication Flow
```text
ESP32-CAM
  -> Performs visual detection
  -> Sends compact detection message via ESP-NOW
ESP32 DevKit V1
  -> Receives and validates packet
  -> Merges with ultrasonic/microphone events
  -> Generates prioritized alert stream
```

## 13) Alert Priority System
| Priority | Category | Example |
|---|---|---|
| P0 (Critical) | Immediate danger / emergency | Fall risk, panic button activated |
| P1 (High) | Close obstacle / urgent hazard | Obstacle within critical threshold |
| P2 (Medium) | Important environmental event | Person/object detected nearby |
| P3 (Low) | Informational updates | General direction or status cue |

Suggested policy:
- Always interrupt lower-priority speech for P0/P1 alerts.
- Throttle repeated alerts to avoid cognitive overload.
- Escalate to emergency contact flow for panic events.

## 14) Project Folder Structure
```text
AssistVision/
├── firmware/
│   ├── esp32-devkit-main/
│   └── esp32-cam-module/
├── android-app/
│   └── app/
├── docs/
│   ├── architecture/
│   └── wiring/
└── README.md
```

## 15) Future Improvements
- Add GPS-based outdoor guidance support
- Integrate vibration/haptic feedback for silent environments
- Improve on-device vision inference with lightweight models
- Add multilingual TTS and user personalization profiles
- Add battery health monitoring and low-power optimization
- Improve environmental robustness through sensor redundancy

## 16) Contributors
- Project Owner: **KarnAbhinav00**
- Contributors: Open by explicit owner authorization only

## 17) License (All Rights Reserved)
This repository uses an **All Rights Reserved** license.  
See the full license terms in [`LICENSE`](LICENSE).

## Restricted Use Policy
No individual, organization, company, institution, government agency, commercial entity, or third party is granted permission to use, deploy, redistribute, commercialize, manufacture, sell, modify, rebrand, integrate, or distribute this project without explicit written permission from the project owner.

Unauthorized use of the source code, hardware design, documentation, assets, branding, concepts, or derivative works is strictly prohibited.

Forking, copying, reproducing, training AI models on repository contents, commercial deployment, and redistribution are not permitted without prior written authorization.

**All rights are reserved by the project owner.**

## 18) Disclaimer
- This project is a research, educational, and prototype project.
- This system must **NOT** be relied upon as a primary mobility aid.
- This project is **not** a certified medical device.
- Detection and alert results may be inaccurate, delayed, incomplete, or unavailable.
- The developers assume **no responsibility** for injury, loss, damages, accidents, or misuse.
- Users must use independent judgment and proper mobility assistance methods at all times.
- This project is provided **"AS IS"**, without warranty of any kind, express or implied.

## 19) Safety Notice
Assist Vision should only be used as a supplementary awareness tool in controlled and validated conditions.  
Users must continue to use established mobility assistance methods (such as canes, trained support, or certified aids) and should never rely exclusively on this prototype for personal safety.