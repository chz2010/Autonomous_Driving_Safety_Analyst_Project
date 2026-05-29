### Opening Map

- **ISO 26262 = E/E malfunction risk**: The lane maintaining perception system relies on sensors and software to detect lane markings, obstacles, and other vehicles.
- **SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**: The system must handle various driving scenarios within the defined operational design domain (ODD).
- **ISO 8800 = AI/data/model assurance risk**: The perception system uses machine learning models to interpret sensor data, which requires robustness and uncertainty analysis.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Lane Detection | Detect lane markings and obstacles | Sensor failure, software bug | Inadequate perception confidence in low-light conditions | Dataset bias towards daytime driving scenarios | ISO 26262, ISO 21448, ISO 8800 | Yes |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Lane Detection | Detect lane markings and obstacles | Sensor failure, software bug | Inadequate perception confidence in low-light conditions | Dataset bias towards daytime driving scenarios | ISO 26262, ISO 21448, ISO 8800 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Lane Detection | Sensor failure, software bug | Collision with vehicle or obstacle in lane | Urban road, 30-50 km/h ego speed, moderate traffic density | Ego: 40 km/h; Object: 20 km/h | Severity: High (potential for severe injury) | Exposure: Moderate (urban driving conditions) | Controllability: Low (driver fallback not always available) | ASIL C | Uncertainty: High (sensor and software reliability) | Review sensor and software diagnostics |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Lane Detection | Collision with vehicle or obstacle in lane | ASIL C | Maintain safe distance from obstacles and follow lane markings | ISO 26262 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Reduce speed, increase headway | HMI warning: "Sensor issue detected" | Lane Keeping Assist (LKA) disabled | Ensure safe operation even with sensor issues |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor redundancy | Redundant cameras and LiDAR | Sensor failure detection | Diagnostics check every 100 ms | Real-time | Diagnostic logs, sensor health checks |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Define safety goals and functional safety concept.
- **Work Products/Evidence**: HARA results, safety goals table, functional safety concept table.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system operates safely within its ODD.

#### Part 3: Item Definition
- **Item-Specific Engineering Activities**: Define functions, inputs, outputs, interfaces, and ODD assumptions.
- **Work Products/Evidence**: Functional decomposition, HARA screening results.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system meets safety goals.

#### Part 4: System Development
- **Item-Specific Engineering Activities**: Develop software and hardware, integrate components, validate functionality.
- **Work Products/Evidence**: Software architecture, integration tests, validation reports.
- **Rationale/Unsafe Behavior Prevented**: Ensure safe operation through robust design and testing.

#### Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Design and test hardware components.
- **Work Products/Evidence**: FMEDA, diagnostic coverage, LFM metrics.
- **Rationale/Unsafe Behavior Prevented**: Ensure hardware reliability.

#### Part 6: Software Development
- **Item-Specific Engineering Activities**: Develop software, perform unit tests, integration tests.
- **Work Products/Evidence**: Unit test results, integration test logs.
- **Rationale/Unsafe Behavior Prevented**: Ensure software robustness and reliability.

#### Part 7: Production
- **Item-Specific Engineering Activities**: Calibration, service recalibration, DTC management.
- **Work Products/Evidence**: End-of-line calibration reports, DTC logs.
- **Rationale/Unsafe Behavior Prevented**: Ensure consistent system performance post-production.

#### Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Change logs, test plans, requirement matrices.
- **Rationale/Unsafe Behavior Prevented**: Maintain safety through systematic processes.

#### Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Perform ASIL decomposition and dependent failure analysis.
- **Work Products/Evidence**: ASIL decomposition table, fault tree analysis (FTA).
- **Rationale/Unsafe Behavior Prevented**: Ensure the system meets required safety levels.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Lane Detection | Inadequate perception confidence in low-light conditions | Rain, fog, night driving | Urban roads with moderate traffic density | Reduced stopping distance, increased risk of collision | Known but not fully characterized | Sensor and model validation tests | Reduce speed, increase headway | Risk remains high due to limited data coverage |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Lane Detection Model | Perception and obstacle avoidance | High-resolution sensor data, diverse driving scenarios | Daytime bias in training dataset | Overfitting to daytime conditions | Night-time driving not well represented | 90% accuracy across all weather conditions | Continuous monitoring of model performance | Risk remains due to limited OOD testing |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Accept Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor Failure Test | Simulate sensor failure | System reduces speed, increases headway | Diagnostics check every 100 ms | Diagnostic logs | SG1 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor accuracy | Calibrate sensors at EOL | 95% accuracy within tolerance | Calibration reports | Continuous monitoring | Ensure consistent performance |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 40 km/h | 20 km/h | Rainy | Dim | None | Urban road | Moderate | L2+ |

#### Accident-Chain Table
1. Ego speed: 40 km/h; Object speed: 20 km/h.
2. Degraded signal: Sensor failure due to rain.
3. System interpretation: Reduced perception confidence.
4. Vehicle response: Increased headway but not enough to avoid collision.
5. Hazard escalation: Collision with obstacle in lane.

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure | Inadequate perception confidence in low-light conditions | Overfitting to daytime conditions | Reduce speed, increase headway | Diagnostic logs |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Accept Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Increase sensor redundancy and diagnostic checks | High | Ensure robust operation in adverse conditions | 95% accuracy within tolerance | Risk remains due to limited OOD testing |

### Final Safety Argument

- **ISO 26262**: The system is designed with ASIL C requirements, ensuring safe operation through hardware and software diagnostics.
- **SOTIF**: The system handles triggering conditions such as rain and low light by reducing speed and increasing headway.
- **ISO 8800**: The perception model is validated for robustness and uncertainty, but limited OOD testing remains a risk.

By integrating these standards, the lane maintaining perception system ensures safe operation within its defined ODD. Continuous monitoring and improvement of data quality and model robustness are critical to reducing residual risks.