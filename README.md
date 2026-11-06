# 🎵 Vibemix-Studio

> **An interactive audiovisual music studio controlled by hand gestures**

Vibemix-Studio combines **real-time hand tracking** with **audio synthesis and digital signal processing**, allowing you to use your hands as a musical instrument. Gestures detected through a camera are translated into OSC messages and mapped to audio parameters in a JUCE-based C++ engine.

---

## ✨ Features

### 📹 Real-Time Hand Tracking

- Hand and finger tracking powered by **MediaPipe** and **OpenCV**
- Gesture recognition for fist, pinch, horns, shaka, peace sign, and open hand
- Parallel-palm detection for two-hand interaction
- Continuous hand openness and pinch-value control
- Live camera preview with annotated landmarks

### 🎚️ JUCE Audio Engine

- Real-time audio processing written in **C++**
- DSP effect concepts including low-pass filtering, delay, pitch shifting, and reverb
- Thread-safe communication between the OSC/network and audio threads

### 🌐 Communication & Web Interface

- OSC/UDP communication between Python and C++
- FastAPI video streaming endpoint for the web application
- React/TypeScript frontend integration
- Real-time gesture telemetry and visual feedback

---

## 🏗️ Architecture

```text
┌─────────────────────────────────────────┐
│       Python / OpenCV / MediaPipe       │
│     Camera input and gesture analysis   │
└──────────────────┬──────────────────────┘
                   │
                   │ OSC / UDP
                   │
                   ▼
┌─────────────────────────────────────────┐
│          JUCE Audio Engine (C++)        │
│                                         │
│  OSC Receiver → Atomic Values           │
│  Smoothed Parameters → DSP Effects      │
│  Audio Output → Speakers                │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│        React / TypeScript Interface     │
│      Visualization and user controls   │
└─────────────────────────────────────────┘
```

---

## 📁 Project Structure

```text
Vibemix-Studio/
│
├── Main.cpp                    # JUCE application entry point
├── MainComponent.cpp/.h        # Main JUCE component and audio logic
├── TAL-Vocoder-2.vst3          # Vocoder plugin
│
├── hand_tracking.py            # Main hand-tracking script
├── gestures.py                 # Gesture detection algorithms
├── audio_stream.py             # Audio streaming utilities
├── drivers.py                  # Driver configuration
├── hand_landmarker.task        # MediaPipe hand-landmarker model
├── woman_hands.jpg             # Sample image
│
├── app/                        # React/TypeScript and FastAPI application
├── osc/                        # OSC-related utilities
└── README.md
```

---

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| **C++ / JUCE** | Audio engine and DSP processing |
| **Python** | Computer vision, gesture recognition, and OSC messages |
| **MediaPipe** | Hand landmark detection |
| **OpenCV** | Camera capture and image processing |
| **OSC / UDP** | Communication between the tracking and audio systems |
| **FastAPI** | Live video streaming |
| **React / TypeScript** | Web interface and visualization |
| **TAL-Vocoder-2** | Vocoder effects |

---

## 🚀 Getting Started

### Install Python Dependencies

```bash
pip install opencv-python mediapipe python-osc numpy fastapi uvicorn
```

### Install Frontend Dependencies

```bash
cd app
npm install
```

### Run Hand Tracking

From the repository root:

```bash
python hand_tracking.py
```

The script opens the camera, detects hand gestures, and sends OSC messages to the configured local UDP endpoint.

The application version also includes a FastAPI video stream:

```bash
cd app
python hand-tracker/hand_tracking.py
```

The video stream is available at:

```text
http://localhost:8000/video
```

### Run the Web Interface

```bash
cd app
npm run dev
```

The development server is typically available at `http://localhost:3000`.

### Build the JUCE Application

The exact build process depends on the JUCE project configuration and operating system. If a Makefile is available for your environment, run:

```bash
make
```

Then launch the generated JUCE application.

---

## 🎛️ Audio Ideas

Vibemix-Studio can be used to experiment with effects such as:

- Underwater or muffled voice
- Autotuned and robotic voice
- Vintage radio or telephone effect
- Choir and vocal-stacking effects
- Large-room or church reverb
- Glitch and loop-based vocal effects

---


| Χειρονομία | Εντολή (OSC) | Λειτουργία στο JUCE | Γιατί βολεύει |
| :--- | :--- | :--- | :--- |
| **Κλειστή Γροθιά (Fist)** | `/looper/record` | **Toggle Rec/Play:** Με το 1ο κλείσιμο ξεκινάει η εγγραφή, με το 2ο κλείνει το loop και ξεκινά η αναπαραγωγή. | Πολύ ξεκάθαρο, δύσκολο να πατηθεί κατά λάθος. |
| **Ανοιχτή Παλάμη (Open Palm)** | `/looper/clear` | **Stop & Mute:** Σταματάει το loop και καθαρίζει το buffer. | Φυσική κίνηση «στοπ» που φαίνεται όμορφα και στη σκηνή. |
| **Δείκτης προς τα πάνω (Point Up)** | `/looper/overdub` | **Overdub:** Γράφει νέα φωνητικά στρώματα πάνω στο υπάρχον loop. | Επιτρέπει διαχωρισμό του βασικού ρυθμικού loop από τα harmonies. |


**Build music with movement. 🎵✨**
