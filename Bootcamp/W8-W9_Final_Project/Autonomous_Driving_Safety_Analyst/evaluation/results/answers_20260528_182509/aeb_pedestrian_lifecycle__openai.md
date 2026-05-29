### Safety Lifecycle for Developing an AEB Pedestrian System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that hazards caused by malfunctioning behavior of electrical/electronic systems are identified, classified, controlled, verified, validated, and managed across the safety lifecycle.
- **ISO 21448 (SOTIF)**: Addresses unsafe intended functionality due to performance limitations, ODD boundaries, and triggering conditions, complementing ISO 26262 by focusing on functional insufficiencies and foreseeable misuse.
- **ISO 8800**: Concentrates on AI/data/model assurance risks, covering AI-specific safety concerns such as data coverage, model behavior, robustness, uncertainty, and AI lifecycle controls.

#### 2. Item Definition
- **Functions**: Detect pedestrians, assess collision risk, and execute automatic emergency braking (AEB).
- **Inputs**: Sensor data (camera, LiDAR, radar), environmental conditions, vehicle dynamics.
- **Outputs**: Braking command, driver alerts.
- **ODD**: Urban environments, daylight and night conditions, various weather scenarios.
- **Assumptions**: Reliable sensor data, timely processing, and effective braking.
- **Safety Role**: Prevent pedestrian collisions by timely detection and braking.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Pedestrian Detection | Object position, velocity | Missed detection | Late detection in occlusion | False negatives | ISO 26262, SOTIF, ISO 8800 | Yes |
| Collision Risk Assessment | Collision probability | Incorrect risk assessment | Misjudged risk in complex scenarios | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| AEB Execution | Braking command | Delayed braking | Insufficient braking force | Integration delay | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|------------|------------|------------|---------|------------|-------------|
| Pedestrian Detection | Missed detection | Collision with pedestrian | Urban crossing | 30-50 km/h | Severe injury | Frequent in urban areas | Driver may not react in time | ASIL B | Moderate | Improve detection algorithms |
| Collision Risk Assessment | Incorrect risk assessment | Delayed AEB | Complex urban scenarios | 30-50 km/h | Severe injury | Frequent in complex scenarios | Driver may not react in time | ASIL B | Moderate | Enhance risk models |
| AEB Execution | Delayed braking | Collision with pedestrian | Urban crossing | 30-50 km/h | Severe injury | Frequent in urban areas | Driver may not react in time | ASIL B | Moderate | Optimize braking response |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Pedestrian Detection | Collision with pedestrian | ASIL B | Timely detection | ISO 26262 |
  | SG2 | Collision Risk Assessment | Delayed AEB | ASIL B | Accurate risk assessment | ISO 26262 |
  | SG3 | AEB Execution | Collision with pedestrian | ASIL B | Immediate braking | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed detection | Alert driver, reduce speed | Visual/audible alert | Reduced speed | Minimize collision risk |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|-----------------------------|--------------|-----------------------|
  | Sensor fusion | Perception module | Missed detection | Sensor health check | 100 ms | Simulation results |

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
| Pedestrian Detection | Late detection | Occlusion | Urban, daylight | Collision | Known | Simulation, field tests | Sensor fusion, speed reduction | Acceptable with mitigation |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Pedestrian Detection | Detect pedestrians | Diverse urban data | Occlusion scenarios | False negatives | Night/rain conditions | No regression on VRU scenarios | Near-miss monitoring | Acceptable with ongoing monitoring |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Pedestrian detection | Occlusion | Timely detection | Detection within 100 ms | Simulation results | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Operation Monitoring Evidence | Rationale |
|-----------------|-----------------|------------------|-------------------------------|------------------|-------------------------------|-----------|
| Production | Sensor misalignment | End-of-line calibration | Calibration within tolerance | Calibration records | Field performance data | Ensures sensor accuracy |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Reaction Time Assumption |
  |-----------|--------------|---------|----------|-----------|-----------|----------------|-----------------|-----------------------------|
  | 50 km/h | 5 km/h | Rain | Night | Yes | Urban | High | L2 | 1.5 seconds |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Occluded pedestrian | No detection | No braking | Collision | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |---------------------------|-----------------------|----------------------------|---------------------|----------------------|
  | Sensor failure | Late detection | False negatives | Sensor fusion | Simulation results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|-------------------------------|---------------|
  | Use sensor fusion | Late detection | Reduces occlusion risk | Detection within 100 ms | Acceptable |

#### 12. Final Safety Argument
The AEB pedestrian system's safety case integrates ISO 26262, SOTIF, and ISO 8800 standards to ensure comprehensive safety management. ISO 26262 addresses E/E malfunctions, SOTIF covers functional insufficiencies and ODD limits, and ISO 8800 ensures AI robustness and data quality. Together, they provide a robust framework for developing a safe and reliable AEB pedestrian system.