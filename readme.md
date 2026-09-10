# Aeolus Avionics Task Round 2

This repository contains my submission for the Aeolus Avionics Task Round 2 (2026 batch).  
It includes solutions for Task 1 (Autonomous Architectures), Task 2 (Communication Architecture), and Task 3 (Propulsion System).

---

## Task 1: Autonomous Architectures

### Choice of Build
I selected **Build 2 (OAK-D Lite + Raspberry Pi 5)**.

### Justification
- **Compute:** Raspberry Pi 5 provides sufficient processing for depth data and AI tasks without excessive power draw.  
- **Power:** More efficient than Jetson Orin Nano, helping endurance stay above 12 minutes.  
- **Use Case:** Depth sensing is critical for search and rescue in stormy seas, allowing accurate obstacle detection and surface scanning.  
- **Weight:** Lightweight camera and Pi board keep total drone mass under the 2.5 kg limit.  
- **Cost:** Affordable compared to Jetson-based builds, making it practical for team deployment.

### Weighted Scoring
| Parameter | Weight | Score (1–10) | Weighted Value |
|-----------|--------|--------------|----------------|
| Compute   | 30%    | 8            | 2.4            |
| Power     | 25%    | 9            | 2.25           |
| Use Case  | 25%    | 9            | 2.25           |
| Weight    | 10%    | 8            | 0.8            |
| Cost      | 10%    | 7            | 0.7            |
| **Total** | 100%   | —            | **8.4 / 10**   |

### Bonus
- **Camera Orientation:** Forward-facing with a slight downward tilt to maximize visibility of the sea surface and obstacles.  
- **Alternate Build:** Build 4 (Stereo + Pi 5) for lighter weight, but it sacrifices depth accuracy compared to Build 2.

---

## Task 2: Communication Architecture

### Components
- **RC Transmitter/Receiver:** For manual override and control.  
- **Telemetry Module:** For sending flight data to ground station.  
- **VTX (Video Transmitter):** For live video feed.  

### Selection & Connections
- RC system: Digital transmitter/receiver (e.g., FrSky or Radiomaster) → connected via PWM/PPM/SBUS to Pixhawk 6C Mini.  
- Telemetry: 915 MHz digital telemetry module → UART port on Pixhawk.  
- VTX: 5.8 GHz digital video transmitter → powered from power distribution board, video input from camera.  

### Protocols & Ranges
- RC: 2.4 GHz, ~1–2 km range.  
- Telemetry: 915 MHz, ~1–5 km range depending on antenna.  
- VTX: 5.8 GHz, ~1 km range (line of sight).  

                ┌───────────────────────┐
                │   RC Transmitter       │
                └──────────┬────────────┘
                           │ 2.4 GHz
                           ▼
                ┌───────────────────────┐
                │   RC Receiver          │
                └──────────┬────────────┘
                           │ PWM/PPM/SBUS
                           ▼
                ┌───────────────────────┐
                │   Pixhawk 6C Mini      │
                └──────────┬────────────┘
        UART (TELEM)       │
 ┌───────────────────────┐ │
 │ Telemetry Module       │ │
 └──────────┬────────────┘ │
            │ 915 MHz       │
            ▼               │
   Ground Station Laptop    │
                            │
                            │
                            │ Video Input
                            ▼
                ┌───────────────────────┐
                │   Camera (Depth/Stereo)│
                └──────────┬────────────┘
                           │
                           ▼
                ┌───────────────────────┐
                │   VTX (Video TX)       │
                └──────────┬────────────┘
                           │ 5.8 GHz
                           ▼
                Ground Station Goggles/Monitor

Power Connections:
- RC Receiver + Telemetry Module → 5V rail from Pixhawk
- VTX → 12V rail from Power Distribution Board (PDB)


## Task 3: Propulsion System

### Motors & Propellers
- **Motors:** Holybro S500 V2 Motor 2216‑920KV‑CCW  
- **Propellers:** Pro‑Range Propellers 1045 (10×4.5)

### Battery Selection
- **Chosen Battery:** 4S LiPo, 6000 mAh, 40C discharge  
- **Reasoning:**  
  - 4S (14.8 V) matches motor KV rating for efficient thrust.  
  - 6000 mAh capacity balances endurance with weight (≈ 500–600 g).  
  - 40C discharge ensures sufficient current supply (~240 A max), well above required draw.

### ESC Selection
- **Chosen ESC:** 30A–40A ESCs (BLHeli‑S or equivalent)  
- **Reasoning:**  
  - Each motor draws ~10–12 A at hover, peak ~20 A.  
  - 30A ESC provides safe margin, 40A adds extra reliability.  
  - Compatible with 4S LiPo and supports smooth throttle response.

### Endurance Calculation
Hover Current per Motor: ~10–12 A

Total Current (4 motors): ~40–48 A

Battery Capacity: 6000 mAh = 6 Ah

Endurance:

Endurance
=
6
 Ah
48
 A
×
60
≈
7.5 minutes


  
- **Optimized Flight (lower throttle ~25–30 A):**  

6
 Ah
30
 A
×
60
≈
12
–
14 minutes

### Bonus
- **Alternative Motors:** Lower KV (~800 KV) brushless motors with higher efficiency can provide better thrust per watt, extending endurance without increasing weight.
