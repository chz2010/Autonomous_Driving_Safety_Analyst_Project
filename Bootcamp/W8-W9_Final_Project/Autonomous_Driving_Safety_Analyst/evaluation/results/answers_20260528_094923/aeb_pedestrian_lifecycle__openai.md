### Safety Lifecycle for Developing an AEB Pedestrian System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that the system's electrical and electronic components do not fail in a way that causes harm.
- **ISO 21448 (SOTIF)**: Addresses the safety of the intended functionality, focusing on limitations, ODD boundaries, and triggering conditions that could lead to unsafe behavior even when the system functions as designed.
- **ISO 8800**: Concerns AI/data/model assurance, focusing on the robustness, data quality, and lifecycle management of AI components within the system.

#### 2. Item Definition
- **Functions**: Detect pedestrians, assess collision risk, and apply brakes if necessary.
- **Inputs**: Sensor data (camera, radar, LiDAR), vehicle speed, environmental conditions.
- **Outputs**: Brake actuation, driver alerts.
- **Interfaces**: Vehicle CAN bus, HMI for driver alerts.
- **ODD**: Urban environments, daylight and nighttime, clear and adverse weather.
- **Assumptions**: Reliable sensor data, timely processing, and effective braking.
- **Safety Role**: Prevent collisions with pedestrians by timely braking.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Pedestrian Detection | Detection signal | Missed detection | False negatives in occlusion | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Collision Risk Assessment | Risk level | Incorrect risk calculation | Misjudgment in complex scenarios | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Brake Actuation | Brake command | Delayed actuation | Over-reliance on system | Control robustness | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|-------------|-------------|-------------|---------|-------------|-------------|
| Pedestrian Detection | Missed detection | Collision with pedestrian | Urban, moderate traffic | 30-50 km/h | Severe injury | Frequent in urban | Difficult to control | ASIL B | High | Improve detection algorithms |
| Collision Risk Assessment | Incorrect risk | Late braking | Urban, complex intersections | 30-50 km/h | Severe injury | Common in intersections | Moderate control | ASIL C | Medium | Enhance risk models |
| Brake Actuation | Delayed actuation | Collision | Urban, pedestrian crossing | 30-50 km/h | Severe injury | Frequent crossings | Difficult to control | ASIL D | Low | Optimize braking response |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Pedestrian Detection | Collision with pedestrian | ASIL B | Alert driver | ISO 26262 |
  | SG2 | Collision Risk Assessment | Late braking | ASIL C | Reduce speed | ISO 26262 |
  | SG3 | Brake Actuation | Collision | ASIL D | Full stop | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed detection | Alert driver | Visual/audible alert | Manual braking | Reduces collision risk |
  | Incorrect risk | Reduce speed | Visual alert | Manual intervention | Mitigates late response |
  | Delayed actuation | Full stop | None | Emergency braking | Prevents collision |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|---------------|-----------------------|
  | Sensor fusion | ECU | Missed detection | Redundant sensing | 100 ms | Sensor test results |
  | Risk model | ECU | Incorrect risk | Model update | 200 ms | Simulation results |
  | Brake control | Brake system | Delayed actuation | Emergency braking | 50 ms | Brake test results |

#### 6. ISO 26262 Part 2-9 Lifecycle Table
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
|----------------|---------|--------------------------------------|------------------------|------------------------------------|---------------------------------|
| Part 2 | Functional safety management | Safety plan, DIA, confirmation measures | Safety plan, DIA | Ensures structured safety management | Aligns with SOTIF risk analysis |
| Part 3 | Concept phase | Item definition, HARA, safety goals | HARA report, safety goals | Identifies hazards and safety goals | Supports SOTIF scenario analysis |
| Part 4 | System development | Technical safety concept, architecture | System architecture | Defines safe system behavior | Integrates SOTIF limitations |
| Part 5 | Hardware development | FMEDA, random hardware metrics | FMEDA report | Ensures hardware reliability | Complements SOTIF hardware checks |
| Part 6 | Software development | Software safety requirements, tests | Software test results | Verifies software safety | Addresses ISO 8800 model concerns |
| Part 7 | Production and operation | Production planning, field monitoring | Production plan, field data | Ensures safe operation | Monitors SOTIF and ISO 8800 risks |
| Part 8 | Supporting processes | Configuration/change management | Configuration records | Maintains traceability | Supports SOTIF/ISO 8800 updates |
| Part 9 | Safety analyses | ASIL decomposition, FMEA, FTA | Analysis reports | Identifies failure modes | Informs SOTIF/ISO 8800 scenarios |

