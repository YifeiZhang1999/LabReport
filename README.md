# LabReport
This is the lab report for Satellite Communication and Navigation course

Here’s a clean and well-structured **README** version of your document content:

---

## 1. GNSS Positioning Modes Analysis

### Parameters Tuned

#### Positioning Mode Overview
Positioning Mode refers to the strategy used by a GNSS (Global Navigation Satellite System) receiver or algorithm to estimate a user's location. Different modes affect satellite data processing, correction methods, and achievable accuracy.

| Mode           | Description |
|----------------|-------------|
| **Single**     | Basic positioning using one GNSS receiver with broadcast satellite data. Accuracy is meter-level. Uses only pseudorange observations. |
| **DGPS/DGNSS** | Differential GNSS with pseudorange corrections from a known reference station. Sub-meter accuracy. |
| **Kinematic**  | Uses carrier-phase observations and differential corrections. Solves integer ambiguities for centimeter-level precision. |
| **Static**     | RTK mode for stationary receivers. Commonly used to establish base station positions. |
| **Static-Start** | Begins in static mode, then switches to kinematic post-initialization. Useful when starting from a rest position. |
| **Moving-Base** | Both rover and base stations are mobile. Used for relative positioning between two moving platforms. |
| **Fixed**      | Base station at a known, fixed location used to provide RTK corrections. |
| **PPP Kinematic** | Precise Point Positioning for moving receivers, requiring precise satellite data but no nearby base station. |
| **PPP Static** | Static version of PPP for long-term, high-accuracy fixed-point positioning. |
| **PPP Fixed**  | PPP with integer-fixed carrier-phase ambiguities for improved accuracy. |

---

### Results

#### Urban Dataset

<p align="center">
  <img src="images/1.png" alt="GNSS lat/lon tracking result" width="300" />
  <img src="images/2.png" alt="GNSS estimation error" width="300" />
</p>

##### GNSS Track Comparison

A comparative figure (not included here) shows GNSS tracks overlaid on an OpenStreetMap basemap for various positioning modes.

- **Missing Results**: PPP Kinematic, PPP Static, and PPP Fixed modes failed to generate outputs—likely due to missing precise satellite data or inadequate quality (e.g., no dual-frequency phase observations).
- **Top Performer**: **Kinematic mode** delivered the most accurate trajectory, aligning closely with the road network and maintaining minimal deviation.
- **Worst Performer**: **Static mode** diverged significantly. Since it assumes a stationary receiver, it fails when applied to a dynamic dataset (e.g., walking or driving), resulting in poor ambiguity resolution and unrealistic estimates.

> **Kinematic mode Q-values**:  
> Q = 2 (float solution) in **20.85%** of observations — higher than all other modes.

---

##### Mode Comparison Across Urban Scenario

A second figure compares positioning performance across five modes: **DGPS, Kinematic, Single, Static-start, and Static**.

- **Kinematic Mode**:
  - Most accurate and stable.
  - Closely follows road boundaries and forms a clear loop.
  - **Q=1 (fixed)**: 44.88%, **Q=2 (float)**: 21.46%, **Total (Q=1 or Q=2)**: 66.34%
- **Static Mode**:
  - Displays chaotic patterns near the start.
  - Assumes stationarity—unsuitable for movement data.
- **Single Mode**:
  - Smoother than Static but less accurate.
  - 100% Q=3 (pseudorange-only), meter-level accuracy.
- **DGPS Mode**:
  - Consistently Q=4 (differential corrections only), no phase ambiguity resolution.
  - Sub-meter level accuracy, suitable for moderate-precision tasks.

Here’s your content reformatted into a clean and structured **README.md** format using Markdown:

---

## 2.

### Overview

This document presents the results of parameter tuning in a GNSS positioning experiment under the **PPP Kinematic mode**. Two primary parameters were tested:

1. **Frequencies**
2. **Filter Type**

---

### 1. Frequencies

#### Overview of GPS Frequency Bands

- **L1 (1575.42 MHz):** Public C/A code + military P(Y) code.
- **L2 (1227.60 MHz):** Originally military-only, now includes civilian L2C.
- **L5 (1176.45 MHz):** High-precision civilian use (e.g., aviation, railways).
- **L3 (1381.05 MHz):** Used for nuclear monitoring.
- **L4 (1379.913 MHz):** Experimental, for ionospheric studies.
- **L6 (1278.75 MHz):** Used by augmentation systems like Japan’s QZSS.

**Galileo Frequencies:**
- **E5a & E5b:** Used by the EU’s Galileo system; E5a matches GPS L5.

#### Frequency Options in Lab

- L1
- L1 + L2/E5b
- L1 + L2/E5b + L5/E5a
- L1 + L2/E5b + L5/E5a + L6

> Note: When selecting one frequency option, other configurations are left at default settings.

#### Results

##### L1 Only
- Achieved **highest positioning accuracy**.
<p align="center">
  <img src="images/3.png" alt=" " width="500" />
</p>

##### L1 + L2/E5b
- Slightly lower accuracy than L1-only.

<p align="center">
  <img src="images/4.png" alt=" " width="500" />
</p>

##### L1 + L2/E5b + L5/E5a
- Comparable to above, but still slightly lower than L1-only.

<p align="center">
  <img src="images/5.png" alt=" " width="500" />
