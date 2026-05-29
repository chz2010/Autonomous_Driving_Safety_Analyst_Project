### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Focuses on unsafe intended functionality from limitations/ODD/triggering conditions.
- **ISO 8800**: Focuses on AI/data/model assurance risk.

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
- Vehicle state information (speed, direction)

**Outputs:**
- Warning signals to driver
- Control commands for hazard lights or turn signals

**Interfaces:**
- ECU communication interfaces
- Human-machine interface (HMI) for warnings

**Operational Domain Description (ODD):**
- Urban and highway lane changes
- Day/night visibility
- Moderate rain conditions

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Object classification | Sensor failure | Performance limitations under poor visibility | Data coverage gaps for occluded objects | ISO 26262, ISO 8800 | Yes |
| Relative velocity estimation | Velocity vector | Algorithm error | Inaccurate speed estimates in rain | Robustness to weather conditions | ISO 26262, SOTIF | Yes |
| Blind-zone occupancy | Occupancy status | False positives/negatives | Misclassification of objects as free space | Model uncertainty under occlusion | ISO 8800 | Yes |
| Driver warning | Warning signal | Delayed or missed warnings | Inadequate driver attention in poor visibility | Monitoring for driver distraction | SOTIF, ISO 26262 | Yes |
| Interface output | Control commands | Communication failure | Miscommunication with HMI | Data integrity checks | ISO 8800 | No |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Sensor failure | Collision with detected object | Urban lane change, poor visibility | Object not detected -> collision risk | High frequency of urban lane changes and poor visibility | Driver cannot avoid by visual check | ASIL C | Low uncertainty from sensor redundancy | Verify sensor health checks |
| Relative velocity estimation | Algorithm error | Incorrect speed-based warning | Highway lane change, rain | Inaccurate speed -> delayed or incorrect warnings | Rain reduces visibility -> higher risk of misjudgment | Driver can reduce speed but not fully compensate for errors | ASIL B | Moderate uncertainty from weather models | Validate algorithm under various weather conditions |
| Blind-zone occupancy | False positives/negatives | Missed warning due to false negative | Urban lane change, occlusion | Object present but not detected -> missed warning | High frequency of urban driving with occlusions | Driver cannot rely on system for critical decisions | ASIL B | Moderate uncertainty from dataset coverage | Improve data labeling for occluded objects |
| Driver warning | Delayed or missed warnings | Driver unaware of potential hazard | Highway lane change, poor visibility | Warning not given -> driver unaware | High risk during lane changes in poor visibility | Driver cannot compensate for delayed warnings | ASIL C | Low uncertainty from fallback logic | Implement fallback visual alerts |
| Interface output | Communication failure | Miscommunication with HMI | Urban driving, sensor failure | Command not received by HMI -> system inoperable | High frequency of urban driving and potential sensor failures | Driver relies on HMI for critical warnings | ASIL B | Low uncertainty from redundancy checks | Implement redundant communication channels |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior |
| --- | --- | --- | --- | --- |
| SG1 | Side object detection | Collision with detected object | C | Object not detected -> collision risk |
| SG2 | Relative velocity estimation | Incorrect speed-based warning | B | Inaccurate speed -> delayed or incorrect warnings |
| SG3 | Blind-zone occupancy | Missed warning due to false negative | B | Object present but not detected -> missed warning |
| SG4 | Driver warning | Driver unaware of potential hazard | C | Warning not given -> driver unaware |
| SG5 | Interface output | Miscommunication with HMI | B | Command not received by HMI -> system inoperable |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | System degrades to lower ASIL mode | Warning displayed on HMI | Reduced functionality with warnings | Ensures driver remains informed and can take manual action |
| Algorithm error | Corrective actions taken by fallback logic | Driver receives warning | Degraded but functional system | Provides time for driver to react |
| False positives/negatives | System degrades to lower ASIL mode | Warning displayed on HMI | Reduced functionality with warnings | Ensures driver remains informed and can take manual action |
| Delayed or missed warnings | Driver receives fallback visual alerts | Visual alerts displayed on HMI | Degraded but functional system | Provides time for driver to react |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor health checks | ECU | Sensor failure | Health check logs, diagnostic tests | Real-time | Log analysis, sensor test results |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### ISO 26262 Part 2: Functional Safety Management
- **Purpose**: Define the safety lifecycle phases and activities.
- **Item-Specific Engineering Activities**:
  - Risk assessment (HARA)
  - Supplier interface management
  - Safety plan development
  - Confirmation measures for functional safety

