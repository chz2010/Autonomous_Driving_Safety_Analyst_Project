### Safety Lifecycle and Item Safety Case for an Automated Parking Assist System

#### 1. Opening Map
- **ISO 26262**: Focuses on E/E malfunction risk, ensuring that the system's electrical and electronic components do not fail in a way that causes harm.
- **ISO 21448 (SOTIF)**: Addresses the safety of the intended functionality, focusing on limitations, ODD boundaries, and triggering conditions that could lead to unsafe behavior even if there is no E/E malfunction.
- **ISO 8800**: Concerns AI/data/model assurance, ensuring that AI components are robust, well-trained, and monitored for safety-related performance.

#### 2. Item Definition
- **Functions**: Slot detection, free-space estimation, obstacle detection, trajectory generation, low-speed control handoff.
- **Inputs**: Sensor data (camera, radar, ultrasonic), vehicle speed, environmental conditions.
- **Outputs**: Steering and braking control signals, driver alerts.
- **Interfaces**: Vehicle CAN bus, driver HMI.
- **ODD**: Parking lots, garages, marked and unmarked spaces, low speed.
- **Assumptions**: Reliable sensor data, driver supervision.
- **Safety Role**: Assist in parking maneuvers safely and efficiently.

#### 3. Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|----------------------|------------------------------|---------------------------|------------------------|-----------------------|
| Slot Detection | Slot position | Missed slot | False negatives in complex environments | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Free-Space Estimation | Free-space map | Incorrect estimation | Misjudged space due to occlusion | Model uncertainty | ISO 26262, SOTIF, ISO 8800 | Yes |
| Obstacle Detection | Obstacle position | Missed obstacle | False negatives in low visibility | Dataset bias | ISO 26262, SOTIF, ISO 8800 | Yes |
| Trajectory Generation | Path plan | Unsafe path | Overly aggressive path | Control algorithm robustness | ISO 26262, SOTIF | Yes |
| Low-Speed Control Handoff | Control signals | Delayed handoff | Overly cautious control | Control algorithm robustness | ISO 26262, SOTIF | Yes |

#### 4. HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|-----------------------|------------------|------------|-------------|-------------|---------|-------------|-------------|
| Slot Detection | Missed slot | Failed parking maneuver | Parking lot, 5 km/h | 5 km/h | Minor damage | Frequent in parking | Driver can intervene | QM | Sensor reliability | Improve sensor fusion |
| Free-Space Estimation | Incorrect estimation | Collision with obstacle | Parking lot, 5 km/h | 5 km/h | Minor damage | Frequent in parking | Driver can intervene | QM | Model accuracy | Enhance model validation |
| Obstacle Detection | Missed obstacle | Collision with obstacle | Parking lot, 5 km/h | 5 km/h | Minor damage | Frequent in parking | Driver can intervene | QM | Sensor reliability | Optimize detection logic |
| Trajectory Generation | Unsafe path | Collision | Parking lot, 5 km/h | 5 km/h | Minor damage | Frequent in parking | Driver can intervene | QM | Path planning accuracy | Optimize control logic |
| Low-Speed Control Handoff | Delayed handoff | Collision | Parking lot, 5 km/h | 5 km/h | Minor damage | Frequent in parking | Driver can intervene | QM | Control latency | Optimize control logic |

#### 5. Safety Goals, Functional Safety Concept, and Technical Safety Concept
- **Safety Goals Table**:
  | ID | Related Function | Hazardous Event Prevented | ASIL | Safe State/Degraded Behavior | Main Standard |
  |----|------------------|---------------------------|------|-----------------------------|---------------|
  | SG1 | Slot Detection | Failed parking maneuver | QM | Manual control | ISO 26262 |

- **Functional Safety Concept Table**:
  | Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
  |-----------------|-----------------------------|---------------------|--------------|-----------|
  | Missed slot | Alert driver | Visual/auditory alert | Manual control | Prevent failed maneuver |

- **Technical Safety Concept Table**:
  | Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
  |-----------|---------------------|-------------------------------|------------------------------|--------------|-----------------------|
  | Sensor fusion | Sensor module | Missed slot | Sensor health check | 100 ms | Sensor test results |

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
| Slot Detection | Complex environments | Poor lighting | Parking lot visibility | Missed slot | Known | Nighttime test cases | Sensor fusion | Acceptable with mitigation |

#### 8. ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|----------------|------------------|--------------------------|----------------------------|----------------------------|------------------------|-------------------------------|----------------------------|
| Slot Detection | Detect parking slots | Diverse parking data | Poor lighting scenarios | Model uncertainty | Weather conditions | Performance metrics | Continuous monitoring | Acceptable with monitoring |

#### 9. Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|-------------------------------|------------------|--------------------|
| Nighttime detection | Poor lighting | Detect parking slots | 95% detection rate | Test report | SG1 |

#### 10. Production and Operation
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|------------------|--------------|-----------|
| Field monitoring | Sensor failure | Health checks | No failures detected | Monitoring logs | Incident review | Ensures ongoing safety |

#### 11. Worst-Case Scenario
- **Scenario Assumptions Table**:
  | Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC/Available Sensing Time | Driver Fallback Assumption | Road Friction |
  |-----------|--------------|---------|----------|-----------|----------|----------------|-----------------|---------------------------|---------------------------|--------------|
  | 5 km/h | N/A | Clear | Night | None | Parking lot | Low | L2 | 2 seconds | Driver alert | Dry |

- **Accident-Chain Table**:
  | Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
  |------|-------------------------|-----------------------|------------------|------------------|-----------------|
  | 1 | Missed slot | No detection | No steering correction | Failed maneuver | Sensor logs |

- **Standard-View Table**:
  | ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
  |----------------------------|-----------------------|-----------------------------|---------------------|-----------------------|
  | Sensor failure | Poor lighting | Dataset gap | Sensor fusion | Test results |

- **Engineering-Decision Table**:
  | Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
  |-------------------------|--------------|-----------|--------------------------------|---------------|
  | Improve sensor fusion | Missed detection | Enhances detection | 95% detection rate | Acceptable |

#### 12. Final Safety Argument
The automated parking assist system's safety case integrates ISO 26262, SOTIF, and ISO 8800 standards to ensure comprehensive safety coverage. ISO 26262 addresses E/E malfunctions, SOTIF covers intended functionality limitations, and ISO 8800 ensures AI robustness and data quality. Together, these standards provide a robust framework for developing a safe and reliable automated parking assist system.