#### 7. SOTIF Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known/Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|-------------------------|--------------|-------------------------------|---------------------------|------------------------|-------------------------|
| Pedestrian Detection | Occlusion | Parked cars | Urban, clear weather | Missed detection | Known | Occlusion tests | Sensor fusion | Reduced with redundancy |
| Collision Risk Assessment | Complex scenarios | Intersections | Urban, moderate traffic | Late braking | Unknown | Intersection tests | Model update | Managed with model improvements |
| Brake Actuation | Over-reliance | High-speed approach | Urban, low speed | Delayed braking | Known | Speed tests | Emergency braking | Minimized with fast response |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|-----------------------------|------------------------|-------------------------------|-----------------------------|
| Pedestrian Detection | Accurate detection | Diverse pedestrian data | Bias in occlusion | High uncertainty in occlusion | High in new environments | Detection accuracy | Continuous monitoring | Managed with diverse datasets |
| Collision Risk Assessment | Accurate risk assessment | Complex scenario data | Limited intersection data | Model uncertainty | Moderate in intersections | Risk model accuracy | Scenario-based testing | Reduced with scenario coverage |
| Brake Actuation | Timely braking | Real-time data | Delay in high-speed | Control robustness | Low in urban | Braking response time | Real-time monitoring | Minimized with fast actuation |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Pedestrian detection test | Occlusion | Accurate detection | 95% detection rate | Test report | SG1 |
| Risk assessment test | Complex intersection | Correct risk level | 90% accuracy | Simulation results | SG2 |
| Brake actuation test | High-speed approach | Timely braking | 100 ms response | Brake test results | SG3 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|-----------------|-----------------|-------------------------------|------------------|---------------|-----------|
| Production | Sensor misalignment | Calibration | Alignment within tolerance | Calibration records | End-of-line checks | Ensures sensor accuracy |
| Operation | Sensor degradation | Health checks | Sensor status OK | Health check logs | Field monitoring | Maintains sensor reliability |
| Service | Software update | Version control | Correct version installed | Update records | OTA updates | Ensures software integrity |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Available Sensing Time | Driver Fallback Assumption |
  |-----------|--------------|---------|----------|-----------|----------|-----------------|-----------------|----------------------------|---------------------------|
  | 50 km/h | 5 km/h | Clear | Daylight | Parked cars | Urban | Moderate | AEB active | 2 seconds | Driver alert |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Missed pedestrian | No detection | No braking | Collision | Detection logs |
  | 2 | Incorrect risk | Low risk | Delayed braking | Collision | Risk assessment logs |
  | 3 | Delayed actuation | Late command | Insufficient braking | Collision | Brake actuation logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|----------------------------|---------------------|-----------------------|
  | Sensor failure | Occlusion | Dataset bias | Sensor fusion | Sensor test results |
  | Risk miscalculation | Complex scenarios | Model uncertainty | Model update | Simulation results |
  | Brake delay | High-speed approach | Control robustness | Emergency braking | Brake test results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Improve sensor fusion | Missed detection | Reduces occlusion risk | 95% detection rate | Low |
  | Enhance risk models | Incorrect risk | Improves scenario handling | 90% accuracy | Medium |
  | Optimize braking response | Delayed actuation | Ensures timely braking | 100 ms response | Low |

#### 12. Final Safety Argument
The AEB pedestrian system's safety case integrates ISO 26262, SOTIF, and ISO 8800 to ensure comprehensive safety coverage. ISO 26262 addresses E/E malfunctions, SOTIF covers intended functionality limitations, and ISO 8800 ensures AI robustness and data quality. Together, these standards provide a robust framework for developing a safe and reliable AEB pedestrian system.