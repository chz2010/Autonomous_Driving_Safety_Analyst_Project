### Safety Lifecycle and Item Safety Case for a Camera-Based Cyclist Detection System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that the system does not fail in a way that could cause harm.
- **ISO 21448 (SOTIF)**: Addresses the safety of intended functionality, focusing on limitations, ODD boundaries, and triggering conditions that could lead to unsafe behavior even if the system functions as designed.
- **ISO 8800**: Concerns AI/data/model assurance, ensuring that AI components are robust, well-validated, and monitored for safety throughout their lifecycle.

#### 2. Item Definition
- **Functions**: Cyclist detection, posture classification, trajectory prediction, occlusion handling, AEB/planning interface output.
- **Inputs**: Camera data, environmental conditions, vehicle speed.
- **Outputs**: Detection signals, trajectory predictions, AEB activation commands.
- **ODD**: Urban intersections, bike lanes, night, rain, glare, partial occlusion.
- **Assumptions**: Reliable sensor data, timely processing, and effective AEB interface.
- **Safety Role**: Detect cyclists accurately to prevent collisions by timely activation of AEB.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Cyclist Detection | Detection signal | Missed detection | False negatives in occlusion | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Posture Classification | Posture data | Incorrect classification | Misclassification in poor lighting | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Trajectory Prediction | Predicted path | Incorrect prediction | Inaccurate prediction in rain | Model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Occlusion Handling | Detection signal | Missed detection | Failure in partial occlusion | Dataset gap | ISO 26262, SOTIF, ISO 8800 | Yes |
| AEB/Planning Interface Output | AEB command | Delayed activation | Over-reliance on system | Actuator failure | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|------------------|------------|-------------|-------------|---------|-------------|-------------|
| Cyclist Detection | Missed detection | Collision with cyclist | Urban, 30-50 km/h | 30-50 km/h | Severe injury | Frequent in urban | Difficult to control | ASIL B | Moderate | Improve sensor fusion |
| Posture Classification | Incorrect classification | Delayed AEB | Urban, 30-50 km/h | 30-50 km/h | Severe injury | Frequent in urban | Driver may intervene | ASIL B | Moderate | Enhance model validation |
| Trajectory Prediction | Incorrect prediction | Collision with cyclist | Urban, 30-50 km/h | 30-50 km/h | Severe injury | Frequent in urban | Driver may intervene | ASIL B | Moderate | Optimize prediction algorithms |
| Occlusion Handling | Missed detection | Collision with cyclist | Urban, 30-50 km/h | 30-50 km/h | Severe injury | Frequent in urban | Driver may intervene | ASIL B | Moderate | Improve occlusion handling |
| AEB/Planning Interface Output | Delayed activation | Collision with cyclist | Urban, 30-50 km/h | 30-50 km/h | Severe injury | Frequent in urban | Driver may intervene | ASIL B | Moderate | Optimize AEB response |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Cyclist Detection | Collision with cyclist | ASIL B | Alert driver | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed detection | Alert driver | Visual/audible alert | Manual braking | Reduces collision risk |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|--------------|-----------------------|
  | Sensor fusion | ECU | Missed detection | Alert driver | 100 ms | Sensor test logs |

#### 6. ISO 26262 Part 2-9 Lifecycle Table
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
|----------------|---------|--------------------------------------|------------------------|------------------------------------|---------------------------------|
| Part 2 | Functional safety management | Develop safety plan, DIA | Safety plan, DIA | Ensures structured safety activities | Supports SOTIF risk management |
| Part 3 | Concept phase | HARA, safety goals | HARA report, safety goals | Identifies hazards and safety goals | Aligns with SOTIF scenarios |
| Part 4 | System development | Technical safety concept | System architecture | Ensures system meets safety goals | Integrates SOTIF measures |
| Part 5 | Hardware development | FMEDA, PMHF | Hardware safety analysis | Ensures hardware reliability | Supports ISO 8800 robustness |
| Part 6 | Software development | Software safety requirements | Software architecture | Ensures software reliability | Supports ISO 8800 validation |
| Part 7 | Production and operation | Field monitoring | Field incident reports | Ensures operational safety | Supports ISO 8800 monitoring |
| Part 8 | Supporting processes | Configuration management | Configuration records | Ensures traceability | Supports ISO 8800 change control |
| Part 9 | Safety analyses | ASIL decomposition | ASIL analysis report | Ensures safety requirement allocation | Supports SOTIF scenario analysis |

#### 7. SOTIF Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known/Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|-------------------------|--------------|-------------------------------|---------------------------|------------------------|-------------------------|
| Cyclist Detection | Occlusion | Parked cars | Urban environment | Missed detection | Known | Occlusion test cases | Sensor fusion | Residual risk minimized |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|----------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Cyclist Detection | Detect cyclists | Diverse urban data | Limited occlusion data | High in occlusion | Moderate | Occlusion performance | Continuous monitoring | Residual risk managed |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Occlusion detection | Parked cars | Detect cyclist | 95% detection rate | Test report | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|------------------|--------------|-----------|
| Field monitoring | Sensor degradation | Regular checks | No critical failures | Maintenance logs | Incident review | Ensures ongoing safety |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Available Sensing Time | Driver Fallback Assumption |
  |-----------|--------------|---------|----------|-----------|----------|-----------------|-----------------|----------------------------|---------------------------|
  | 40 km/h | 15 km/h | Rain | Night | Parked cars | Urban | Moderate | L2 | 2 seconds | Driver alert |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Missed cyclist | No detection | No braking | Collision | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|----------------------------|---------------------|-----------------------|
  | Sensor failure | Occlusion | Dataset gap | Sensor fusion | Test reports |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Improve sensor fusion | Occlusion risk | Better detection | 95% detection rate | Managed |

#### 12. Final Safety Argument
The camera-based cyclist detection system's safety case integrates ISO 26262, SOTIF, and ISO 8800 to ensure comprehensive safety coverage. ISO 26262 addresses E/E malfunctions, SOTIF manages intended-function limitations, and ISO 8800 ensures AI robustness and data quality. Together, they provide a robust framework for developing a safe and reliable cyclist detection system.