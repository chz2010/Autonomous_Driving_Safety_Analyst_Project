### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Addresses unsafe intended functionality from limitations, ODD, and triggering conditions.
- **ISO 8800**: Ensures AI/data/model assurance.

---

### Item Definition

**Functions:**
1. Cyclist detection
2. Posture classification
3. Trajectory prediction
4. Occlusion handling
5. AEB/planning interface output

**Inputs:** 
- Camera sensor data
- LiDAR sensor data (if applicable)
- Radar sensor data (if applicable)

**Outputs:**
- Cyclist presence and position
- Cyclist posture (e.g., standing, sitting)
- Trajectory prediction for cyclists
- Occlusion status
- AEB/planning interface signals

**Interfaces:** 
- Camera input/output to perception module
- LiDAR/Radar input/output to perception module
- Planning/AEB system output

**ODD:**
- Urban intersections
- Bike lanes
- Nighttime (low visibility)
- Rainy conditions
- Glare conditions
- Partial occlusion scenarios

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Cyclist detection | Presence and position | Sensor failure, false negatives | Inadequate cyclist detection under low visibility or occlusion | Dataset gaps in cyclist scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |
| Posture classification | Posture status (standing/sitting) | Model misclassification due to occlusion or poor lighting | Misclassification of cyclists as non-cyclists under low visibility | Dataset gaps in cyclist posture scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |
| Trajectory prediction | Predicted trajectory | Inaccurate prediction due to sensor noise | Inadequate handling of dynamic traffic conditions | ODD limitations and triggering conditions | ISO 26262, SOTIF, ISO 8800 | Yes |
| Occlusion handling | Occlusion status | Failure to detect occlusions | Insufficient handling of occlusions in complex urban environments | Dataset gaps in occlusion scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |
| AEB/planning interface output | Safety signals for AEB and planning systems | Malfunctioning safety signals | Inadequate coordination with other vehicles or infrastructure under dynamic conditions | ODD limitations and triggering conditions | ISO 26262, SOTIF, ISO 8800 | Yes |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cyclist detection | Sensor failure, false negatives | Collision with cyclist | Urban intersection at 30 km/h | Ego speed: 30-50 km/h; Object speed: 15-20 km/h | Severity: High - Risk of severe injury or fatality. | Exposure: Moderate - Common in urban areas during daytime and nighttime. | Controllability: Low - Driver fallback is limited due to high traffic density. | ASIL C | Uncertain - Need more data on cyclist detection performance. | Further HARA refinement needed. |
| Posture classification | Model misclassification | Misidentification of cyclist as pedestrian | Nighttime, low visibility | Ego speed: 30-50 km/h; Object speed: 15-20 km/h | Severity: High - Risk of collision with cyclists mistaken for pedestrians. | Exposure: Moderate - Common in urban areas during nighttime and rainy conditions. | Controllability: Low - Driver fallback is limited due to low visibility. | ASIL C | Uncertain - Need more data on cyclist posture classification performance. | Further HARA refinement needed. |
| Trajectory prediction | Inaccurate prediction | Collision with cyclist | Urban intersection at 30 km/h | Ego speed: 30-50 km/h; Object speed: 15-20 km/h | Severity: High - Risk of severe injury or fatality. | Exposure: Moderate - Common in urban areas during daytime and nighttime. | Controllability: Low - Driver fallback is limited due to high traffic density. | ASIL C | Uncertain - Need more data on trajectory prediction performance. | Further HARA refinement needed. |
| Occlusion handling | Failure to detect occlusions | Collision with cyclist behind parked cars or buses | Urban intersection at 30 km/h | Ego speed: 30-50 km/h; Object speed: 15-20 km/h | Severity: High - Risk of severe injury or fatality. | Exposure: Moderate - Common in urban areas during daytime and nighttime. | Controllability: Low - Driver fallback is limited due to high traffic density. | ASIL C | Uncertain - Need more data on occlusion handling performance. | Further HARA refinement needed. |
| AEB/planning interface output | Malfunctioning safety signals | Collision with cyclist | Urban intersection at 30 km/h | Ego speed: 30-50 km/h; Object speed: 15-20 km/h | Severity: High - Risk of severe injury or fatality. | Exposure: Moderate - Common in urban areas during daytime and nighttime. | Controllability: Low - Driver fallback is limited due to high traffic density. | ASIL C | Uncertain - Need more data on AEB/planning interface performance. | Further HARA refinement needed. |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| G1 | Cyclist detection | Collision with cyclist | C | Presence and position of cyclists accurately detected. | ISO 26262, SOTIF, ISO 8800 |
| G2 | Posture classification | Misidentification of cyclist as pedestrian | C | Correctly classify cyclist posture (standing/sitting). | ISO 26262, SOTIF, ISO 8800 |
| G3 | Trajectory prediction | Collision with cyclist | C | Accurate prediction of cyclist trajectory. | ISO 26262, SOTIF, ISO 8800 |
| G4 | Occlusion handling | Collision with cyclist behind parked cars or buses | C | Detect and handle occlusions effectively. | ISO 26262, SOTIF, ISO 8800 |
| G5 | AEB/planning interface output | Malfunctioning safety signals | C | Properly communicate safety signals to AEB and planning systems. | ISO 26262, SOTIF, ISO 8800 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure in cyclist detection | Fail-safe mode with reduced AEB activation. | HMI warning to driver about potential sensor issues. | Reduced functionality but no harm. | Ensures safety while maintaining system availability. |
| Model misclassification in posture classification | HMI warning and manual override for critical situations. | Driver intervention required for safe operation. | Degraded mode with reduced performance. | Mitigates risk through human oversight. |
| Inaccurate trajectory prediction | HMI warning and fallback to conservative braking strategy. | Driver intervention required for safe operation. | Reduced functionality but no harm. | Ensures safety while maintaining system availability. |
| Failure to detect occlusions | HMI warning and fallback to conservative braking strategy. | Driver intervention required for safe operation. | Reduced functionality but no harm. | Ensures safety while maintaining system availability. |
| Malfunctioning AEB/planning interface output | Fail-safe mode with reduced AEB activation. | HMI warning to driver about potential communication issues. | Reduced functionality but no harm. | Ensures safety while maintaining system availability. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor data validation | Perception module | Sensor failure detection and mitigation | Real-time diagnostic checks. | Within 10 ms of sensor input. | Unit tests, integration tests, HIL testing. |
| Model robustness | AI model | Misclassification due to occlusion or poor lighting | Post-processing filters for occlusions. | Within 50 ms after object detection. | Model validation using dataset profiles and real-world testing. |
| Trajectory prediction accuracy | Planning module | Inaccurate trajectory prediction under dynamic conditions | Fallback to conservative braking strategy. | Within 1 s of predicted collision time. | Real-time monitoring, HIL testing, and field data collection. |
| Occlusion handling | Perception module | Failure to detect occlusions in complex urban environments | HMI warning for driver intervention. | Within 20 ms after object detection. | Unit tests, integration tests, real-world testing. |
| AEB/planning interface communication | Communication protocol | Malfunctioning safety signals | Fail-safe mode with reduced functionality. | Within 100 ms of signal transmission. | Network diagnostics, HIL testing, and field data collection. |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose**: Define the safety-related requirements.
- **Item-Specific Engineering Activities**:
  - Requirement analysis for cyclist detection system.
  - Hazard identification and risk assessment.
  - Development of functional safety plan.
