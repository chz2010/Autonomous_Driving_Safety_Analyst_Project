### Opening Map

- **ISO 26262**: Focus on E/E malfunction risk.
- **SOTIF**: Consider intended-function insufficiencies, performance limitations, foreseeable misuse, and triggering conditions.
- **ISO 8800**: Address AI/data/model assurance risks.

---

### Item Definition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Object detection and classification | Sensor failure, false positives/negatives | Occluded vehicles/pedestrians not detected due to limitations in perception system | Dataset gaps for occluded objects, insufficient label quality |

---

### Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Object detection and classification | Sensor failure, false positives/negatives | Occluded vehicles/pedestrians not detected due to limitations in perception system | ISO 26262, ISO 8800 | Yes |
| Object Classification | Object type identification | Model misclassification | Performance limitations under occlusion | ISO 21448 (SOTIF) | Yes |
| TTC Estimation | Time-to-collision estimation | Sensor latency, model prediction errors | Inaccurate TTC leading to delayed warnings | ISO 26262, ISO 8800 | Yes |
| Warning Arbitration | Decision on warning display | Conflicting sensor data, decision-making errors | Unforeseeable misuse of warning system | ISO 21448 (SOTIF) | Yes |
| Driver HMI Output | Visual and auditory warnings | Display failure, audio output issues | Misleading or insufficient warnings leading to driver confusion | ISO 26262, ISO 8800 | Yes |

---

### HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Sensor failure, false positives/negatives | Collision with occluded vehicle/pedestrian | Low-speed parking lot, occlusion due to parked cars | Severity: High (physical harm) | Exposure: Moderate (parking lots and low-speed reversing scenarios) | Controllability: Low (driver fallback not available in ODD) | ASIL B | Uncertainty: High (sensor performance variability) | HARA for sensor performance |
| Object Classification | Model misclassification | Collision with occluded vehicle/pedestrian | Low-speed parking lot, occlusion due to parked cars | Severity: High (physical harm) | Exposure: Moderate (parking lots and low-speed reversing scenarios) | Controllability: Low (driver fallback not available in ODD) | ASIL B | Uncertainty: High (label quality issues) | HARA for model robustness |
| TTC Estimation | Sensor latency, prediction errors | Collision with occluded vehicle/pedestrian | Low-speed parking lot, occlusion due to parked cars | Severity: High (physical harm) | Exposure: Moderate (parking lots and low-speed reversing scenarios) | Controllability: Low (driver fallback not available in ODD) | ASIL B | Uncertainty: High (sensor latency variability) | HARA for sensor latency |
| Warning Arbitration | Conflicting sensor data, decision-making errors | Collision with occluded vehicle/pedestrian | Low-speed parking lot, occlusion due to parked cars | Severity: High (physical harm) | Exposure: Moderate (parking lots and low-speed reversing scenarios) | Controllability: Low (driver fallback not available in ODD) | ASIL B | Uncertainty: High (decision-making errors) | HARA for decision-making |
| Driver HMI Output | Display failure, audio output issues | Collision with occluded vehicle/pedestrian | Low-speed parking lot, occlusion due to parked cars | Severity: High (physical harm) | Exposure: Moderate (parking lots and low-speed reversing scenarios) | Controllability: Low (driver fallback not available in ODD) | ASIL B | Uncertainty: High (display/audio issues) | HARA for display/audio |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept
#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior |
| --- | --- | --- | --- | --- |
| SG1 | Cross-Traffic Detection | Collision with occluded vehicle/pedestrian | ASIL B | Degraded behavior: Warning display and fallback to manual driving if sensor fails. |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Display warning, fallback to manual driving | HMI display warning and instructions for driver | Manual driving mode | Ensures safe operation in case of sensor failure. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor data validation | ECU | Sensor performance limitations | Real-time diagnostic checks, fallback to manual driving if sensor fails | Real-time | Unit tests, integration tests |

---

### ISO 26262 Part 2-9 Lifecycle Assessment
#### Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Define safety goals and functional safety concept.
- **Work Products/Evidence**: HARA results, safety goals table, functional safety concept table.
- **Rationale/Unsafe Behavior Prevented**: Address potential E/E malfunctions through robust design and diagnostics.
- **Interaction with SOTIF/ISO 8800**: Ensure that ISO 26262 activities complement SOTIF and ISO 8800 requirements.

