# 🎵 Vibemix-Studio

> **An interactive music studio controlled by hand gestures**

https://github.com/user-attachments/assets/b24ac466-168c-42a4-848d-6c32347708f5

Vibemix-Studio combines **real-time hand tracking** with **digital signal processing**, allowing you to use your hands to experiment with effects. Gestures detected through a camera are translated into OSC messages and mapped to audio parameters in a JUCE-based C++ engine.

---

## Features

### Real-Time Hand Tracking

- Hand and finger tracking powered by **MediaPipe** 
- Gesture recognition for pinch gesture, open/closed hand, peace sign etc.
- Parallel-palm detection for two-hand interaction
- Continuous hand openness and pinch-value control
- Live camera preview with annotated landmarks

### JUCE Audio Engine

- Real-time audio processing written in **C++**
- DSP effect concepts including low-pass filtering, delay, pitch shifting, and reverb
- Thread-safe communication between the OSC/network and audio threads

### Communication & Web Interface

- OSC/UDP communication between Python and C++
- FastAPI video streaming endpoint for the web application
- React/TypeScript frontend integration
- Real-time gesture visual feedback

---

## More audio effects to-be implemented


**Build music with movement. 🎵✨**
