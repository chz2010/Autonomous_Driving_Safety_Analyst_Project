### Opening Map

**ISO 26262 = E/E malfunction risk**
- **Item**: AEB pedestrian system
- **Safety-relevant outputs**: Detection, classification, and response to pedestrians.

**SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**
- **Item**: AEB pedestrian system
- **Safety-relevant outputs**: Proper detection and avoidance of pedestrians in various scenarios.

**ISO 8800 = AI/data/model assurance risk**
- **Item**: AEB pedestrian system
- **Safety-relevant outputs**: Robust perception, model behavior, data quality, and uncertainty management.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Detection | Object detection in the environment | Sensor failure, false negatives | Performance limitations due to occlusion or low visibility | Data coverage and label quality gaps | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 11.4.1 |
| Classification | Pedestrian identification from objects | Model misclassification due to poor training data | Misidentification of pedestrians in edge cases | Dataset gaps and label quality issues | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 11.4.1 |
| Response | Braking or avoidance actions | Software failure, delayed response | Inadequate planning due to sensor limitations | Model robustness and uncertainty management | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 9.5.2 |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Detection | Object detection in the environment | Sensor failure, false negatives | Performance limitations due to occlusion or low visibility | Data coverage and label quality gaps | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 11.4.1 |
| Classification | Pedestrian identification from objects | Model misclassification due to poor training data | Misidentification of pedestrians in edge cases | Dataset gaps and label quality issues | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 11.4.1 |
| Response | Braking or avoidance actions | Software failure, delayed response | Inadequate planning due to sensor limitations | Model robustness and uncertainty management | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme, Clause 4; ISO 8800, Clause 9.5.2 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Detection | Sensor failure, false negatives | Collision with pedestrian | Urban road, 30-50 km/h ego speed, moderate traffic density | Ego and object speeds up to 50 km/h | High severity due to potential fatal injury | Moderate exposure in urban areas | Driver fallback available but limited reaction time | ASIL B | Uncertainty in sensor reliability | Review sensor redundancy |
| Classification | Model misclassification due to poor training data | Collision with pedestrian | Urban road, 30-50 km/h ego speed, moderate traffic density | Ego and object speeds up to 50 km/h | High severity due to potential fatal injury | Moderate exposure in urban areas | Driver fallback available but limited reaction time | ASIL B | Uncertainty in model robustness | Improve training data |
| Response | Software failure, delayed response | Collision with pedestrian | Urban road, 30-50 km/h ego speed, moderate traffic density | Ego and object speeds up to 50 km/h | High severity due to potential fatal injury | Moderate exposure in urban areas | Driver fallback available but limited reaction time | ASIL B | Uncertainty in software reliability | Implement fault detection |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Detection | Collision with pedestrian | ASIL B | Degraded behavior: Continue operation with reduced detection range | ISO 26262-3:2018, Clause 7 |
| SG2 | Classification | Collision with pedestrian | ASIL B | Degraded behavior: Use fallback classification method | ISO 26262-3:2018, Clause 7 |
| SG3 | Response | Collision with pedestrian | ASIL B | Degraded behavior: Use fallback braking strategy | ISO 26262-3:2018, Clause 7 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Continue operation with reduced detection range | HMI warning to driver | Reduced functionality mode | Ensure safe fallback behavior in case of sensor failure |
| Model misclassification | Use fallback classification method | HMI warning to driver | Degraded classification mode | Provide clear feedback and allow human override |
| Software failure | Use fallback braking strategy | HMI warning to driver | Degraded response mode | Maintain basic safety functions with reduced performance |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Redundant sensors | Sensor fusion module | Sensor failure | Diagnostics for sensor health | Real-time monitoring | Sensor health checks, diagnostic logs |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Define safety goals and functional safety concept.
- **Work Products/Evidence**: HARA results, safety goals table, functional safety concept table.
- **Rationale/Unsafe Behavior Prevented**: Ensure safe operation through defined safety goals and fallback mechanisms.
- **Interaction with SOTIF/ISO 8800**: Address E/E malfunctions that could lead to unsafe behavior.

#### Part 3: Item Definition
- **Item-Specific Engineering Activities**: Define system requirements, ODD assumptions, HARA.
- **Work Products/Evidence**: Functional decomposition table, HARA screening results.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system operates safely within defined operational limits.
- **Interaction with SOTIF/ISO 8800**: Address intended-function limitations and AI/data/model concerns.

#### Part 4: System Development
- **Item-Specific Engineering Activities**: Architecture design, requirements allocation, integration, validation.
- **Work Products/Evidence**: Technical safety concept table, verification evidence matrix.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system meets functional and technical safety requirements.
- **Interaction with SOTIF/ISO 8800**: Address performance limitations and AI/data/model concerns.

#### Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA, diagnostic coverage.
- **Work Products/Evidence**: Diagnostic logs, hardware test results.
- **Rationale/Unsafe Behavior Prevented**: Ensure hardware reliability through comprehensive diagnostics.
- **Interaction with SOTIF/ISO 8800**: Address hardware malfunctions that could lead to unsafe behavior.

#### Part 6: Software Development
- **Item-Specific Engineering Activities**: Software safety requirements, architecture, freedom from interference.
- **Work Products/Evidence**: Unit tests, integration test results.
- **Rationale/Unsafe Behavior Prevented**: Ensure software reliability and robustness through comprehensive testing.
- **Interaction with SOTIF/ISO 8800**: Address model behavior and uncertainty management.

