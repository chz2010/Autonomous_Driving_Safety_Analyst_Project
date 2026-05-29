### Safety Lifecycle and Item Safety Case for a Minimal-Risk Maneuver Controller

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that the system's electrical and electronic components do not fail in a way that causes harm.
- **ISO 21448 (SOTIF)**: Addresses the safety of the intended functionality, focusing on limitations, ODD boundaries, and triggering conditions that could lead to unsafe behavior even when the system functions as designed.
- **ISO 8800**: Concerns AI/data/model assurance, focusing on the robustness, data quality, and lifecycle management of AI components within the system.

#### 2. Item Definition
- **Functions**: Failure detection, fallback trajectory selection, hazard-light request, controlled deceleration, safe-stop confirmation.
- **Inputs**: Sensor data (camera, radar, LiDAR), vehicle speed, environmental conditions.
- **Outputs**: Trajectory commands, hazard light activation, deceleration control.
- **Interfaces**: Vehicle CAN bus, HMI for driver alerts.
- **ODD**: L3 highway pilot fallback after perception or actuator degradation.
- **Assumptions**: Reliable sensor data, timely processing, and effective fallback execution.
- **Safety Role**: Ensure safe vehicle stop in case of system degradation or failure.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Failure Detection | Fault signal | Missed fault | False negatives in degraded conditions | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Fallback Trajectory Selection | Trajectory command | Incorrect trajectory | Misjudgment in complex scenarios | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Hazard-Light Request | Light activation | Delayed activation | Over-reliance on system | Control robustness | ISO 26262, SOTIF | Yes |
| Controlled Deceleration | Deceleration command | Delayed deceleration | Inadequate deceleration timing | Interface latency | ISO 26262, SOTIF | Yes |
| Safe-Stop Confirmation | Stop confirmation | Incorrect confirmation | Misleading information | Display reliability | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|-------------|-------------|-------------|---------|-------------|-------------|
| Failure Detection | Missed fault | Uncontrolled vehicle | Highway, moderate traffic | 80-120 km/h | Severe injury | Frequent on highways | Difficult to control | ASIL C | High | Improve detection algorithms |
| Fallback Trajectory Selection | Incorrect trajectory | Unsafe stop | Highway, complex scenarios | 80-120 km/h | Severe injury | Common in complex scenarios | Moderate control | ASIL D | Medium | Enhance trajectory models |
| Hazard-Light Request | Delayed activation | Collision | Highway, high speed | 80-120 km/h | Severe injury | Frequent on highways | Difficult to control | ASIL D | Low | Optimize light activation |
| Controlled Deceleration | Delayed deceleration | Collision | Highway, pedestrian crossing | 80-120 km/h | Severe injury | Frequent crossings | Difficult to control | ASIL D | Low | Optimize deceleration response |
| Safe-Stop Confirmation | Incorrect confirmation | Driver confusion | Highway, moderate traffic | 80-120 km/h | Moderate injury | Common in urban | Moderate control | ASIL B | Medium | Improve confirmation reliability |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Failure Detection | Uncontrolled vehicle | ASIL C | Alert driver | ISO 26262 |
  | SG2 | Fallback Trajectory Selection | Unsafe stop | ASIL D | Safe trajectory | ISO 26262 |
  | SG3 | Hazard-Light Request | Collision | ASIL D | Immediate activation | ISO 26262 |
  | SG4 | Controlled Deceleration | Collision | ASIL D | Controlled stop | ISO 26262 |
  | SG5 | Safe-Stop Confirmation | Driver confusion | ASIL B | Clear confirmation | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed fault | Alert driver | Visual/audible alert | Manual intervention | Reduces collision risk |
  | Incorrect trajectory | Safe trajectory | Visual alert | Manual intervention | Mitigates unsafe stop |
  | Delayed activation | Immediate activation | None | Emergency alert | Prevents collision |
  | Delayed deceleration | Controlled stop | None | Emergency deceleration | Prevents collision |
  | Incorrect confirmation | Clear confirmation | None | Manual check | Prevents confusion |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|---------------|-----------------------|
  | Sensor fusion | ECU | Missed fault | Redundant sensing | 100 ms | Sensor test results |
  | Trajectory model | ECU | Incorrect trajectory | Model update | 200 ms | Simulation results |
  | Light control | ECU | Delayed activation | Immediate alert | 50 ms | Light test results |
  | Deceleration control | Brake system | Delayed deceleration | Emergency deceleration | 50 ms | Deceleration test results |
  | Confirmation system | Display | Incorrect confirmation | Manual check | 100 ms | Confirmation test results |

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
| Failure Detection | Degraded conditions | Sensor failure | Highway, clear weather | Missed fault | Known | Degraded condition tests | Sensor fusion | Reduced with redundancy |
| Fallback Trajectory Selection | Complex scenarios | Intersections | Highway, moderate traffic | Unsafe stop | Unknown | Scenario tests | Model update | Managed with model improvements |
| Hazard-Light Request | Over-reliance | High-speed approach | Highway, low speed | Delayed activation | Known | Timing tests | Immediate alert | Minimized with fast response |
| Controlled Deceleration | Inadequate timing | High-speed approach | Highway, low speed | Delayed deceleration | Known | Timing tests | Emergency deceleration | Minimized with fast response |
| Safe-Stop Confirmation | Misleading information | Complex intersections | Highway, moderate traffic | Incorrect confirmation | Unknown | Interface tests | Manual check | Managed with interface improvements |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|-----------------------------|------------------------|-------------------------------|-----------------------------|
| Failure Detection | Accurate detection | Diverse fault data | Bias in degraded conditions | High uncertainty in degradation | High in new environments | Detection accuracy | Continuous monitoring | Managed with diverse datasets |
| Fallback Trajectory Selection | Accurate trajectory selection | Complex scenario data | Limited intersection data | Model uncertainty | Moderate in intersections | Trajectory model accuracy | Scenario-based testing | Reduced with scenario coverage |
| Hazard-Light Request | Timely activation | Real-time data | Delay in high-speed | Control robustness | Low in urban | Light activation time | Real-time monitoring | Minimized with fast actuation |
| Controlled Deceleration | Timely deceleration | Real-time data | Delay in high-speed | Deceleration robustness | Low in urban | Deceleration response time | Real-time monitoring | Minimized with fast actuation |
| Safe-Stop Confirmation | Reliable confirmation | Real-time data | Delay in complex scenarios | Confirmation robustness | Low in urban | Confirmation display time | Real-time monitoring | Minimized with fast actuation |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Failure detection test | Degraded conditions | Accurate detection | 95% detection rate | Test report | SG1 |
| Trajectory selection test | Complex scenario | Correct trajectory | 90% accuracy | Simulation results | SG2 |
| Hazard-light request test | High-speed approach | Timely activation | 50 ms response | Light test results | SG3 |
| Controlled deceleration test | High-speed approach | Timely deceleration | 50 ms response | Deceleration test results | SG4 |
| Safe-stop confirmation test | Complex intersection | Clear confirmation | 100 ms response | Confirmation test results | SG5 |

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
  | 100 km/h | N/A | Moderate rain | Night | Parked cars | Highway | Moderate | Minimal-risk maneuver active | 2 seconds | Driver alert |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Missed fault | No detection | No warning | Collision | Detection logs |
  | 2 | Incorrect trajectory | Low risk | Delayed warning | Collision | Trajectory assessment logs |
  | 3 | Delayed activation | Late command | Insufficient warning | Collision | Light activation logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|----------------------------|---------------------|-----------------------|
  | Sensor failure | Degraded conditions | Dataset bias | Sensor fusion | Sensor test results |
  | Trajectory miscalculation | Complex scenarios | Model uncertainty | Model update | Simulation results |
  | Activation delay | High-speed approach | Control robustness | Immediate alert | Light test results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Improve sensor fusion | Missed fault | Reduces degradation risk | 95% detection rate | Low |
  | Enhance trajectory models | Incorrect trajectory | Improves scenario handling | 90% accuracy | Medium |
  | Optimize light activation | Delayed activation | Ensures timely warning | 50 ms response | Low |

#### 12. Final Safety Argument
The minimal-risk maneuver controller's safety case integrates ISO 26262, SOTIF, and ISO 8800 to ensure comprehensive safety coverage. ISO 26262 addresses E/E malfunctions, SOTIF covers intended functionality limitations, and ISO 8800 ensures AI robustness and data quality. Together, these standards provide a robust framework for developing a safe and reliable minimal-risk maneuver controller.