- **Work Products/Evidence**:
  - Safety requirement document.
  - HARA report.
  - Functional safety plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures all safety-related requirements are identified and managed throughout the lifecycle.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 3: Item Definition
- **Purpose**: Define the system architecture and safety-related outputs.
- **Item-Specific Engineering Activities**:
  - System architecture design.
  - Safety-related output identification.
- **Work Products/Evidence**:
  - System architectural design specification.
  - Safety-related output list.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is designed to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 4: System Development
- **Purpose**: Develop the system architecture and allocate safety-related requirements to hardware/software elements.
- **Item-Specific Engineering Activities**:
  - Software development for perception module.
  - Hardware development for sensor integration.
- **Work Products/Evidence**:
  - Software design specification.
  - Hardware design specification.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is developed to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 5: Hardware Development
- **Purpose**: Develop hardware components for the system.
- **Item-Specific Engineering Activities**:
  - Sensor integration and calibration.
  - Diagnostic coverage development.
- **Work Products/Evidence**:
  - Diagnostic test plan.
  - Calibration report.
- **Rationale/Unsafe Behavior Prevented**: Ensures hardware is developed to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 6: Software Development
- **Purpose**: Develop software components for the system.
- **Item-Specific Engineering Activities**:
  - AI model development and validation.
  - Real-time monitoring and diagnostics.
- **Work Products/Evidence**:
  - AI safety requirements document.
  - Model validation report.
