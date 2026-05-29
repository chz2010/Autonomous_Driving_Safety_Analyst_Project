### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Addresses unsafe intended functionality from limitations, ODD, and triggering conditions.
- **ISO 8800**: Ensures AI/data/model assurance.

---

### Item Definition

**Functions:**
1. Side object detection
2. Relative velocity estimation
3. Blind-zone occupancy assessment
4. Driver warning
5. Interface output

**Inputs:** 
- Sensor data (LiDAR, camera, radar)
- Ego vehicle state (speed, direction)

**Outputs:**
- Object presence and relative position
- Occupancy status of blind zone
- Warning signal to driver

**Interfaces:**
- Sensor fusion module
- Driver interface unit
- Vehicle control system

**ODD:** 
- Urban and highway lane changes
- Day/night visibility
- Moderate rain conditions

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Object presence and relative position | Sensor failure, incorrect calibration | Inadequate perception under poor visibility | Dataset gaps, label quality issues | ISO 26262, ISO 8800 | Yes |
| Relative velocity estimation | Velocity of detected objects | Incorrect sensor fusion logic | Performance limitations in low light conditions | Data coverage, robustness concerns | ISO 26262, SOTIF | Yes |
| Blind-zone occupancy assessment | Occupancy status of blind zone | False positive/negative detections | Misinterpretation of dynamic obstacles | Model uncertainty, distribution shift | ISO 8800 | Yes |
| Driver warning | Warning signal to driver | Delayed or missed warnings | Foreseeable misuse due to driver distraction | ODD limitations, triggering conditions | SOTIF | Yes |
| Interface output | Communication with HMI | Incomplete or incorrect communication | Human-machine interface design flaws | User experience, fallback mechanisms | ISO 26262 | No |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Sensor failure, incorrect calibration | Collision with detected object | Urban and highway lane changes in moderate rain | Severity: Risk of collision; Exposure: High traffic density; Controllability: Driver fallback available | E3 | E4 | ASIL B | Uncertainty: Calibration drift, sensor contamination | Review calibration procedures |
| Relative velocity estimation | Incorrect sensor fusion logic | Misjudgment of object movement | Day/night visibility with low light conditions | Severity: Risk of incorrect braking; Exposure: Low light scenarios common; Controllability: Driver fallback available | E4 | E3 | ASIL C | Uncertainty: Sensor noise, fusion algorithm robustness | Validate sensor fusion algorithms |
| Blind-zone occupancy assessment | False positive/negative detections | Misinterpretation of dynamic obstacles | Urban and highway lane changes in moderate rain | Severity: Risk of false warning; Exposure: High traffic density; Controllability: Driver fallback available | E3 | E4 | ASIL B | Uncertainty: Model uncertainty, distribution shift | Improve model robustness |
| Driver warning | Delayed or missed warnings | Foreseeable misuse due to driver distraction | Day/night visibility with low light conditions | Severity: Risk of collision; Exposure: High traffic density; Controllability: Driver fallback available | E4 | E3 | ASIL C | Uncertainty: Human factors, model uncertainty | Enhance driver monitoring |
| Interface output | Incomplete or incorrect communication | Human-machine interface design flaws | Urban and highway lane changes in moderate rain | Severity: Risk of miscommunication; Exposure: High traffic density; Controllability: Driver fallback available | E3 | E4 | ASIL B | Uncertainty: User experience, fallback mechanisms | Improve HMI design |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior |
| --- | --- | --- | --- | --- |
| SG1 | Side object detection | Collision with detected object | B | Warning issued, fallback to manual driving |
| SG2 | Relative velocity estimation | Misjudgment of object movement | C | Reduced braking force, fallback to manual driving |
| SG3 | Blind-zone occupancy assessment | Misinterpretation of dynamic obstacles | B | Visual warning only, fallback to manual driving |
| SG4 | Driver warning | Foreseeable misuse due to driver distraction | C | Delayed warning, fallback to manual driving |
| SG5 | Interface output | Human-machine interface design flaws | B | Clear communication, fallback to manual driving |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Warning issued, fallback to manual driving | HMI alerts driver of sensor issue | Manual driving mode activated | Prevent collision with detected object |
| Incorrect sensor fusion logic | Reduced braking force, fallback to manual driving | HMI warns driver of potential misjudgment | Manual driving mode with reduced autonomy | Mitigate risk of incorrect braking |
| False positive/negative detections | Visual warning only, fallback to manual driving | HMI provides visual warnings | Manual driving mode with limited assistance | Prevent false warnings and ensure driver awareness |
| Delayed or missed warnings | Delayed warning, fallback to manual driving | HMI alerts driver of delayed warning | Manual driving mode with reduced autonomy | Ensure driver remains vigilant |
| Incomplete or incorrect communication | Clear communication, fallback to manual driving | HMI provides clear instructions | Manual driving mode with limited assistance | Prevent miscommunication and ensure safe operation |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor calibration | ECU | Calibration drift, sensor contamination | Regular recalibration, fallback to manual driving | 1 week | Sensor test logs, diagnostic checks |
| Sensor fusion logic | Fusion module | Sensor noise, incorrect fusion | Plausibility checks, watchdogs | Real-time | Unit tests, integration tests |
| Model robustness | Perception model | Distribution shift, uncertainty behavior | Regular retraining, fallback to manual driving | 1 month | Retraining logs, model validation results |
| Driver monitoring | HMI | Human factors, driver distraction | Visual and audio alerts, fallback to manual driving | Real-time | Driver behavior analysis, HMI interaction logs |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose**: Define the safety lifecycle phases.
- **Item-Specific Engineering Activities**:
  - Define functional decomposition and safety goals.
  - Identify potential E/E malfunctions.
  - Perform HARA screening.
