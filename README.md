# DJ System with OSC Controller and Pure Data

## Team Members
- **Rui Yu Lei Wu**
- **Juan David Bernal**

---

## Project Overview

This project implements an interactive DJ system using **OSC Controller** (Open Sound Control) and **Pure Data (PD)**. The system allows real-time electronic music creation through multiple control interfaces, combining algorithmic sound generation, MIDI synthesis, FM modulation, and interactive rhythm patterns.

---

## System Architecture

### Technology Stack
- **OSC Controller App**: Mobile interface for real-time control
- **Pure Data (PD)**: Audio processing and synthesis engine
- **OSC Protocol**: Communication between controller and audio engine

---

## Page Descriptions

### **P1 - Recording Control and Effects**

#### 4 Sliders:
1. **Slider 1**: Controls volume of Toggle 1 (algorithmic sound)
2. **Slider 2**: Controls volume of Toggle 2 (algorithmic sound)
3. **Slider 3**: Controls volume of Toggle 3 (algorithmic sound) and Grid Button 24
4. **Slider 4**: Controls frequency of Grid Button 24

#### 3 Switches (ON/OFF):
- **Toggle 1**: Activates algorithmic sound generator 1
- **Toggle 2**: Activates algorithmic sound generator 2
- **Toggle 3**: Activates algorithmic sound generator 3

#### 3 Buttons:
- **Button 1**: Krell Music generative sound
- **Button 2**: MIDI noteout sound
- **Button 3**: MIDI noteout sound

**Function**: This page serves as the main control hub for recording, volume management, and algorithmic sound generation. The three toggles trigger algorithmically generated sounds, while sliders control their individual volumes and parameters.

---

### **P2 - Advanced Modulation (FM Synthesis)**

#### 2 Control Axes:
- **Y-Axis (Frequency)**: Adjusts the carrier frequency for FM synthesis, changing the pitch
- **X-Axis (Amplitude)**: Modifies the modulation depth, affecting timbre and harmonic content

**Function**: This page features an FM (Frequency Modulation) synthesis engine controlled by a 2D touch interface. Users can explore complex timbres by manipulating carrier and modulator parameters in real-time.

---

### **P3 - Rhythm Base Management (Grid Buttons)**

#### 24 Switches organized in a 4x6 grid:
- **Structure**: 4 columns × 6 percussion instruments per column
- **Function**: Step sequencer for creating rhythmic patterns
  - Each switch represents a time step in the sequence
  - Activating a switch triggers the corresponding instrument at that time position
  - All sounds are **algorithmically generated**
  - Patterns loop continuously until modified by the user

**Instruments**: 6 different percussion sounds (kick, snare, hi-hat, clap, tom, cymbal)

---

### **P4 - Sound Management (Piano and Sound Effects)**

#### 24 Buttons organized in 2 groups:

**Group 1 - Piano Sounds (12 buttons)**:
- Each button triggers a specific piano note via **MIDI noteout**
- Chromatic scale arrangement for melodic performance

**Group 2 - Sound Effects (12 buttons)**:
- Each button activates a specific sound effect via **MIDI noteout**
- Variety of electronic and percussive timbres

**Function**: Performance page for melodic and textural elements, all generated through MIDI synthesis.

---

## Technical Implementation

### Sound Generation Methods:

1. **Algorithmic Synthesis** (P1 - Toggles, P3 - Grid):
   - Generative algorithms
   - Mathematical functions (cos~, sin~, sqrt~)
   - Dynamic parameter modulation
   - Pure Data native synthesis

2. **FM Synthesis** (P2):
   - Carrier and modulator oscillators
   - Real-time modulation index control
   - 2D touch interface mapping

3. **MIDI Synthesis** (P1 - Buttons 2 & 3, P4):
   - noteout~ objects
   - MIDI note generation
   - External synthesizer routing

4. **Krell Music** (P1 - Button 1):
   - Generative ambient music technique
   - Random note generation within scales
   - Evolving textures

---

## OSC Communication