</p>

#### L1 + L2/E5b + L5/E5a + L6
- Similar accuracy, slightly lower than L1-only.

<p align="center">
  <img src="images/6.png" alt=" " width="500" />
</p>

#### Conclusion

While multi-frequency modes should theoretically outperform single-frequency setups, in this case, **L1-only yielded the best accuracy**. Possible reasons include:

- Data quality
- Satellite geometry
- Software processing settings
- Convergence time

---

### 2. Filter Type

#### Filter Types Tested

- **Forward Filtering**  
  Processes data chronologically. Common in real-time applications.

- **Backward Filtering**  
  Processes data in reverse. Useful in post-processing for refining accuracy.

- **Combined Filtering**  
  Merges forward and backward filtering for highest accuracy (post-processing only).

#### Results (Under PPP Kinematic mode, using L1 Frequencies)

##### Forward Filter
- Standard accuracy with initial convergence limitations.

<p align="center">
  <img src="images/7.png" alt=" " width="500" />
</p>

##### Backward Filter
- Improved accuracy over forward filtering.

<p align="center">
  <img src="images/8.png" alt=" " width="500" />
</p>

##### Combined Filter
- **Highest positioning accuracy**.
- Benefits:
  - Corrects convergence issues.
  - Smooths out noise.
  - Resolves ambiguities more effectively.
 
<p align="center">
  <img src="images/9.png" alt=" " width="500" />
</p>

---

### Final Notes

The study showed that:
- **L1-only frequency** provided the **best results** in this particular PPP Kinematic context.
- **Combined filtering** is the **most accurate filtering strategy**.

These outcomes highlight how parameter tuning can lead to unexpected yet insightful results in GNSS processing.

Absolutely! Here's the **English version** of the README with **image placeholders** included so you can easily plug in plots or diagrams later:

---

## 3.

### 🛠️ Parameters Tuned

#### Elevation Mask / SNR Mask

- **Elevation Mask**: Minimum satellite elevation angle (range: 0°–70°, step: 5°).
- **SNR Mask**: Minimum Signal-to-Noise Ratio (SNR) threshold to filter out weak or noisy satellite signals.

> Proper adjustment of these masks can help improve GNSS signal quality and positioning accuracy.

<p align="center">
  <img src="images/10.png" alt=" " width="500" />
</p>
---

#### Rec Dynamics / Earth Tides Correction

- **Rec Dynamics**: Corrects for motion of the receiver (velocity, acceleration, rotation).
- **Earth Tides Correction**:
  - **OFF**: No correction
  - **Solid**: Corrects for solid Earth deformation due to tidal forces
  - **Solid/OTL**: Adds Ocean Tide Loading for coastal/ocean regions

> These corrections help improve precision, especially in dynamic or high-accuracy environments.

<p align="center">
  <img src="images/11.png" alt=" " width="500" />
</p>

---

### Accuracy Evaluation Metrics

#### 1. Position Quality Indicator (Q)

| Q Value | Description                        | Accuracy Level     |
|---------|------------------------------------|--------------------|
| 1       | Fixed RTK                          | Centimeter-level   |
| 2       | Float RTK                          | Decimeter-level    |
| 3       | SBAS                               | 1–3 meters         |
| 4       | DGPS                               | 0.5–3 meters       |
| 5       | Single GNSS                        | 3–50 meters        |
| 6       | PPP (Precise Point Positioning)    | Centimeter–Decimeter |

> Q=1 is best, Q=2 is acceptable, Q=4 or higher indicates lower accuracy.

<p align="center">
  <img src="images/12.png" alt=" " width="500" />
</p>

---

#### 2. RMSE (Root Mean Square Error)

Used to compare GNSS trajectory results against ground truth from the dataset.

<p align="center">
  <img src="images/13.png" alt=" " width="500" />
</p>

---

### Impact of Parameter Changes

#### Elevation Mask / SNR Mask

##### Urban Dataset

- Elevation Mask from **25°–35°** improved Q=1 significantly.
- Higher than 50° caused Q=2 to drop sharply due to fewer visible satellites.

##### Dynamic Dataset

- Lower Elevation Masks (0°–15°) maintain more stable Q=1 and Q=2.
- Higher masks remove noisy signals but reduce available satellites, hurting accuracy.

<p align="center">
  <img src="images/14.png" alt=" " width="500" />
</p>
---

#### Rec Dynamics / Earth Tides Correction

- Enabling these corrections greatly improved **Q=2** results.
- **Q=4** remained largely unaffected.

<p align="center">
  <img src="images/15.png" alt=" " width="500" />
</p>

---

###  Analysis & Recommendations

#### Elevation Mask / SNR Mask

- Recommended Elevation Mask: **10°–15°**
- This provides a good balance between satellite count and signal quality.

#### Rec Dynamics & Earth Tides Correction

- Should be enabled in **dynamic environments** or **high-precision applications**.
- Major improvements observed in Q=2 when these are turned ON.

---

### Conclusion

Careful tuning of Elevation Mask, SNR Mask, and enabling dynamic corrections (Rec Dynamics + Earth Tides) can significantly enhance the accuracy and stability of GNSS positioning in varying environmental conditions.

---

Would you like me to save this as a downloadable `.md` file for you? Or would you like help inserting actual images into this layout?