- **Rationale/Unsafe Behavior Prevented**: Ensures software is developed to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 7: Production
- **Purpose**: Ensure the system meets production standards.
- **Item-Specific Engineering Activities**:
  - End-of-line calibration.
  - Sensor health checks.
- **Work Products/Evidence**:
  - Calibration report.
  - Sensor health check logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is produced to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 8: Supporting Processes
- **Purpose**: Ensure traceability and documentation of the system development process.
- **Item-Specific Engineering Activities**:
  - Requirements traceability matrix.
  - Verification planning.
- **Work Products/Evidence**:
  - Requirements traceability matrix.
  - Verification plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures all safety-related requirements are traced and verified throughout the development process.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

#### Part 9: ASIL Decomposition
- **Purpose**: Decompose system into sub-systems and determine their ASIL levels.
- **Item-Specific Engineering Activities**:
  - Sub-system identification.
  - ASIL decomposition.
- **Work Products/Evidence**:
  - ASIL decomposition report.
- **Rationale/Unsafe Behavior Prevented**: Ensures all sub-systems are developed to meet safety goals and requirements.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E malfunctions, while SOTIF address functional insufficiencies.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cyclist detection | Inadequate cyclist detection under low visibility | Low visibility conditions (rain, fog) | Urban intersections at 30-50 km/h | Collision with cyclists | Known | Dataset profiles and real-world testing. | HMI warning for driver intervention. | Risk remains but is mitigated through human oversight. |
| Posture classification | Misclassification of cyclists as pedestrians under low visibility | Low visibility conditions (rain, fog) | Urban intersections at 30-50 km/h | Collision with cyclists mistaken for pedestrians | Known | Dataset profiles and real-world testing. | HMI warning for driver intervention. | Risk remains but is mitigated through human oversight. |
| Trajectory prediction | Inaccurate trajectory prediction under dynamic traffic conditions | Dynamic traffic conditions (multiple vehicles, pedestrians) | Urban intersections at 30-50 km/h | Collision with cyclists due to inaccurate predictions | Unknown | Real-world testing and scenario-based validation. | Fallback to conservative braking strategy. | Risk is managed through fallback mechanisms but remains. |
| Occlusion handling | Failure to detect occlusions in complex urban environments | Complex urban environments (parked cars, buses) | Urban intersections at 30-50 km/h | Collision with cyclists behind obstacles | Known | Real-world testing and scenario-based validation. | HMI warning for driver intervention. | Risk remains but is mitigated through human oversight. |
| AEB/planning interface output | Malfunctioning safety signals under dynamic conditions | Dynamic traffic conditions (multiple vehicles, pedestrians) | Urban intersections at 30-50 km/h | Collision with cyclists due to malfunctioning signals | Unknown | Real-world testing and scenario-based validation. | Fail-safe mode with reduced functionality. | Risk is managed through fallback mechanisms but remains.

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cyclist detection | Safety-critical perception function | High-resolution camera data, LiDAR/Radar data | Dataset gaps in cyclist scenarios under low visibility and occlusion. | Model misclassification due to occlusion or poor lighting. | Distribution shift in cyclist scenarios. | 90% dataset coverage for cyclist presence and position. | Real-time monitoring of model performance using A/B testing. | Risk is managed through continuous monitoring but remains. |
| Posture classification | Safety-critical perception function | High-resolution camera data, LiDAR/Radar data | Dataset gaps in cyclist posture scenarios under low visibility. | Model misclassification due to occlusion or poor lighting. | Distribution shift in cyclist posture scenarios. | 90% dataset coverage for cyclist posture. | Real-time monitoring of model performance using A/B testing. | Risk is managed through continuous monitoring but remains. |
| Trajectory prediction | Safety-critical planning function | High-resolution camera data, LiDAR/Radar data | Dataset gaps in dynamic traffic conditions. | Model misclassification due to occlusion or poor lighting. | Distribution shift in dynamic traffic scenarios. | 90% dataset coverage for trajectory predictions. | Real-time monitoring of model performance using A/B testing. | Risk is managed through continuous monitoring but remains. |
| Occlusion handling | Safety-critical perception function | High-resolution camera data, LiDAR/Radar data | Dataset gaps in occlusion scenarios under complex urban environments. | Model misclassification due to occlusion or poor lighting. | Distribution shift in occlusion scenarios. | 90% dataset coverage for occlusions. | Real-time monitoring of model performance using A/B testing. | Risk is managed through continuous monitoring but remains.