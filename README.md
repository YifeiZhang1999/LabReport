# LabReport
This is the lab report for Satellite Communication and Navigation course

Here’s a clean and well-structured **README** version of your document content:

---

## GNSS Positioning Modes Analysis

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
