### Opening Map

- **ISO 26262 = E/E malfunction risk**: The AEB pedestrian system must handle hardware faults and systematic/random E/E faults.
- **SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**: The system must ensure that the intended function is safe within its operational design domain (ODD) and does not fail in edge cases or foreseeable misuse scenarios.
- **ISO 8800 = AI/data/model assurance risk**: The AEB pedestrian system must address AI-specific risks such as data coverage, model robustness, uncertainty, and distribution shift.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| AEB initiation | Decision to initiate AEB based on pedestrian detection | E/E fault in sensor data processing | Performance limitation due to insufficient perception confidence | Data coverage and label quality gaps | ISO 26262, ISO 8800 |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| **1. Perception** | Object detection and classification | Sensor failure, E/E fault in data processing | Performance limitation due to occlusion or low visibility conditions | Data coverage and label quality gaps | ISO 26262, ISO 8800 |
| **2. Decision-making** | AEB initiation decision based on object distance and speed | E/E fault in logic execution | Performance limitation due to complex pedestrian behavior scenarios | Model robustness and uncertainty | ISO 26262, SOTIF, ISO 8800 |
| **3. Actuation** | Control signals for braking system | E/E fault in actuator control | Performance limitation due to brake system latency | Data coverage and label quality gaps | ISO 26262 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Perception | Sensor failure, E/E fault in data processing | AEB not initiated when pedestrian is detected | Urban road, 30-50 km/h ego speed, moderate traffic density, occlusion possible | Ego: 30-40 km/h; Object: 2-5 km/h | Severity: Risk of collision due to undetected pedestrian. | Exposure: High in urban areas with pedestrians. | Controllability: Driver fallback is available but may not be timely. | ASIL B | Uncertainty: Need for more robust perception model and better data coverage. | Further HARA refinement |
| 2. Decision-making | Performance limitation due to occlusion or low visibility conditions | AEB initiated too late, leading to collision | Urban road, 30-50 km/h ego speed, moderate traffic density, occlusion possible | Ego: 30-40 km/h; Object: 2-5 km/h | Severity: Risk of collision due to delayed braking. | Exposure: High in urban areas with pedestrians and occlusions. | Controllability: Driver fallback is available but may not be timely. | ASIL B | Uncertainty: Need for more robust perception model and better data coverage. | Further HARA refinement |
| 3. Actuation | E/E fault in actuator control | AEB fails to initiate braking, leading to collision | Urban road, 30-50 km/h ego speed, moderate traffic density, occlusion possible | Ego: 30-40 km/h; Object: 2-5 km/h | Severity: Risk of collision due to undetected pedestrian. | Exposure: High in urban areas with pedestrians. | Controllability: Driver fallback is available but may not be timely. | ASIL B | Uncertainty: Need for more robust perception model and better data coverage. | Further HARA refinement |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| 1.01 | Perception | Undetected pedestrian leading to collision | ASIL B | Degraded behavior: Continue monitoring and alert driver if necessary. | ISO 26262, ISO 8800 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Initiate fallback mode and alert driver. | Provide visual and audio alerts to driver. | Continue monitoring and alerting until system recovers or failsafe state is reached. | Ensures safe operation in case of sensor failure. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Perception model robustness | AI system and perception module | Data coverage gaps, label quality issues | Regular health checks and fallback to manual driving mode. | Real-time monitoring of perception outputs. | Model performance metrics, HMI logs, diagnostic tests. |

### ISO 26262 Part 2-9 Lifecycle Assessment

| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| **Part 2** | Functional Safety Management | Define safety goals, HARA, and ASIL levels. | Safety plan, DIA, release responsibilities. | Ensures systematic approach to functional safety management. | Interacts with SOTIF by defining ODD assumptions and ASIL levels. |
| **Part 3** | Item Definition | Decompose system into functions and outputs. | Functional decomposition table, HARA screening. | Prevents unsafe behavior through detailed function definition. | Interacts with ISO 8800 by addressing AI safety concepts. |
| **Part 4** | System Development | Allocate functional safety requirements to components. | Technical safety concept, architecture design. | Ensures safe system development and integration. | Interacts with SOTIF by defining triggering conditions and ODD assumptions. |
| **Part 5** | Hardware Development | Define hardware safety requirements. | FMEDA, diagnostic coverage analysis. | Prevents E/E malfunctions through robust hardware design. | Interacts with ISO 8800 by ensuring data integrity and model robustness. |
| **Part 6** | Software Development | Allocate software safety requirements. | Software safety concept, unit tests. | Ensures safe software execution and behavior. | Interacts with SOTIF by defining performance limitations and triggering conditions. |
| **Part 7** | Production/Operation | Define operational controls and service procedures. | End-of-line calibration, DTCs, field monitoring. | Ensures safe operation through regular checks and updates. | Interacts with ISO 8800 by addressing AI lifecycle concerns during production and operation. |
| **Part 8** | Supporting Processes | Ensure traceability and verification planning. | Requirements traceability matrix, verification plan. | Prevents unsafe behavior through systematic process management. | Interacts with SOTIF by defining validation criteria and evidence artifacts. |
| **Part 9** | ASIL Decomposition | Define dependent failure analysis. | ASIL decomposition table, fault tree analysis. | Ensures safe system operation through detailed ASIL levels. | Interacts with ISO 8800 by addressing AI-specific risks during ASIL decomposition. |

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Occlusion or low visibility conditions | Pedestrian occluded by parked cars or buses. | Urban roads, moderate traffic density. | AEB not initiated in time, leading to collision. | Known scenario but with high uncertainty. | Scenario catalogue entry, confidence/uncertainty calibration, validation results under rain/night/occlusion. | Fallback mode activation and driver alerts. | High residual risk due to uncertain occlusion scenarios. |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception model | Data-driven decision-making | High-quality pedestrian detection dataset. | Gaps in occlusion scenarios, night-time conditions. | Model overfitting to training data. | Distribution shift due to weather and lighting changes. | Model performance metrics, scenario-specific validation results. | Regular monitoring of model robustness and uncertainty through field tests and real-world feedback. | High residual risk due to uncertain occlusion and low visibility conditions. |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Perception model validation | Occluded pedestrian scenario | AEB initiated in time to avoid collision. | Time-to-collision metric, false-negative rate. | Model performance metrics, HMI logs. | Safety goal 1.01 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor health checks | Regular calibration of sensors. | No sensor failures detected. | Sensor logs, diagnostic reports. | Continuous monitoring and feedback from field operations. | Ensures safe operation through regular checks. |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time | Driver Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 30-40 km/h | 2-5 km/h | Rainy day | Dim light | Behind parked cars | Urban road | Moderate traffic density | Fully autonomous mode | 1.5 seconds | Available but may not be timely |

#### Accident-Chain Table
| Step | Degraded/ Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Occluded pedestrian detection | AEB not initiated. | Collision occurs. | High risk of injury or fatality. | Scenario catalogue entry, confidence/uncertainty calibration, validation results under rain/night/occlusion. |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure leading to undetected pedestrian. | Performance limitation due to occlusion or low visibility conditions. | Model overfitting and uncertainty in occluded scenarios. | Fallback mode activation, driver alerts, regular model updates. | Model performance metrics, HMI logs, diagnostic tests. |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement fallback mode and regular health checks. | High risk reduced to medium. | Ensures safe operation through robust fallback mechanisms. | No sensor failures detected, AEB initiated in time for occluded pedestrians. | Uncertainty remains due to low visibility conditions. |

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 combine to ensure the safety of the AEB pedestrian system through a comprehensive approach:

- **ISO 26262** ensures that hardware faults are managed and E/E malfunctions do not lead to unsafe behavior.
- **SOTIF** addresses performance limitations and triggering conditions to prevent unsafe intended functionality, ensuring safe operation within its ODD.
- **ISO 8800** focuses on AI-specific risks such as data coverage, model robustness, uncertainty, and distribution shift, ensuring that the system remains safe across all operational scenarios.

By addressing these aspects through detailed functional decomposition, HARA screening, safety goals, and comprehensive verification and validation processes, the AEB pedestrian system can be designed to meet high safety standards.