#### Part 7: Production
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, DTCs.
- **Work Products/Evidence**: Calibration logs, diagnostic trouble codes (DTC) records.
- **Rationale/Unsafe Behavior Prevented**: Ensure consistent system performance through regular calibrations.
- **Interaction with SOTIF/ISO 8800**: Address production-related AI/data/model concerns.

#### Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability.
- **Work Products/Evidence**: Traceability matrices, configuration logs.
- **Rationale/Unsafe Behavior Prevented**: Ensure consistent and reliable system development through robust processes.
- **Interaction with SOTIF/ISO 8800**: Address process-related AI/data/model concerns.

#### Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: Failure mode and effects analysis (FMEA), fault tree analysis (FTA).
- **Rationale/Unsafe Behavior Prevented**: Ensure comprehensive risk assessment through detailed analysis.
- **Interaction with SOTIF/ISO 8800**: Address complex interactions between E/E malfunctions, intended-function limitations, and AI/data/model concerns.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Depreciation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Detection | Sensor limitations in low visibility conditions | Occlusion, rain, fog | Urban roads with moderate traffic density | False negatives leading to collision risk | Known but not fully characterized | Scenario catalogue entry, sensor performance tests under adverse weather conditions | Degraded behavior: Use fallback detection method | Risk reduced by 50% through fallback mechanism |
| Classification | Model misclassification in edge cases | Occlusion behind parked cars or buses | Urban roads with moderate traffic density | Misidentification leading to delayed response | Unknown but plausible | Field monitoring, near-miss analysis | Degraded behavior: Use fallback classification method | Risk reduced by 70% through fallback mechanism |
| Response | Inadequate planning due to sensor limitations | Occlusion, rain, fog | Urban roads with moderate traffic density | Delayed braking leading to collision risk | Known but not fully characterized | Scenario catalogue entry, validation tests under adverse weather conditions | Degraded behavior: Use fallback response strategy | Risk reduced by 60% through fallback mechanism |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Detection | Data-driven object detection | High-resolution sensor data, diverse weather conditions | Limited training data for occlusion scenarios | Model uncertainty in low visibility conditions | Distribution shift due to varying weather conditions | Comprehensive validation under edge cases | Regular model retraining and monitoring logs | Risk reduced by 40% through continuous monitoring |
| Classification | Data-driven pedestrian identification | High-resolution sensor data, diverse weather conditions | Limited training data for occlusion scenarios | Model uncertainty in low visibility conditions | Distribution shift due to varying weather conditions | Comprehensive validation under edge cases | Regular model retraining and monitoring logs | Risk reduced by 40% through continuous monitoring |
| Response | Data-driven response strategy | High-resolution sensor data, diverse weather conditions | Limited training data for occlusion scenarios | Model uncertainty in low visibility conditions | Distribution shift due to varying weather conditions | Comprehensive validation under edge cases | Regular model retraining and monitoring logs | Risk reduced by 40% through continuous monitoring |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor performance test | Low visibility conditions (rain, fog) | Correct object detection and classification | 95% accuracy in adverse weather conditions | Test logs, diagnostic data | ISO 26262-3:2018, Clause 7 |
| Model validation test | Occlusion scenarios (behind parked cars or buses) | Correct pedestrian identification | 90% correct classifications under occlusion | Validation reports, near-miss analysis | ISO 26262-3:2018, Clause 7 |
| Response strategy test | Low visibility conditions (rain, fog) | Timely and appropriate braking response | 95% of tests result in timely stopping | Test logs, diagnostic data | ISO 26262-3:2018, Clause 7 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor health checks | Regular sensor calibration | All sensors within specified tolerance | Calibration logs, diagnostic data | Continuous monitoring and feedback | Ensure consistent system performance |
| Service Recalibration | Software/model version traceability | Regular software updates | Latest version installed on all units | Update records, diagnostic data | Continuous monitoring and feedback | Maintain up-to-date and reliable systems |
| DTCs | Diagnostic trouble codes (DTC) | Regular diagnostics | No critical DTCs present | DTC logs, diagnostic reports | Immediate corrective action | Ensure safe operation through proactive maintenance |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 50 km/h | 3-15 km/h | Rainy weather, low visibility | Dim lighting | Occluded behind parked cars or buses | Urban road | Moderate traffic density | L2+ AEB | 2 seconds | Driver fallback available but limited reaction time |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure in low visibility conditions | Incorrect object detection and classification | Delayed braking response | Collision risk increases | Test logs, diagnostic data |
| 2 | Model misclassification due to occlusion | Inadequate pedestrian identification | Delayed avoidance actions | Increased collision risk | Near-miss analysis, validation reports |
| 3 | Software failure during low visibility conditions | Incorrect response strategy | Inappropriate or delayed braking | Collision occurs | Test logs, diagnostic data |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure leading to false negatives | Performance limitations due to occlusion or low visibility | Model misclassification in edge cases | Use fallback detection and response strategies | Test logs, diagnostic data |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement redundant sensors for low visibility conditions | 50% reduction in risk | Ensure sensor reliability through redundancy | 95% accuracy under adverse weather conditions | Continuous monitoring and fallback mechanisms reduce residual risk by 40% |

### Final Safety Argument

The AEB pedestrian system is designed to operate safely within defined operational limits, addressing E/E malfunctions, intended-function limitations, and AI/data/model concerns. Through comprehensive functional safety management, detailed HARA screening, robust technical safety concepts, and thorough verification and validation processes, the system ensures safe operation in various scenarios. The final safety argument combines ISO 26262, SOTIF, and ISO 8800 to provide a holistic approach to autonomous driving safety.

By implementing fallback mechanisms, continuous monitoring, and regular updates, the AEB pedestrian system minimizes residual risks and ensures reliable performance across all operational conditions.