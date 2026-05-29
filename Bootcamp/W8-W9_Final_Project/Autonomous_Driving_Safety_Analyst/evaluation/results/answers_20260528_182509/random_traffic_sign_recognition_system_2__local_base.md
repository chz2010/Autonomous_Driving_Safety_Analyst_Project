### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Evaluates intended-function insufficiencies, performance limitations, foreseeable misuse, and triggering conditions.
- **ISO 8800**: Ensures AI/data/model robustness, uncertainty management, and distribution shift.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Sign Detection | Object coordinates, confidence score | Sensor failure, incorrect detection | Inadequate perception under low visibility and occlusion | Insufficient performance in low-visibility scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Sign Detection | Object coordinates, confidence score | Sensor failure, incorrect detection | Inadequate perception under low visibility and occlusion | Insufficient performance in low-visibility scenarios | ISO 26262, SOTIF, ISO 8800 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Sign Detection | Sensor failure, incorrect detection | Collision with sign | Low visibility and partial occlusion on urban/rural/highway roads | 30-50 km/h, 80-130 km/h | High risk of collision; potential for severe injury or death | Occurs frequently in low-visibility scenarios | Driver can take corrective action but limited time | ASIL B-C | Moderate uncertainty due to varying visibility conditions | Detailed HARA |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG01 | Sign Detection | Collision with sign | ASIL B-C | Display warning to driver and reduce speed if possible | ISO 26262, SOTIF, ISO 8800 |

| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Emergency braking and warning display | Warning message to driver | Reduced speed limit in low-visibility conditions | Ensures safety under malfunction |

| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor failure detection | ECU | Sensor failure | Diagnostics and fallback logic | Real-time | Unit tests, integration tests |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Item Definition**: Defined sign detection function.
- **Supplier Interface**: Supplier provided sensor data with known limitations.
- **Safety Plan**: HARA and ASIL classification performed.
- **Confirmation Measures**: Unit tests, integration tests.
- **Impact Analysis**: Identified potential E/E failures.
- **Release Responsibilities**: Ensured safety requirements met.

#### Part 3: Item Definition
- **ODD Assumptions**: Urban/rural/highway roads with regional sign variants.
- **HARA**: Performed HARA for sign detection function.
- **S/E/C**: Evaluated severity, exposure, controllability.
- **ASIL**: ASIL B-C classification.

#### Part 4: System Development
- **Technical Safety Concept**: Defined safety goals and functional safety concept.
- **Architecture**: Designed system architecture with redundancy.
- **Requirements Allocation**: Allocated requirements to hardware/software components.
- **Integration**: Integrated sign detection into overall system.
- **Validation**: Conducted unit tests, integration tests.

#### Part 5: Hardware Development
- **Hardware Safety Requirements**: Defined hardware safety requirements.
- **FMEDA**: Performed Failure Modes and Effects Analysis (FMEA).
- **Random Hardware Metrics**: Monitored random hardware failures.
- **Diagnostic Coverage**: Implemented diagnostic coverage for sensor failure detection.

#### Part 6: Software Development
- **Software Safety Requirements**: Defined software safety requirements.
- **Architecture**: Designed software architecture with fault tolerance.
- **Freedom from Interference**: Ensured software is free from interference.
- **Freshness/Plausibility Checks**: Implemented checks to ensure data freshness.
- **Watchdog**: Used watchdog timers for real-time monitoring.

#### Part 7: Production
- **Operation**: Monitored system operation and performance.
- **Service**: Provided service recalibration and DTCs.
- **Decommissioning**: Planned decommissioning procedures.

#### Part 8: Supporting Processes
- **Configuration/Change Management**: Managed configuration changes.
- **Requirements Traceability**: Traced requirements to implementation.
- **Verification Planning**: Developed verification plans.
- **Documentation**: Maintained documentation for safety case evidence.

#### Part 9: ASIL Decomposition
- **Dependent Failure Analysis**: Analyzed dependent failures.
- **Common-Cause/Cascading Failure Analysis**: Identified common causes and cascading effects.
- **Freedom from Interference**: Ensured system is free from interference.
- **FMEA, FTA, DFA**: Performed failure mode analysis.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Sign Detection | Inadequate performance in low visibility and occlusion | Low visibility, partial occlusion | Urban/rural/highway roads with regional sign variants | Collision risk | Known scenario | Detailed HARA, sensor validation tests | Increased fallback time | Moderate residual risk due to varying visibility conditions |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Sign Detection | Ensuring accurate detection under varying conditions | High-resolution sensor data, diverse sign types | Limited dataset coverage for occlusion and low visibility | Model robustness in varying lighting conditions | Distribution shift due to regional sign variants | Comprehensive validation tests | Continuous monitoring of model performance | Moderate residual risk due to limited dataset coverage |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor Failure Detection | Simulated sensor failure | Correct warning display, reduced speed limit | No false positives/negatives | Unit test logs, integration test results | SG01 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Operation Monitoring Evidence | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor calibration drift | Calibrate sensors at end of line | No significant drift detected | Calibration logs, sensor test results | Regular calibration checks | Ensures accurate sign detection |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 30-50 | 10-20 | Rainy | Dim | Partial occlusion | Urban/rural/highway | Moderate | L2+ | 2-4 seconds | Limited |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure, occlusion | Inaccurate sign detection | Incorrect speed limit adjustment | Increased collision risk | HARA results, sensor validation tests |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure detection | Inadequate performance in low visibility and occlusion | Model robustness under varying conditions | Increased fallback time, continuous monitoring | Unit test logs, integration test results |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Increase sensor redundancy and fallback time | Moderate risk reduction | Ensures timely response in low visibility conditions | No false positives/negatives, no significant drift detected | Moderate residual risk due to varying visibility conditions |

### Final Safety Argument

- **ISO 26262**: Ensured safety through HARA, ASIL classification, and functional safety concept.
- **SOTIF**: Addressed performance limitations in low-visibility scenarios with fallback time and continuous monitoring.
- **ISO 8800**: Managed AI robustness and uncertainty through comprehensive validation tests.

This detailed analysis ensures a holistic approach to the traffic sign recognition system's safety across ISO 26262, SOTIF, and ISO 8800 standards.