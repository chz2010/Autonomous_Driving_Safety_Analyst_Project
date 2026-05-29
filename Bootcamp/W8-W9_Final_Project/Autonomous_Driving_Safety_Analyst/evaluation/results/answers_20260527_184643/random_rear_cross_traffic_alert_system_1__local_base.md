### Opening Map

**ISO 26262 Malfunction Risk:** The rear cross-traffic alert system may fail due to hardware faults or software errors.

**SOTIF Insufficiency Risk:** The intended function of the system might be insufficient in certain operational conditions, such as occluded vehicles and pedestrians.

**ISO 8800 AI/Data/Model Risk:** The perception system's data coverage, label quality, model robustness, and uncertainty may lead to unsafe behavior under specific scenarios.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Cross-traffic detection | Object classification, TTC estimation | Sensor failure, software bug | Occluded vehicles and pedestrians not detected due to limitations in the perception system | Data coverage gaps for occluded objects, label quality issues | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |
| Object classification | Classification of objects as vehicles or pedestrians | Incorrect object classification due to sensor noise or software bug | Misclassification of occluded objects leading to false negatives | Data coverage gaps for occluded objects, label quality issues | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |
| TTC estimation | Time-to-collision value | Sensor failure, software bug | Inaccurate TTC due to occlusion or sensor limitations | Data coverage gaps for occluded objects, label quality issues | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |
| Warning arbitration | Decision on warning display | Software bug, incorrect decision logic | Insufficient performance in low-visibility conditions leading to delayed warnings | Data coverage gaps for occluded objects, label quality issues | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |
| Driver HMI output | Warning display and audio alerts | Software bug, incorrect decision logic | Insufficient performance in low-visibility conditions leading to delayed warnings | Data coverage gaps for occluded objects, label quality issues | ISO 26262, ISO 21448 (SOTIF), ISO 8800 | Yes |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Cross-traffic detection | Object classification, TTC estimation | Sensor failure, software bug | Occluded vehicles and pedestrians not detected due to limitations in the perception system | Data coverage gaps for occluded objects, label quality issues |
| Object classification | Classification of objects as vehicles or pedestrians | Incorrect object classification due to sensor noise or software bug | Misclassification of occluded objects leading to false negatives | Data coverage gaps for occluded objects, label quality issues |
| TTC estimation | Time-to-collision value | Sensor failure, software bug | Inaccurate TTC due to occlusion or sensor limitations | Data coverage gaps for occluded objects, label quality issues |
| Warning arbitration | Decision on warning display | Software bug, incorrect decision logic | Insufficient performance in low-visibility conditions leading to delayed warnings | Data coverage gaps for occluded objects, label quality issues |
| Driver HMI output | Warning display and audio alerts | Software bug, incorrect decision logic | Insufficient performance in low-visibility conditions leading to delayed warnings | Data coverage gaps for occluded objects, label quality issues |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-traffic detection | Sensor failure, software bug | Collision with occluded vehicle or pedestrian | Low-speed reversing in parking lots | 5-10 km/h | E/E malfunction can lead to missed detections and collisions. | Exposure is high due to frequent low-speed maneuvers. | Controllability is low as the driver may not be aware of occlusions. | ASIL B-C | Uncertainty from data gaps and model robustness. | Perform HARA for each function. |
| Object classification | Incorrect object classification | False negatives leading to delayed warnings | Low-speed reversing in parking lots | 5-10 km/h | SOTIF insufficiency can lead to unsafe behavior. | Exposure is high due to frequent low-speed maneuvers. | Controllability is low as the driver may not be aware of occlusions. | ASIL B-C | Uncertainty from data gaps and model robustness. | Perform HARA for each function. |
| TTC estimation | Sensor failure, software bug | Inaccurate collision avoidance | Low-speed reversing in parking lots | 5-10 km/h | E/E malfunction can lead to delayed warnings. | Exposure is high due to frequent low-speed maneuvers. | Controllability is low as the driver may not be aware of occlusions. | ASIL B-C | Uncertainty from data gaps and model robustness. | Perform HARA for each function. |
| Warning arbitration | Software bug, incorrect decision logic | Delayed warning display | Low-speed reversing in parking lots | 5-10 km/h | SOTIF insufficiency can lead to unsafe behavior. | Exposure is high due to frequent low-speed maneuvers. | Controllability is low as the driver may not be aware of occlusions. | ASIL B-C | Uncertainty from data gaps and model robustness. | Perform HARA for each function. |
| Driver HMI output | Software bug, incorrect decision logic | Delayed warning display | Low-speed reversing in parking lots | 5-10 km/h | SOTIF insufficiency can lead to unsafe behavior. | Exposure is high due to frequent low-speed maneuvers. | Controllability is low as the driver may not be aware of occlusions. | ASIL B-C | Uncertainty from data gaps and model robustness. | Perform HARA for each function. |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior |
| --- | --- | --- | --- | --- |
| 1 | Cross-traffic detection | Collision with occluded vehicle or pedestrian | ASIL B-C | Degraded behavior includes reduced warning display. |
| 2 | Object classification | False negatives leading to delayed warnings | ASIL B-C | Degraded behavior includes reduced warning display. |
| 3 | TTC estimation | Inaccurate collision avoidance | ASIL B-C | Degraded behavior includes reduced warning display. |
| 4 | Warning arbitration | Delayed warning display | ASIL B-C | Degraded behavior includes reduced warning display. |
| 5 | Driver HMI output | Delayed warning display | ASIL B-C | Degraded behavior includes reduced warning display. |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure, software bug | System fails safe and displays a degraded warning. | HMI alerts the driver of potential occlusions. | Reduced functionality mode with warnings. | Ensures safety by providing timely alerts even in degraded states. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor fusion and redundancy | Perception system | Sensor failure | Redundant sensors provide fallback. | Real-time monitoring of sensor health. | Unit tests, integration tests, and field monitoring. |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose:** Define the safety goals and manage the functional safety process.
- **Item-Specific Engineering Activities:** Define the item's safety goals, perform HARA, derive ASIL levels, develop a safety plan, and define confirmation measures.
- **Work Products/Evidence:** Safety goals document, HARA table, ASIL level derivation, safety plan, confirmation measures.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all functions are analyzed for potential hazards and mitigated accordingly.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures E/E malfunctions are addressed, while SOTIF addresses intended-function insufficiencies.