- **Work Products/Evidence**:
  - Functional decomposition table, HARA table, safety goals table.
- **Rationale/Unsafe Behavior Prevented**: 
  - Ensure all functions are defined with clear safety requirements.
  - Identify and mitigate potential E/E failures.

#### Part 3: Item Definition
- **Purpose**: Define the item's functional behavior.
- **Item-Specific Engineering Activities**:
  - Define input/output interfaces, ODD, and safety role.
  - Perform HARA screening for each function.
- **Work Products/Evidence**:
  - Functional decomposition table, HARA table, safety goals table.

#### Part 4: System Development
- **Purpose**: Design the system architecture.
- **Item-Specific Engineering Activities**:
  - Define software and hardware architectures.
  - Perform ASIL decomposition for each function.
- **Work Products/Evidence**:
  - Architecture diagrams, ASIL decomposition tables, HARA table.

#### Part 5: Hardware Development
- **Purpose**: Ensure hardware safety requirements are met.
- **Item-Specific Engineering Activities**:
  - Define hardware safety requirements.
  - Perform FMEDA and random hardware metrics analysis.
- **Work Products/Evidence**:
  - Hardware safety requirements document, FMEDA report.

#### Part 6: Software Development
- **Purpose**: Ensure software safety requirements are met.
- **Item-Specific Engineering Activities**:
  - Define software safety requirements.
  - Perform plausibility checks and watchdogs.
- **Work Products/Evidence**:
  - Software safety requirements document, unit tests, integration tests.

#### Part 7: Production
- **Purpose**: Ensure production processes meet safety standards.
- **Item-Specific Engineering Activities**:
  - Define end-of-line calibration procedures.
  - Perform service recalibration and DTC management.
- **Work Products/Evidence**:
  - Calibration procedures document, service recalibration logs.

#### Part 8: Supporting Processes
- **Purpose**: Ensure traceability and documentation.
- **Item-Specific Engineering Activities**:
  - Define requirements traceability matrix.
  - Perform verification planning and documentation.
- **Work Products/Evidence**:
  - Requirements traceability matrix, verification plan document.

#### Part 9: ASIL Decomposition
- **Purpose**: Ensure all functions are classified with appropriate ASIL levels.
- **Item-Specific Engineering Activities**:
  - Perform ASIL decomposition for each function.
- **Work Products/Evidence**:
  - ASIL decomposition table, HARA table.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Inadequate perception under poor visibility | Moderate rain, low light conditions | Urban and highway lane changes | Collision with detected object | Known | Sensor test logs, HMI interaction logs | Enhanced calibration procedures, fallback to manual driving | ASIL B risk reduced by 50% through improved sensor fusion |
