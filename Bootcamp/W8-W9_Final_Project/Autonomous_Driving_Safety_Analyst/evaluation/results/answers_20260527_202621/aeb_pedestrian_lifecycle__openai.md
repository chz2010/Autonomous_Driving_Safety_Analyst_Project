### Safety Lifecycle for Developing an AEB Pedestrian System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that hazards caused by malfunctioning behavior of electrical/electronic systems are identified, classified, controlled, verified, validated, and managed across the safety lifecycle.
- **ISO 21448 (SOTIF)**: Addresses unsafe intended functionality due to performance limitations, ODD boundaries, and triggering conditions, complementing ISO 26262 by focusing on functional insufficiencies and foreseeable misuse.
- **ISO 8800**: Concentrates on AI-specific safety concerns, including data coverage, model behavior, robustness, uncertainty, and AI lifecycle controls.

#### 2. Item Definition
- **Functions**: Detect pedestrians, assess collision risk, and execute automatic emergency braking.
- **Inputs**: Sensor data (camera, radar, LiDAR), environmental conditions, vehicle dynamics.
- **Outputs**: Braking command, HMI alerts.
- **ODD**: Urban environments, varied lighting/weather conditions.
- **Assumptions**: Reliable sensor data, timely processing, and effective braking.
- **Safety Role**: Prevent pedestrian collisions by timely detection and braking.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Pedestrian Detection | Object position, velocity | Missed detection | Late detection in occlusion | False negatives | ISO 26262, SOTIF, ISO 8800 | Yes |
| Collision Risk Assessment | Collision probability | Incorrect risk assessment | Misjudged risk in complex scenarios | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Braking Execution | Braking force | Delayed braking | Insufficient braking force | Actuator failure | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|-------------|-------------|-------------|---------|-------------|-------------|
| Pedestrian Detection | Missed detection | Collision with pedestrian | Urban crossing | 30-50 km/h | Severe injury | Frequent in urban areas | Limited driver intervention | ASIL B | High | Improve detection algorithms |
| Collision Risk Assessment | Incorrect risk assessment | Late braking | Complex urban scenarios | 30-50 km/h | Severe injury | Common in dense traffic | Limited driver intervention | ASIL B | Medium | Enhance risk models |
| Braking Execution | Delayed braking | Collision with pedestrian | Urban crossing | 30-50 km/h | Severe injury | Frequent in urban areas | Limited driver intervention | ASIL B | Low | Validate actuator response |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Pedestrian Detection | Collision with pedestrian | ASIL B | Timely detection | ISO 26262 |
  | SG2 | Collision Risk Assessment | Late braking | ASIL B | Accurate risk assessment | ISO 26262 |
  | SG3 | Braking Execution | Collision with pedestrian | ASIL B | Effective braking | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|---------------|-----------|
  | Missed detection | Alert driver, apply brakes | Visual/audible alert | Reduced speed | Minimize collision risk |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|---------------|-----------------------|
  | Sensor fusion | Perception module | Missed detection | Request driver intervention | < 100 ms | Simulation results |

#### 6. ISO 26262 Part 2-9 Lifecycle Table
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
|----------------|---------|--------------------------------------|------------------------|------------------------------------|---------------------------------|
| Part 2 | Functional safety management | Safety plan, DIA, confirmation measures | Safety plan, DIA | Ensure lifecycle safety | Complements SOTIF |
| Part 3 | Concept phase | Item definition, HARA, safety goals | HARA, safety goals | Identify hazards | Complements SOTIF |
| Part 4 | System development | Technical safety concept, architecture | System architecture | Prevent system-level failures | Complements SOTIF |
| Part 5 | Hardware development | Hardware safety requirements, FMEDA | FMEDA report | Address hardware faults | Complements SOTIF |
| Part 6 | Software development | Software safety requirements, tests | Software test results | Address software faults | Complements SOTIF |
| Part 7 | Production and operation | Production planning, field monitoring | Production plan | Ensure operational safety | Complements SOTIF |
| Part 8 | Supporting processes | Configuration/change management | Configuration records | Maintain process integrity | Complements SOTIF |
| Part 9 | Safety analyses | ASIL decomposition, FMEA | FMEA report | Analyze failure modes | Complements SOTIF |

#### 7. SOTIF Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known/Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|-------------------------|--------------|-------------------------------|---------------------------|------------------------|-------------------------|
| Pedestrian Detection | Late detection | Occlusion | Urban environment | Collision | Known | Simulation, field tests | Increase sensor coverage | Acceptable with mitigation |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|----------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Pedestrian Detection | Detect pedestrians | Diverse urban data | Occlusion scenarios | High in occlusion | High in new environments | Performance threshold | Field performance logs | Acceptable with monitoring |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|-------------------|--------------------|
| Pedestrian detection | Occlusion | Timely detection | Detection within 100 ms | Test report | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|-------------------|--------------|-----------|
| Production | Sensor misalignment | Calibration checks | Alignment within tolerance | Calibration logs | Field feedback | Ensure sensor accuracy |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Available Sensing Time | Driver Fallback Assumption | Road Friction |
  |-----------|--------------|---------|----------|-----------|-----------|----------------|-----------------|---------------------------|---------------------------|--------------|
  | 50 km/h | 5 km/h | Clear | Daylight | High | Urban | High | L2 | 2 seconds | Limited | Normal |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Occluded pedestrian | No detection | No braking | Collision | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|----------------------------|---------------------|----------------------|
  | Sensor failure | Occlusion | Model uncertainty | Sensor fusion | Simulation results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Add radar | Occlusion risk | Redundant detection | Detection in occlusion | Low |

#### 12. Final Safety Argument
The integration of ISO 26262, SOTIF, and ISO 8800 ensures a comprehensive safety case for the AEB pedestrian system, addressing E/E malfunctions, functional insufficiencies, and AI-specific concerns. This lifecycle approach provides a robust framework for developing, validating, and operating the system safely across its intended operational domain.