### Opening Map

- **ISO 26262 = E/E malfunction risk**: The perception system could fail due to hardware faults or software bugs.
- **SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**: The lane maintaining function might not perform as expected under certain operational situations, such as low visibility or unexpected road conditions.
- **ISO 8800 = AI/data/model assurance risk**: The perception system's AI model could have data gaps, robustness issues, or uncertainty that lead to unsafe behavior.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Perception | Object detection and tracking, lane boundaries identification | Sensor failure, software bugs, incorrect data interpretation | Low perception confidence in low visibility conditions, model limitations due to ODD | Data gaps, label quality issues, uncertainty in AI predictions | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Perception | Object detection and tracking, lane boundaries identification | Sensor failure, software bugs, incorrect data interpretation | Low perception confidence in low visibility conditions, model limitations due to ODD | Data gaps, label quality issues, uncertainty in AI predictions | ISO 26262, ISO 21448 (SOTIF), ISO 8800 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Sensor failure, software bugs, incorrect data interpretation | Object collision or near-miss | Low visibility conditions (rain, fog) | E/E malfunction can lead to missed object detection | Exposure is high due to frequent low-visibility conditions on roads | Driver cannot avoid the hazard in time | ASIL B | Uncertainty from weather conditions and sensor performance | Review sensor redundancy and fallback mechanisms |
| Perception | Low perception confidence in low visibility conditions, model limitations due to ODD | Object collision or near-miss | Low visibility conditions (rain, fog) | Insufficient performance can lead to missed object detection | Exposure is high due to frequent low-visibility conditions on roads | Driver cannot avoid the hazard in time | ASIL B | Uncertainty from weather conditions and sensor performance | Implement robust model training with diverse data |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Perception | Object collision or near-miss | ASIL B | Correct object detection and tracking, lane boundaries identification | ISO 26262 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Emergency braking or fallback to manual control | Warning message on HMI | Manual driving mode | Ensures safety in case of sensor failure |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Redundant sensors | Sensor fusion module | Sensor failure | Fallback to primary sensor if secondary fails | Real-time | Log files, diagnostic tests |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### ISO 26262 Part 2: Functional Safety Management
- **Purpose**: Define the safety management process.
- **Item-Specific Engineering Activities**: Risk assessment, risk reduction planning, safety plan development.
- **Work Products/Evidence**: Safety policy, risk assessment report, safety plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures systematic approach to managing risks.
- **Interaction with SOTIF/ISO 8800**: Aligns with SOTIF and ISO 8800 by considering functional limitations and AI-specific risks.

#### ISO 26262 Part 3: Item Definition
- **Purpose**: Define the system requirements and safety goals.
- **Item-Specific Engineering Activities**: Functional decomposition, HARA, safety goal definition.
- **Work Products/Evidence**: Functional decomposition diagram, HARA table, safety goals document.
- **Rationale/Unsafe Behavior Prevented**: Ensures clear understanding of potential hazards.
- **Interaction with SOTIF/ISO 8800**: Incorporates SOTIF and ISO 8800 considerations into the functional definition.

#### ISO 26262 Part 4: System Development
- **Purpose**: Develop the system architecture and allocate safety requirements.
- **Item-Specific Engineering Activities**: Architecture design, requirement allocation, integration testing.
- **Work Products/Evidence**: System architecture diagram, requirement traceability matrix, integration test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe system behavior through proper architecture and requirements.
- **Interaction with SOTIF/ISO 8800**: Integrates SOTIF performance limitations and ISO 8800 AI robustness.

#### ISO 26262 Part 5: Hardware Development
- **Purpose**: Develop the hardware components.
- **Item-Specific Engineering Activities**: Hardware design, FMEDA, diagnostic coverage analysis.
- **Work Products/Evidence**: Hardware design documentation, FMEDA report, diagnostic test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures reliable hardware operation.
- **Interaction with SOTIF/ISO 8800**: No direct interaction as it focuses on E/E components.

