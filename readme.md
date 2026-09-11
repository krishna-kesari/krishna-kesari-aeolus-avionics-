# Aeolus Avionics Challenge – Round 2 🚀


---

## Task 1: Autonomous Architectures

### Choice of Build
I selected **Build 2 (OAK-D Lite + Raspberry Pi 5)**.

### Why This Build?
- **Compute:** Raspberry Pi 5 offers enough processing power for depth data and AI tasks without draining too much energy.  
- **Power:** More efficient than Jetson Orin Nano, which helps keep flight endurance above 12 minutes.  
- **Use Case:** Depth sensing is vital for search and rescue in stormy seas, enabling accurate obstacle detection and surface scanning.  
- **Weight:** Lightweight components keep the drone under the 2.5 kg limit.  
- **Cost:** More affordable than Jetson‑based builds, making it practical for team deployment.

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
- **Camera Orientation:** Forward‑facing with a slight downward tilt for maximum visibility of the sea surface and obstacles.  
- **Alternate Build:** Build 4 (Stereo + Pi 5) is lighter, but sacrifices depth accuracy compared to Build 2.  

---

## Task 2: Communication Architecture

### Components
- **RC Transmitter/Receiver:** For manual override and control.  
- **Telemetry Module:** Sends flight data to the ground station.  
- **VTX (Video Transmitter):** Provides live video feed.  

### Connections
- RC system: Digital transmitter/receiver (e.g., FrSky or Radiomaster) → connected via PWM/PPM/SBUS to Pixhawk 6C Mini.  
- Telemetry: 915 MHz digital telemetry module → UART port on Pixhawk.  
- VTX: 5.8 GHz digital video transmitter → powered from the power distribution board, video input from the camera.  

### Protocols & Ranges
- RC: 2.4 GHz, ~1–2 km range.  
- Telemetry: 915 MHz, ~1–5 km range depending on antenna.  
- VTX: 5.8 GHz, ~1 km range (line of sight).  

### Diagram (ASCII Placeholder)



<img width="555" height="370" alt="image" src="https://github.com/user-attachments/assets/9ab68c25-b36c-4c1f-ad54-91bc2ea23b0f" />






---

## Task 3: Propulsion System

### Motors & Propellers
- **Motors:** Holybro S500 V2 Motor 2216‑920KV‑CCW  
- **Propellers:** Pro‑Range Propellers 1045 (10×4.5)

### Battery Choice
- **4S LiPo, 6000 mAh, 40C discharge**  
- Matches motor KV rating for efficient thrust.  
- Provides a balance between endurance and weight (~500–600 g).  
- 40C discharge ensures ample current supply (~240 A max), far above required draw.

### ESC Choice
- **30A–40A ESCs (BLHeli‑S or equivalent)**  
- Each motor draws ~10–12 A at hover, peak ~20 A.  
- 30A ESCs provide safe margin; 40A adds extra reliability.  
- Fully compatible with 4S LiPo and supports smooth throttle response.

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