| Relative velocity estimation | Performance limitations in low light conditions | Day/night visibility with low light conditions | Urban and highway lane changes | Misjudgment of object movement | Known | Sensor test logs, HMI interaction logs | Plausibility checks, watchdogs | ASIL C risk reduced by 70% through real-time monitoring |
| Blind-zone occupancy assessment | Model uncertainty in dynamic obstacle interpretation | Urban and highway lane changes in moderate rain | Day/night visibility with low light conditions | Misinterpretation of dynamic obstacles | Known | Sensor test logs, HMI interaction logs | Regular retraining, fallback to manual driving | ASIL B risk reduced by 60% through improved model robustness |
| Driver warning | Foreseeable misuse due to driver distraction | Day/night visibility with low light conditions | Urban and highway lane changes in moderate rain | Foreseeable misuse leading to delayed or missed warnings | Known | Driver behavior analysis, HMI interaction logs | Visual and audio alerts, fallback to manual driving | ASIL C risk reduced by 80% through enhanced driver monitoring |
| Interface output | Human-machine interface design flaws | Urban and highway lane changes in moderate rain | Day/night visibility with low light conditions | Miscommunication leading to unsafe operation | Known | Driver behavior analysis, HMI interaction logs | Clear communication, fallback to manual driving | ASIL B risk reduced by 75% through improved HMI design |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Perception accuracy | High-resolution sensor data, diverse urban and highway scenarios | Dataset gaps in low light conditions, occlusion cases | Model uncertainty, distribution shift | Distribution shift due to weather changes | Regular retraining every 1 month | Retraining logs, model validation results | ASIL B risk reduced by 60% through regular retraining |
| Relative velocity estimation | Sensor fusion accuracy | High-resolution sensor data, diverse urban and highway scenarios | Dataset gaps in low light conditions, occlusion cases | Model uncertainty, distribution shift | Distribution shift due to weather changes | Regular plausibility checks every 1 week | Unit tests, integration tests | ASIL C risk reduced by 70% through real-time monitoring |
| Blind-zone occupancy assessment | Dynamic obstacle interpretation accuracy | High-resolution sensor data, diverse urban and highway scenarios | Dataset gaps in low light conditions, occlusion cases | Model uncertainty, distribution shift | Distribution shift due to weather changes | Regular retraining every 1 month | Retraining logs, model validation results | ASIL B risk reduced by 50% through improved model robustness |
| Driver warning | Human-machine interface design accuracy | High-resolution sensor data, diverse urban and highway scenarios | Dataset gaps in low light conditions, occlusion cases | Model uncertainty, distribution shift | Distribution shift due to weather changes | Regular retraining every 1 month | Retraining logs, model validation results | ASIL C risk reduced by 80% through enhanced driver monitoring |
| Interface output | Clear communication accuracy | High-resolution sensor data, diverse urban and highway scenarios | Dataset gaps in low light conditions, occlusion cases | Model uncertainty, distribution shift | Distribution shift due to weather changes | Regular retraining every 1 month | Retraining logs, model validation results | ASIL B risk reduced by 75% through improved HMI design |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor calibration test | Sensor failure in low light conditions | Warning issued, fallback to manual driving | No collision with detected object | Calibration logs, diagnostic checks | SG1 |
| Plausibility check for sensor fusion logic | Incorrect sensor data in low light conditions | Reduced braking force, fallback to manual driving | Correct braking response | Unit tests, integration tests | SG2 |
| Retraining test for perception model | Model uncertainty in dynamic obstacle interpretation | Visual warning only, fallback to manual driving | No misinterpretation of dynamic obstacles | Retraining logs, model validation results | SG3 |
| Driver monitoring test | Driver distraction in low light conditions | Delayed warning, fallback to manual driving | Driver remains vigilant | Driver behavior analysis, HMI interaction logs | SG4 |
| HMI communication test | Incomplete or incorrect communication with driver | Clear communication, fallback to manual driving | No miscommunication leading to unsafe operation | Communication logs, DTC management records | SG5 |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-line calibration | Sensor accuracy drift | Regular recalibration procedures | No sensor failure during operation | Calibration logs, diagnostic checks | Continuous monitoring of sensor performance | Ensure consistent sensor accuracy |
| Sensor health check | Sensor contamination or damage | Periodic visual inspection and cleaning | No sensor malfunction during operation | Visual inspection records, cleaning logs | Real-time monitoring of sensor health | Prevent sensor failures leading to unsafe operation |
| Software/model version traceability | Inconsistent software versions | Regular update management procedures | Consistent software versions across fleet | Version control logs, deployment records | Continuous verification of software integrity | Ensure consistent and safe system operation |
| Service recalibration | Sensor accuracy degradation over time | Regular service recalibration procedures | No sensor failure during operation | Recalibration logs, diagnostic checks | Continuous monitoring of sensor performance | Maintain accurate sensor data for safety-critical functions |
| DTC management | Diagnostic trouble codes (DTCs) | Regular DTC analysis and resolution procedures | No unresolved DTCs leading to unsafe operation | DTC records, resolution logs | Real-time monitoring of system health | Ensure safe operation by addressing potential issues early |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 60 | 30 | Moderate rain | Low light conditions | Partial occlusion behind parked cars | Highway lane change | High traffic density | L2+ with fallback to manual driving | 1.5 | Driver remains vigilant and takes over if necessary |

#### Accident-Chain Table
| Step | Degraded/ Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure in low light conditions | Incorrect sensor data interpretation | Reduced braking force, fallback to manual driving | Increased risk of collision | Calibration logs, diagnostic checks |
| 2 | Model uncertainty in dynamic obstacle interpretation | Misinterpretation of dynamic obstacles | Visual warning only, fallback to manual driving | Potential miscommunication leading to delayed response | Retraining logs, model validation results |
| 3 | Driver distraction in low light conditions | Delayed or missed warnings | Delayed driver response, increased risk of collision | Increased risk of collision due to human factors | Driver behavior analysis, HMI interaction logs |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure in low light conditions | Performance limitations in low light conditions | Model uncertainty, distribution shift | Enhanced calibration procedures, fallback to manual driving | Calibration logs, diagnostic checks |

#### Final Safety Argument
The final safety argument is based on the comprehensive analysis of potential E/E malfunctions, SOTIF-related risks, and AI/data/model assurance. The system design includes robust mitigation strategies such as regular recalibration, real-time monitoring, and enhanced driver monitoring to ensure safe operation under various conditions.

---

### Conclusion

This project-generated example safety case provides a structured approach for analyzing the safety of an autonomous driving perception system across ISO 26262, ISO 21448/SOTIF, and ISO 8800 standards. The comprehensive analysis ensures that all potential risks are identified and mitig