#### Part 3: Item Definition
- **Purpose:** Define the item's functions, inputs, outputs, interfaces, ODD, and safety role.
- **Item-Specific Engineering Activities:** Define the cross-traffic alert system’s functions, inputs, outputs, interfaces, ODD, and safety role.
- **Work Products/Evidence:** Functional decomposition table, interface diagrams, ODD assumptions, safety role definition.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all functions are clearly defined and their interactions are well understood.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures clear function definitions, while SOTIF addresses potential performance limitations.

#### Part 4: System Development
- **Purpose:** Develop the system architecture, allocate safety requirements, integrate components, and perform validation.
- **Item-Specific Engineering Activities:** Develop the perception system, allocate safety requirements, integrate hardware and software, and validate the system.
- **Work Products/Evidence:** Architecture diagrams, safety requirement allocation table, integration test plans, validation reports.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all components are developed with safety in mind and validated thoroughly.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures E/E components are safe, while SOTIF addresses intended-function insufficiencies.

#### Part 5: Hardware Development
- **Purpose:** Develop the hardware components and ensure they meet safety requirements.
- **Item-Specific Engineering Activities:** Design and develop hardware components, perform FMEDA, random hardware metrics analysis, diagnostic coverage assessment.
- **Work Products/Evidence:** Hardware design documents, FMEDA reports, random hardware metrics data, diagnostic coverage plans.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all hardware is safe and reliable.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures hardware safety, while SOTIF addresses intended-function insufficiencies.

#### Part 6: Software Development
- **Purpose:** Develop the software components and ensure they meet safety requirements.
- **Item-Specific Engineering Activities:** Develop software components, perform freedom from interference analysis, freshness/plausibility checks, watchdogs, degraded-mode logic, unit/integration tests.
- **Work Products/Evidence:** Software design documents, freedom from interference plans, freshness/plausibility check reports, watchdog logs, test results.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all software is safe and reliable.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures software safety, while SOTIF addresses intended-function insufficiencies.

#### Part 7: Production
- **Purpose:** Ensure the production process meets safety requirements.
- **Item-Specific Engineering Activities:** Perform end-of-line calibration, service recalibration, DTCs management, field monitoring.
- **Work Products/Evidence:** Calibration reports, service recalibration plans, DTC logs, field monitoring data.
- **Rationale/Unsafe Behavior Prevented:** Ensures that the production process is safe and reliable.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures safety during production, while SOTIF addresses intended-function insufficiencies.

#### Part 8: Supporting Processes
- **Purpose:** Ensure supporting processes meet safety requirements.
- **Item-Specific Engineering Activities:** Configuration/change management, requirements traceability, verification planning, documentation, tool or component qualification, safety case evidence.
- **Work Products/Evidence:** Configuration management plans, requirements traceability matrices, verification plans, documentation, qualification reports.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all supporting processes are safe and reliable.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures safety during production, while SOTIF addresses intended-function insufficiencies.