#### ISO 26262 Part 3: Item Definition
- **Purpose**: Define the item's functions, inputs, outputs, and interfaces.
- **Item-Specific Engineering Activities**:
  - Functional decomposition
  - ODD definition
  - HARA screening

#### ISO 26262 Part 4: System Development
- **Purpose**: Develop the system architecture and allocate safety requirements.
- **Item-Specific Engineering Activities**:
  - Architecture design
  - Requirements allocation
  - Integration and validation

#### ISO 26262 Part 5: Hardware Development
- **Purpose**: Develop hardware components to meet safety requirements.
- **Item-Specific Engineering Activities**:
  - Fault tree analysis (FTA)
  - Failure mode effects and criticality analysis (FMEA)

#### ISO 26262 Part 6: Software Development
- **Purpose**: Develop software components to meet safety requirements.
- **Item-Specific Engineering Activities**:
  - Software architecture design
  - Safety-critical code development

#### ISO 26262 Part 7: Production, Operation, Service
- **Purpose**: Ensure the system operates safely in production and service phases.
- **Item-Specific Engineering Activities**:
  - End-of-line calibration
  - Service recalibration
  - Diagnostic trouble codes (DTCs)

#### ISO 26262 Part 8: Supporting Processes
- **Purpose**: Support processes for configuration, change management, and documentation.
- **Item-Specific Engineering Activities**:
  - Requirements traceability
  - Verification planning

#### ISO 26262 Part 9: ASIL Decomposition
- **Purpose**: Decompose the system into sub-items with appropriate ASIL levels.
- **Item-Specific Engineering Activities**:
  - Dependent failure analysis
  - Common cause/failure analysis

---

### SOTIF Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Performance limitations under poor visibility | Rain, low light conditions | Urban driving with frequent lane changes | Missed detections -> collision risk | Known scenarios | Validate performance in various weather conditions | Degraded mode with fallback logic | Moderate residual risk due to uncertainty |
| Relative velocity estimation | Inaccurate speed estimates in rain | Rain, low visibility | Highway driving during poor weather | Incorrect warnings -> delayed response | Known scenarios | Validate algorithm under different weather conditions | Fallback visual alerts | Low residual risk from fallback mechanisms |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side object detection | Data-driven decision-making | High-resolution sensor data, diverse weather conditions | Occluded objects in dataset | Model uncertainty under occlusion | Distribution shift due to varying road conditions | Comprehensive dataset coverage and regular updates | Regular model retraining and validation | Moderate residual risk from ongoing monitoring |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor health check | Sensor failure | System degrades to lower ASIL mode | Log analysis, diagnostic tests pass | Health check logs | SG1 |
| Algorithm validation | Rain, low visibility | Correct speed estimates and warnings | Validation in various weather conditions passes | Test results | SG2 |
| Driver warning system | Delayed or missed warnings | Driver receives fallback visual alerts | Fallback logic triggers correctly | Log analysis | SG4 |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-line calibration | Sensor accuracy | Calibration checks | All sensors within tolerance | Calibration logs | Continuous monitoring | Ensures system operates as intended |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 60 | 30 | Moderate rain | Dim | Partial occlusion | Urban road | Low to moderate | L2+ |

#### Accident-Chain Table
1. **Degraded/missing signal**: Sensor failure in rainy conditions.
2. **System interpretation**: Object not detected due to occlusion.
3. **Vehicle response**: No warning given to driver.
4. **Hazard escalation**: Driver unaware and unable to react in time.

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure -> no warning given | Performance limitations under poor visibility -> missed detection | Model uncertainty under occlusion -> fallback logic | Degraded mode with fallback visual alerts | Log analysis, sensor test results |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement redundant sensors and health checks | Moderate risk reduction | Ensures system reliability in poor conditions | All sensors pass health check logs | Ongoing monitoring required |

---

### Final Safety Argument

The safety case for the blind spot monitoring system is built on a comprehensive approach that integrates ISO 26262, SOTIF, and ISO 8800. The HARA analysis identifies key risks and mitigation strategies, ensuring that the system operates safely under various conditions. Verification and validation activities are in place to ensure robust performance, while production controls maintain system integrity. The worst-case scenario analysis provides a clear understanding of potential hazards and how they can be mitigated.

By following this structured approach, the blind spot monitoring system is designed to meet stringent safety standards, providing reliable support for drivers during urban and highway lane changes, even in moderate rain conditions.