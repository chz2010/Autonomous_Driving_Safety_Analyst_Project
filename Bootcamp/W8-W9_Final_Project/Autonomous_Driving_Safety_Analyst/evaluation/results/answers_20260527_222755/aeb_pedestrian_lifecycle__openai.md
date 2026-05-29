### Safety Lifecycle for Developing an AEB Pedestrian System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that the system's electrical and electronic components do not fail in a way that causes harm.
- **ISO 21448 (SOTIF)**: Addresses the safety of the intended functionality, focusing on limitations, ODD boundaries, and triggering conditions that could lead to unsafe behavior even if there is no E/E malfunction.
- **ISO 8800**: Concerns AI/data/model assurance, ensuring that AI components are robust, well-trained, and monitored for safety-related performance.

#### 2. Item Definition
- **Functions**: Detect pedestrians, assess collision risk, and apply brakes.
- **Inputs**: Sensor data (camera, radar, LiDAR), vehicle speed, environmental conditions.
- **Outputs**: Brake actuation signal.
- **Interfaces**: Vehicle CAN bus, driver HMI.
- **ODD**: Urban environments, daylight and nighttime, clear and adverse weather.
- **Assumptions**: Reliable sensor data, driver supervision.
- **Safety Role**: Prevent pedestrian collisions.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Pedestrian Detection | Detection signal | Missed detection | False negatives in occlusion | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Collision Risk Assessment | Risk level | Incorrect risk assessment | Misjudged pedestrian speed | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Brake Actuation | Brake command | Delayed actuation | Overly cautious braking | Control algorithm robustness | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|-----------------------|------------------|------------|-------------|-------------|---------|-------------|-------------|
| Pedestrian Detection | Missed detection | Collision with pedestrian | Urban, 30 km/h | 30 km/h | Severe injury | Frequent in urban | Difficult to control | ASIL B | Sensor reliability | Improve sensor fusion |
| Collision Risk Assessment | Incorrect risk | Late braking | Urban, 30 km/h | 30 km/h | Severe injury | Frequent in urban | Driver can intervene | ASIL A | Model accuracy | Enhance model validation |
| Brake Actuation | Delayed actuation | Collision | Urban, 30 km/h | 30 km/h | Severe injury | Frequent in urban | Driver can intervene | ASIL A | Actuation latency | Optimize control logic |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Pedestrian Detection | Collision with pedestrian | ASIL B | Immediate braking | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed detection | Automatic braking | Alert driver | Reduced speed | Prevent collision |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|--------------|-----------------------|
  | Sensor fusion | Sensor module | Missed detection | Sensor health check | 100 ms | Sensor test results |

#### 6. ISO 26262 Part 2-9 Lifecycle Table
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
|----------------|---------|--------------------------------------|------------------------|------------------------------------|---------------------------------|
| Part 2 | Functional safety management | Safety plan, DIA | Safety plan document | Ensures structured safety activities | Aligns with SOTIF risk management |
| Part 3 | Concept phase | HARA, safety goals | HARA report, safety goals | Identifies and mitigates hazards | Considers SOTIF scenarios |
| Part 4 | System development | Technical safety concept | System architecture | Ensures system meets safety goals | Considers AI model integration |
| Part 5 | Hardware development | FMEDA, PMHF | Hardware safety analysis | Ensures hardware reliability | Supports SOTIF hardware scenarios |
| Part 6 | Software development | Software safety requirements | Software architecture | Ensures software reliability | Considers AI model robustness |
| Part 7 | Production and operation | Field monitoring | Monitoring plan | Detects field issues early | Supports SOTIF operational scenarios |
| Part 8 | Supporting processes | Configuration management | Configuration records | Ensures traceability | Supports AI model updates |
| Part 9 | Safety analyses | ASIL decomposition | Safety analysis report | Identifies independent safety elements | Considers SOTIF and AI dependencies |

#### 7. SOTIF Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known/Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|-------------------------|--------------|-------------------------------|---------------------------|------------------------|-------------------------|
| Pedestrian Detection | Occlusion | Parked cars | Urban visibility | Missed detection | Known | Occlusion test cases | Sensor fusion | Acceptable with mitigation |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|----------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Pedestrian Detection | Detect VRUs | Diverse urban data | Occlusion scenarios | Model uncertainty | Nighttime conditions | Performance metrics | Continuous monitoring | Acceptable with monitoring |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Occlusion detection | Parked cars | Detect pedestrian | 95% detection rate | Test report | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|------------------|--------------|-----------|
| Field monitoring | Sensor failure | Health checks | No failures detected | Monitoring logs | Incident review | Ensures ongoing safety |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Available Sensing Time | Driver Fallback Assumption | Road Friction |
  |-----------|--------------|---------|----------|-----------|----------|----------------|-----------------|---------------------------|---------------------------|--------------|
  | 30 km/h | 5 km/h | Clear | Daylight | Parked cars | Urban | Moderate | L2 | 2 seconds | Driver alert | Dry |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Missed pedestrian | No detection | No braking | Collision | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|-----------------------------|---------------------|-----------------------|
  | Sensor failure | Occlusion | Dataset gap | Sensor fusion | Test results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Improve sensor fusion | Missed detection | Enhances detection | 95% detection rate | Acceptable |

#### 12. Final Safety Argument
The AEB pedestrian system's safety case integrates ISO 26262, SOTIF, and ISO 8800 standards to ensure comprehensive safety coverage. ISO 26262 addresses E/E malfunctions, SOTIF covers intended functionality limitations, and ISO 8800 ensures AI robustness and data quality. Together, these standards provide a robust framework for developing a safe and reliable AEB pedestrian system.