#### Part 9: ASIL Decomposition
- **Purpose:** Decompose the system into smaller components for detailed analysis.
- **Item-Specific Engineering Activities:** Perform ASIL decomposition, dependent failure analysis, common-cause/cascading failure analysis, freedom from interference analysis, FMEA, FTA, DFA.
- **Work Products/Evidence:** ASIL decomposition table, dependent failure analysis reports, common-cause/cascading failure analysis results, freedom from interference plans, FMEA, FTA, DFA.
- **Rationale/Unsafe Behavior Prevented:** Ensures that all components are analyzed for potential hazards and mitigated accordingly.
- **Interaction with SOTIF/ISO 8800:** ISO 26262 ensures E/E malfunctions are addressed, while SOTIF addresses intended-function insufficiencies.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-traffic detection | Occluded vehicles and pedestrians not detected due to limitations in the perception system | Low visibility, occlusion | Parking lots, low-speed reversing | False negatives leading to delayed warnings | Known | Data coverage gaps for occluded objects, label quality issues | Perform HARA for each function. | Uncertainty from data gaps and model robustness. |
| Object classification | Misclassification of occluded objects leading to false negatives | Low visibility, occlusion | Parking lots, low-speed reversing | False negatives leading to delayed warnings | Known | Data coverage gaps for occluded objects, label quality issues | Perform HARA for each function. | Uncertainty from data gaps and model robustness. |
| TTC estimation | Inaccurate TTC due to occlusion or sensor limitations | Low visibility, occlusion | Parking lots, low-speed reversing | Delayed warnings leading to collisions | Known | Data coverage gaps for occluded objects, label quality issues | Perform HARA for each function. | Uncertainty from data gaps and model robustness. |
| Warning arbitration | Insufficient performance in low-visibility conditions leading to delayed warnings | Low visibility, occlusion | Parking lots, low-speed reversing | Delayed warnings leading to collisions | Known | Data coverage gaps for occluded objects, label quality issues | Perform HARA for each function. | Uncertainty from data gaps and model robustness. |
| Driver HMI output | Insufficient performance in low-visibility conditions leading to delayed warnings | Low visibility, occlusion | Parking lots, low-speed reversing | Delayed warnings leading to collisions | Known | Data coverage gaps for occluded objects, label quality issues | Perform HARA for each function. | Uncertainty from data gaps and model robustness. |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Cross-traffic detection | Perception system | High-resolution sensor data, object labels | Data coverage gaps for occluded objects, label quality issues | Model robustness and uncertainty in low-visibility conditions | Distribution shift due to varying weather and lighting conditions | Perform HARA for each function. | Continuous monitoring of model performance, regular retraining with new data. | Uncertainty from data gaps and model robustness. |
| Object classification | Perception system | High-resolution sensor data, object labels | Data coverage gaps for occluded objects, label quality issues | Model robustness and uncertainty in low-visibility conditions | Distribution shift due to varying weather and lighting conditions | Perform HARA for each function. | Continuous monitoring of model performance, regular retraining with new data. | Uncertainty from data gaps and model robustness. |
| TTC estimation | Perception system | High-resolution sensor data, object labels | Data coverage gaps for occluded objects, label quality issues | Model robustness and uncertainty in low-visibility conditions | Distribution shift due to varying weather and lighting conditions | Perform HARA for each function. | Continuous monitoring of model performance, regular retraining with new data. | Uncertainty from data gaps and model robustness. |
| Warning arbitration | Decision logic | High-resolution sensor data, object labels | Data coverage gaps for occluded objects, label quality issues | Model robustness and uncertainty in low-visibility conditions | Distribution shift due to varying weather and lighting conditions | Perform HARA for each function. | Continuous monitoring of model performance, regular retraining with new data. | Uncertainty from data gaps and model robustness. |
| Driver HMI output | Warning display and audio alerts | High-resolution sensor data, object labels | Data coverage gaps for occluded objects, label quality issues | Model robustness and uncertainty in low-visibility conditions | Distribution shift due to varying weather and lighting conditions | Perform HARA for each function. | Continuous monitoring of model performance, regular retraining with new data. | Uncertainty from data gaps and model robustness. |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Cross-traffic detection | Occluded vehicle in low visibility | Correct object classification, TTC estimation | Correct warning display and audio alerts | HMI logs, sensor data, validation reports | Safety goal 1 |
| Object classification | Occluded pedestrian in low visibility | Correct object classification, TTC estimation | Correct warning display and audio alerts | HMI logs, sensor data, validation reports | Safety goal 2 |
| TTC estimation | Occluded vehicle in low visibility | Correct object classification, TTC estimation | Correct warning display and audio alerts | HMI logs, sensor data, validation reports | Safety goal 3 |
| Warning arbitration | Delayed warning due to occlusion | Correct decision on warning display | Correct warning display and audio alerts | HMI logs, sensor data, validation reports | Safety goal 4