#### ISO 26262 Part 6: Software Development
- **Purpose**: Develop the software components.
- **Item-Specific Engineering Activities**: Software design, unit testing, integration testing.
- **Work Products/Evidence**: Software design documentation, test cases, test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe and reliable software operation.
- **Interaction with SOTIF/ISO 8800**: Integrates AI-specific validation and robustness checks.

#### ISO 26262 Part 7: Production
- **Purpose**: Ensure the production process meets safety requirements.
- **Item-Specific Engineering Activities**: Calibration, service recalibration, DTC management.
- **Work Products/Evidence**: Calibration documentation, DTC logs, service records.
- **Rationale/Unsafe Behavior Prevented**: Ensures consistent and reliable system performance in production.
- **Interaction with SOTIF/ISO 8800**: No direct interaction as it focuses on E/E components.

#### ISO 26262 Part 8: Supporting Processes
- **Purpose**: Manage the supporting processes to ensure safety.
- **Item-Specific Engineering Activities**: Configuration management, requirements traceability, verification planning.
- **Work Products/Evidence**: Configuration logs, requirement traceability matrix, verification plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures systematic and controlled development process.
- **Interaction with SOTIF/ISO 8800**: Integrates AI-specific validation and robustness checks.

#### ISO 26262 Part 9: ASIL Decomposition
- **Purpose**: Decompose the system into ASIL levels.
- **Item-Specific Engineering Activities**: ASIL decomposition, dependent failure analysis.
- **Work Products/Evidence**: ASIL decomposition diagram, dependent failure analysis report.
- **Rationale/Unsafe Behavior Prevented**: Ensures proper allocation of safety requirements.
- **Interaction with SOTIF/ISO 8800**: Integrates SOTIF and ISO 8800 considerations into the ASIL decomposition.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Low perception confidence in low visibility conditions, model limitations due to ODD | Rain, fog, night-time driving | Defined ODD (urban roads, 30-50 km/h) | Object collision or near-miss | Known scenario status | Robust model training with diverse data | Fallback to manual control | Residual risk is managed through fallback mechanisms and robust model training |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Object detection and tracking, lane boundaries identification | High-quality labeled data, diverse weather conditions | Data gaps in low-visibility scenarios | Model uncertainty in low-confidence predictions | Distribution shift due to changing weather conditions | Robust model training with diverse data | Continuous monitoring of model performance | Residual risk is managed through robust model training and continuous monitoring |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Perception | Low visibility conditions (rain, fog) | Correct object detection and tracking, lane boundaries identification | High perception confidence in low-visibility scenarios | Log files, diagnostic tests | SG1 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor calibration drift | Regular sensor recalibration | Sensor performance within specified limits | Calibration logs, diagnostic tests | Continuous monitoring of sensor performance | Ensures consistent and reliable system operation |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 50 | 3-15 | Rain, fog | Dim | None | Urban road | Moderate | L2+ | 2-4 | Manual takeover |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Low perception confidence in rain, fog | Object not detected | No braking or avoidance action | Object collision | Log files, diagnostic tests |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure or software bug | Low perception confidence in low visibility conditions, model limitations due to ODD | Data gaps, label quality issues, uncertainty in AI predictions | Fallback to manual control, robust model training with diverse data | Log files, diagnostic tests |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement fallback mechanisms and robust model training | Yes | Ensures safety in case of sensor failure or low perception confidence | High perception confidence in low-visibility scenarios | Residual risk is managed through fallback mechanisms and robust model training |

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 combine to ensure the lane maintaining perception system operates safely under various conditions. The ASIL B safety goals address potential E/E malfunctions and functional limitations. The SOTIF analysis identifies triggering conditions and ODD limitations that require robust model training and fallback mechanisms. The ISO 8800 evaluation ensures data quality, model robustness, and uncertainty management to prevent unsafe behavior in unknown scenarios. Verification through log files, diagnostic tests, and continuous monitoring supports the safety case.

This comprehensive approach ensures a holistic safety argument for the lane maintaining perception system.