#### Part 3: Item Definition
- **Item-Specific Engineering Activities**: Define functions, inputs, outputs, interfaces, ODD.
- **Work Products/Evidence**: Functional decomposition table, HARA screening results.
- **Rationale/Unsafe Behavior Prevented**: Ensure that all safety-relevant functions are identified and addressed.

#### Part 4: System Development
- **Item-Specific Engineering Activities**: Architectural design, requirements allocation, integration, validation.
- **Work Products/Evidence**: Technical safety concept table, verification evidence from unit tests and integration tests.
- **Rationale/Unsafe Behavior Prevented**: Ensure that the system architecture supports safe operation under all ODD conditions.

#### Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA, diagnostic coverage.
- **Work Products/Evidence**: Diagnostic test results, failure mode analysis.
- **Rationale/Unsafe Behavior Prevented**: Ensure that hardware components are robust and reliable under all operating conditions.

#### Part 6: Software Development
- **Item-Specific Engineering Activities**: Software safety requirements, architecture, freedom from interference.
- **Work Products/Evidence**: Unit tests, integration tests, diagnostic coverage.
- **Rationale/Unsafe Behavior Prevented**: Ensure that software is free from interference and robust under all operating conditions.

#### Part 7: Production
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, DTCs.
- **Work Products/Evidence**: Calibration logs, diagnostic trouble codes (DTC) records.
- **Rationale/Unsafe Behavior Prevented**: Ensure that the system is calibrated and operational before deployment.

#### Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Traceability matrix, verification plan.
- **Rationale/Unsafe Behavior Prevented**: Ensure that all safety-related activities are documented and traceable.

#### Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: ASIL decomposition table, FMEA/Fault Tree Analysis (FTA).
- **Rationale/Unsafe Behavior Prevented**: Ensure that all potential failures are identified and mitigated.

---

### ISO 21448 (SOTIF) Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Accuracy | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Occluded vehicles/pedestrians not detected due to limitations in perception system | Low-speed parking lot, occlusion due to parked cars | ODD: Low-speed reversing, occluded objects | Collision with occluded vehicle/pedestrian | Known | HARA for sensor performance and model robustness | Degraded behavior: Warning display and fallback to manual driving if sensor fails. | ASIL B |

---

### ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Perception system | Occluded object detection and classification | Insufficient data for occluded objects, label quality issues | Model misclassification under occlusion | Distribution shift due to varying weather conditions | Model performance must meet safety goals during validation. | Continuous monitoring of model performance using real-world data. | ASIL B |

---

### Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Cross-Traffic Detection | Occluded vehicle/pedestrian in low-speed parking lot | Warning display and fallback to manual driving if sensor fails. | Sensor performance meets safety goals during validation. | HARA results, diagnostic test logs. | ASIL B |

---

### Production and Operation Controls
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor performance variability | Calibrate sensors before deployment. | Calibration logs meet safety goals. | Calibration logs, diagnostic test results. | Continuous monitoring of sensor performance during operation. | Ensures that the system is calibrated and operational before deployment.

---

### Worst-Case Scenario
#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 5-10 | 3-5 | Clear | Daylight | Partially occluded by parked cars | Parking lot | Low | Manual driving | 2-4 seconds | Not available in ODD |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation |
| --- | --- | --- | --- | --- |
| 1 | Sensor failure, occluded object not detected | Cross-Traffic Detection fails to detect occluded vehicle/pedestrian. | Warning display and fallback to manual driving if sensor fails. | Driver confusion leading to delayed response.

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure, false positives/negatives | Occluded vehicles/pedestrians not detected due to limitations in perception system | Model misclassification under occlusion | Degraded behavior: Warning display and fallback to manual driving if sensor fails. | HARA results, diagnostic test logs.

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement robust diagnostics for sensors and perception system. | ASIL B risk reduced to acceptable levels. | Ensures that the system is reliable under all operating conditions. | Sensor performance meets safety goals during validation. | ASIL B residual risk.

---

### Final Safety Argument
The ISO 26262, SOTIF, and ISO 8800 combine into a comprehensive safety case for the rear cross-traffic alert system. The HARA screening identifies potential hazards and their associated risks, which are mitigated through robust design, diagnostics, and continuous monitoring. The verification and validation matrix ensures that all safety-related functions meet the required standards during development and production. The worst-case scenario analysis provides a clear understanding of how to handle degraded behavior and ensure safe operation under all ODD conditions.

The final ASIL B risk is reduced to acceptable levels through the implementation of robust diagnostics, continuous monitoring, and fallback mechanisms.