### Message Format:
```
/page1/slider1 [float 0-1]
/page1/toggle1 [int 0-1]
/page1/button1 [int 1]
/page2/xy [float x, float y]
/page3/grid/1/1 [int 0-1]
/page4/button1 [int 1]
```

### Pure Data Routing:
- `[oscparse]` object for message reception
- `[routeOSC]` for address filtering
- Individual handlers for each control element

---

## Features

✅ **Real-time Control**: All parameters respond immediately to OSC messages

✅ **Multiple Synthesis Methods**: Algorithmic, FM, and MIDI generation

✅ **Step Sequencer**: 24-step grid for rhythm pattern creation

✅ **Performance Interface**: Piano keys and sound effects for live performance

✅ **Volume Control**: Individual level management for each sound source

✅ **Frequency Modulation**: Dynamic pitch and timbre control

---

## Project Requirements

### Constraints:
- ✅ Use OSC Controller and Pure Data
- ✅ Utilize different OSC interactions (sliders, buttons, toggles, XY pads)
- ✅ All interactions must affect audio in PD
- ✅ Video demonstration (max 5 minutes) uploaded to YouTube

---

## Project Timeline

- **Preliminary Delivery**: October 24th - Progress presentation
- **Final Delivery & Presentation**: November 1st - Complete project and demonstration

---

## Setup Instructions

### Requirements:
1. Pure Data (Pd-extended or Purr Data recommended)
2. OSC Controller app (iOS/Android)
3. Computer and mobile device on the same network

### Installation:
1. Open the Pure Data patch `dj_system.pd`
2. Launch OSC Controller app on mobile device
3. Configure OSC output to computer's IP address
4. Set port to `8000` (or as configured in PD patch)
5. Verify DSP is enabled in Pure Data (Media → Audio ON)

### Configuration:
```
Pure Data patch receives on: 0.0.0.0:8000
OSC Controller sends to: [YOUR_COMPUTER_IP]:8000
```

---

## Usage Guide

### Basic Workflow:
1. **Start with P1**: Activate toggles for algorithmic background textures
2. **Add rhythm with P3**: Create drum patterns using the grid sequencer
3. **Modulate with P2**: Add FM synthesis sounds via XY pad
4. **Perform with P4**: Play melodies and effects using button pads

### Live Performance Tips:
- Use sliders 1-3 to balance algorithmic sound levels
- Adjust slider 4 to change rhythm sequence frequency
- Combine multiple pages for complex arrangements
- Use P1 buttons for accents and transitions

---

## Video Demonstration

📹 **YouTube Demo**: [Link to be added]

The demonstration video showcases:
- All four pages in action
- Real-time control manipulation
- Live music creation process
- Audio output examples

---

## Technical Details

### Pure Data Objects Used:
- `[oscparse]`, `[routeOSC]` - OSC communication
- `[osc~]`, `[cos~]`, `[sin~]` - Algorithmic synthesis
- `[mtof]`, `[noteout]` - MIDI generation
- `[metro]`, `[random]` - Rhythm generation
- `[*~]`, `[+~]` - Signal processing
- `[throw~]`, `[catch~]` - Audio routing
- `[writesf~]`, `[readsf~]` - Recording capabilities

### Audio Signal Flow:
```
OSC Input → PD Processing → Synthesis/MIDI → Audio Output
                ↓
         [dac~] / External Synth
```

---

## Limitations & Considerations

- Network latency may affect real-time response
- MIDI noteout requires external synthesizer or sound bank
- Grid sequencer timing depends on metro object accuracy
- FM synthesis CPU intensive at high modulation rates

---

## Future Improvements

- [ ] Add effects chain (reverb, delay, distortion)
- [ ] Implement recording and looping functionality
- [ ] Add preset saving/loading system
- [ ] Expand grid sequencer to 32 or 64 steps
- [ ] Include visual feedback in Pure Data interface

---

## Acknowledgments

This project was developed as part of an electronic music and interactive systems course, exploring the creative possibilities of OSC communication and Pure Data for live electronic music performance.

---



## Contact

For questions or collaboration:
- Rui Yu Lei Wu
- Juan David Bernal

