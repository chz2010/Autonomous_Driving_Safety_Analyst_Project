### Safety Lifecycle and Item Safety Case for a Minimal-Risk Maneuver Controller

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring hazards caused by malfunctioning behavior of electrical/electronic systems are identified, classified, controlled, verified, validated, and managed across the safety lifecycle.
- **ISO 21448 (SOTIF)**: Addresses unsafe intended functionality due to performance limitations, ODD boundaries, and triggering conditions, complementing ISO 26262 by focusing on functional insufficiencies and foreseeable misuse.
- **ISO 8800**: Concentrates on AI/data/model assurance risks, covering AI-specific safety concerns such as data coverage, model behavior, robustness, uncertainty, and AI lifecycle controls.

#### 2. Item Definition
- **Functions**: Failure detection, fallback trajectory selection, hazard-light request, controlled deceleration, safe-stop confirmation.
- **Inputs**: Sensor data, vehicle dynamics, environmental conditions.
- **Outputs**: Steering and braking commands, hazard light activation.
- **ODD**: L3 highway pilot fallback after perception or actuator degradation.
- **Assumptions**: Reliable sensor data, timely processing, and effective control.
- **Safety Role**: Ensure vehicle safety during fallback maneuvers to a minimal-risk condition.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Failure Detection | Fault signal | Missed fault | Late detection | False negatives | ISO 26262, SOTIF, ISO 8800 | Yes |
| Fallback Trajectory Selection | Safe path | Incorrect path | Path not safe in all conditions | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Hazard-Light Request | Light activation | No activation | Late activation | Integration delay | ISO 26262, SOTIF | Yes |
| Controlled Deceleration | Braking command | Delayed braking | Insufficient braking force | Integration delay | ISO 26262, SOTIF | Yes |
| Safe-Stop Confirmation | Stop confirmation | No confirmation | Late confirmation | False negatives | ISO 26262, SOTIF, ISO 8800 | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|------------|------------|------------|---------|------------|-------------|
| Failure Detection | Missed fault | Uncontrolled vehicle | Highway fallback | 80-130 km/h | Severe injury | Frequent on highways | Driver may not react in time | ASIL C | Moderate | Improve detection algorithms |
| Fallback Trajectory Selection | Incorrect path | Unsafe maneuver | Highway fallback | 80-130 km/h | Severe injury | Frequent in fallback scenarios | Driver may not react in time | ASIL C | Moderate | Enhance path models |
| Hazard-Light Request | No activation | Reduced visibility | Highway fallback | 80-130 km/h | Moderate injury | Frequent in fallback scenarios | Driver may not react in time | ASIL B | Moderate | Optimize light activation |
| Controlled Deceleration | Delayed braking | Collision | Highway fallback | 80-130 km/h | Severe injury | Frequent on highways | Driver may not react in time | ASIL C | Moderate | Optimize braking response |
| Safe-Stop Confirmation | No confirmation | Vehicle not stopped | Highway fallback | 80-130 km/h | Severe injury | Frequent in fallback scenarios | Driver may not react in time | ASIL C | Moderate | Improve confirmation logic |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Failure Detection | Uncontrolled vehicle | ASIL C | Timely fault detection | ISO 26262 |
  | SG2 | Fallback Trajectory Selection | Unsafe maneuver | ASIL C | Safe path selection | ISO 26262 |
  | SG3 | Hazard-Light Request | Reduced visibility | ASIL B | Immediate light activation | ISO 26262 |
  | SG4 | Controlled Deceleration | Collision | ASIL C | Immediate braking | ISO 26262 |
  | SG5 | Safe-Stop Confirmation | Vehicle not stopped | ASIL C | Confirmed stop | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed fault | Alert driver, maintain control | Visual/audible alert | Reduced speed | Minimize risk |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|-----------------------------|--------------|-----------------------|
  | Sensor fusion | Perception module | Missed fault | Sensor health check | 100 ms | Simulation results |

#### 6. ISO 26262 Part 2-9 Lifecycle Table
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
|----------------|---------|--------------------------------------|------------------------|------------------------------------|---------------------------------|
| Part 2 | Functional safety management | Safety plan, DIA, confirmation measures | Safety plan, DIA | Ensures structured safety management | Complements SOTIF risk management |
| Part 3 | Concept phase | Item definition, HARA, safety goals | HARA table, safety goals | Identifies and mitigates hazards | Supports SOTIF scenario analysis |
| Part 4 | System development | Technical safety concept, architecture | System architecture | Ensures system meets safety goals | Integrates SOTIF performance limits |
| Part 5 | Hardware development | Hardware safety requirements, FMEDA | FMEDA report | Mitigates hardware faults | Supports ISO 8800 robustness checks |
| Part 6 | Software development | Software safety requirements, tests | Software test reports | Ensures software reliability | Validates ISO 8800 AI behavior |
| Part 7 | Production and operation | Production/service plans, field monitoring | Production plan, field data | Ensures ongoing safety | Monitors SOTIF/ISO 8800 performance |
| Part 8 | Supporting processes | Configuration/change management | Configuration records | Maintains traceability | Supports ISO 8800 change control |
| Part 9 | Safety analyses | ASIL decomposition, FMEA | FMEA report | Identifies failure modes | Complements SOTIF scenario analysis |

#### 7. SOTIF Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known/Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|-------------------------|--------------|-------------------------------|---------------------------|------------------------|-------------------------|
| Failure Detection | Late detection | Sensor degradation | Highway, daylight | Uncontrolled vehicle | Known | Simulation, field tests | Sensor fusion, speed reduction | Acceptable with mitigation |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Fallback Trajectory Selection | Select safe path | Diverse highway data | Path scenarios | False negatives | Night/rain conditions | No regression on path scenarios | Near-miss monitoring | Acceptable with ongoing monitoring |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Failure detection | Sensor degradation | Timely detection | Detection within 100 ms | Simulation results | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Operation Monitoring Evidence | Rationale |
|-----------------|-----------------|------------------|-------------------------------|------------------|-------------------------------|-----------|
| Production | Sensor misalignment | End-of-line calibration | Calibration within tolerance | Calibration records | Field performance data | Ensures sensor accuracy |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Reaction Time Assumption |
  |-----------|--------------|---------|----------|-----------|-----------|----------------|-----------------|-----------------------------|
  | 100 km/h | N/A | Rain | Night | Yes | Highway | Moderate | L3 | 1.5 seconds |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Sensor degradation | No fault detection | No fallback | Uncontrolled vehicle | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |---------------------------|-----------------------|----------------------------|---------------------|----------------------|
  | Sensor failure | Late detection | False negatives | Sensor fusion | Simulation results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|-------------------------------|---------------|
  | Use sensor fusion | Late detection | Reduces degradation risk | Detection within 100 ms | Acceptable |

#### 12. Final Safety Argument
The minimal-risk maneuver controller's safety case integrates ISO 26262, SOTIF, and ISO 8800 standards to ensure comprehensive safety management. ISO 26262 addresses E/E malfunctions, SOTIF covers functional insufficiencies and ODD limits, and ISO 8800 ensures AI robustness and data quality. Together, they provide a robust framework for developing a safe and reliable minimal-risk maneuver controller.