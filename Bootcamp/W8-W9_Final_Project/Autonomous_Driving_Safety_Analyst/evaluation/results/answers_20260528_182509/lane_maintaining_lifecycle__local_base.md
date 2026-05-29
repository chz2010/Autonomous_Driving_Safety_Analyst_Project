### Opening Map

**ISO 26262 = E/E malfunction risk; SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions; ISO 8800 = AI/data/model assurance risk**

---

### Item Definition

| Function | Input | Output | Interfaces | ODD | Safety Role |
| --- | --- | --- | --- | --- | --- |
| Perception | Sensor data (LiDAR, camera) | Lane position, lane boundaries, object detection | ECU, ADAS HMI, Vehicle Control Unit (VCU) | Urban roads up to 80 km/h; no heavy rain or fog | Ensures safe vehicle positioning and obstacle avoidance |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Perception | Lane position, lane boundaries, object detection | Sensor failure, incorrect data processing | Insufficient perception confidence in low-light conditions | Data coverage gap for dark clothing pedestrians | ISO 26262, SOTIF, ISO 8800 | Yes |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Sensor failure, incorrect data processing | Vehicle deviates from lane or collides with object | Urban roads up to 80 km/h; low-light conditions | Ego speed: 30-50 km/h; Object speed: 3-15 km/h | Severity: High - Risk of collision or vehicle deviation leading to injury or death. | Exposure: Moderate - Occurs in urban areas with moderate traffic and varying weather conditions. | Controllability: Low - Driver fallback is limited due to low-light conditions. | ASIL D (QM) | Uncertainty: Ego speed and object speed assumptions may vary. | Review sensor redundancy and data processing algorithms |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Perception | Vehicle deviating from lane or colliding with object | ASIL D | Lane-keeping and obstacle avoidance maintained; fallback to driver control if perception fails. | ISO 26262 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure or incorrect data processing | Lane-keeping and obstacle avoidance maintained; fallback to driver control if perception fails. | HMI alerts driver of potential issues. | Driver takeover or safe stop | Ensures safety in case of sensor or data processing failures. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Redundant sensors and data fusion | ECU, VCU | Sensor failure or incorrect data processing | Lane-keeping and obstacle avoidance maintained; fallback to driver control if perception fails. | Real-time detection of sensor failures within 100 ms | Unit tests, integration tests, diagnostic logs |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| Part 2: Functional Safety Management | Define and manage the safety lifecycle. | Define ASIL, HARA, safety goals, functional safety concept, technical safety concept. | ASIL D classification; HARA table; safety goals; functional safety concept; technical safety concept. | Prevents E/E malfunctions leading to unsafe behavior. | Interacts with SOTIF and ISO 8800 by ensuring safe system design and operation. |
| Part 3: Item Definition | Define the item, its functions, inputs, outputs, interfaces, ODD, assumptions, and safety role. | Defined in previous sections. | Functional decomposition; HARA table; safety goals; functional safety concept; technical safety concept. | Ensures safe system design and operation. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 4: System Development | Develop the item, including architecture, requirements allocation, integration, validation, vehicle-level behavior. | Developed in previous sections. | Architecture diagram; requirements traceability matrix; integration tests; validation evidence. | Ensures safe system development and operation. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 5: Hardware Development | Develop the hardware, including safety requirements, FMEDA, random hardware metrics, diagnostic coverage, SPFM/LFM/PMHF where applicable. | Developed in previous sections. | Hardware design; FMEDA report; diagnostic logs; SPFM/LFM/PMHF analysis. | Ensures safe hardware development and operation. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 6: Software Development | Develop the software, including safety requirements, architecture, freedom from interference, freshness/plausibility checks, watchdogs, degraded-mode logic, unit/integration tests. | Developed in previous sections. | Software design; safety requirements traceability matrix; integration tests; diagnostic logs. | Ensures safe software development and operation. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 7: Production, Operation, Service, Decommissioning | Ensure the item is produced, operated, serviced, and decommissioned safely. | End-of-line calibration; service recalibration; DTCs; field monitoring; incident/near-miss review; OTA gates; staged rollout; rollback; drift monitoring; ODD restriction/disabling criteria. | Production logs; operation monitoring evidence; DTCs; field monitoring reports. | Ensures safe production, operation, and decommissioning. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 8: Supporting Processes | Support the safety lifecycle through configuration/change management, requirements traceability, verification planning, documentation, tool or component qualification, safety case evidence. | Developed in previous sections. | Configuration logs; change control records; requirements traceability matrix; verification plans; documentation; tool qualification reports. | Ensures safe supporting processes. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |
| Part 9: ASIL Decomposition, Dependent Failure Analysis, Common-Cause/Cascading Failure Analysis, Freedom from Interference, FMEA, FTA, DFA | Perform detailed analysis to ensure safety integrity level (ASIL) is met. | ASIL decomposition; dependent failure analysis; common-cause/cascading failure analysis; freedom from interference; FMEA; FTA; DFA. | ASIL decomposition report; dependent failure analysis report; common-cause/cascading failure analysis report; freedom from interference report; FMEA; FTA; DFA. | Ensures safe system design and operation. | Interacts with SOTIF by ensuring intended functionality under defined conditions. |

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Insufficient perception confidence in low-light conditions | Low-light conditions (e.g., rain, fog) | Urban roads up to 80 km/h; no heavy rain or fog | Vehicle deviates from lane or collides with object | Known | Scenario tests, timing analysis | Reduce speed and increase headway when perception confidence drops | Risk reduced but not eliminated due to varying weather conditions. |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Ensures safe perception and obstacle avoidance | High-quality sensor data, labeled datasets for dark clothing pedestrians | Data coverage gap for dark clothing pedestrians; negative samples missing | Model uncertainty in low-light conditions | OOD detection insufficient for known deployment limits | Integration tests show unsafe planner or AEB response to AI output | Continuous monitoring of model performance; fallback to driver control if perception fails. | Risk reduced but not eliminated due to varying weather and lighting conditions. |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor Failure Test | Simulated sensor failure | Lane-keeping and obstacle avoidance maintained; fallback to driver control if perception fails. | System detects sensor failure within 100 ms; fallback logic activated. | Diagnostic logs, integration tests | SG1 |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Operation Monitoring Evidence | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor calibration drift | Perform end-of-line calibration | Calibration within 10% tolerance | Calibration logs, diagnostic checks | Diagnostic logs, operation monitoring reports | Ensures sensor accuracy and reliability. |
| Service Recalibration | Sensor performance degradation | Recalibrate sensors during service intervals | Calibration within 10% tolerance | Calibration logs, diagnostic checks | Diagnostic logs, operation monitoring reports | Ensures ongoing sensor accuracy and reliability. |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 50 | 10 | Rainy | Dim | None | Urban road | Moderate | L2 | 3-5 seconds | Limited fallback to driver control |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure in low-light conditions | Incorrect lane position detection | Lane departure or collision with object | High risk of injury or death | Diagnostic logs, integration tests |
| 2 | System fails to detect sensor failure | No fallback logic activated | Vehicle continues to operate without safety checks | Increased risk of accident | Diagnostic logs, operation monitoring reports |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure leading to incorrect lane position detection | Insufficient perception confidence in low-light conditions | Model uncertainty in low-light conditions; data coverage gap for dark clothing pedestrians | Fallback logic activated; continuous monitoring of model performance. | Diagnostic logs, integration tests |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement redundant sensors and data fusion | Yes | Ensures safety in case of sensor or data processing failures. | System detects sensor failure within 100 ms; fallback logic activated. | Risk reduced but not eliminated due to varying weather conditions. |

---

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 combined into a comprehensive safety case for the lane maintaining perception system. The E/E malfunction risk is mitigated through redundant sensors and data fusion, ensuring safe operation even in sensor failure scenarios. The SOTIF insufficiency risk is addressed by defining performance limitations and triggering conditions, with fallback logic activated when necessary. The ISO 8800 AI/data/model risk is managed through continuous monitoring of model performance and fallback to driver control if perception fails. The final residual risk is reduced but not eliminated due to varying weather and lighting conditions, which are continuously monitored and addressed through ongoing validation and verification activities.

This safety case ensures the lane maintaining perception system operates safely within its defined operational domain, providing a robust foundation for autonomous driving applications.