### Opening Map

**ISO 26262 = E/E malfunction risk; SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions; ISO 8800 = AI/data/model assurance risk**

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Perception | Lane boundary detection, vehicle position estimation | Sensor failure, processing errors | ODD limitations, triggering conditions not met | Data coverage, model robustness, uncertainty analysis | ISO 26262, ISO 21448 (SOTIF), ISO 8800 |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Perception | Lane boundary detection, vehicle position estimation | Sensor failure, processing errors | ODD limitations, triggering conditions not met | Data coverage, model robustness, uncertainty analysis |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Sensor failure, processing errors | Vehicle departure from lane | Urban road, 30-50 km/h ego speed, moderate traffic density | Ego and object speeds up to 60 km/h; visibility reduced by rain/fog | Severity: Risk of collision or injury due to vehicle leaving the lane. | Exposure: Occurs in urban areas with moderate traffic. | Controllability: Driver can take over control if system fails. | ASIL C | Uncertainty: Varies based on weather and traffic conditions. | Review sensor reliability and processing robustness. |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table

| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior |
| --- | --- | --- | --- | --- |
| SG1 | Perception | Vehicle departure from lane | ASIL C | Lane keeping within defined boundaries. |

#### Functional Safety Concept Table

| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure, processing errors | Emergency braking and HMI warning | Warning to driver to take over control | Fallback to manual driving mode | Ensures safe operation even if perception system fails. |

#### Technical Safety Concept Table

| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Redundant sensors | Perception module | Sensor failure detection and correction | Failsafe mode with HMI warning | Real-time | Sensor health checks, diagnostic logs |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### ISO 26262 Part 2: Functional Safety Management
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Define safety goals and requirements | Define safety goals, allocate ASILs | Safety goals document, ASIL allocation matrix | Ensures all functions are classified according to their risk. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 3: Item Definition
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Define system architecture and interfaces | Define system architecture, allocate functions to components | System architecture diagram, interface specification | Ensures proper allocation of safety-critical functions. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 4: System Development
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Develop and integrate system components | Develop perception algorithms, integrate with control logic | Code repository, integration test results | Ensures correct implementation of safety-critical functions. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 5: Hardware Development
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Develop and test hardware components | Develop sensor hardware, perform EMI testing | Hardware design documentation, test reports | Ensures robustness of hardware components. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 6: Software Development
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Develop and test software components | Develop perception algorithms, perform unit tests | Code repository, test results | Ensures correct implementation of safety-critical functions. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 7: Production
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Ensure production quality and safety | Perform final calibration, conduct field testing | Calibration logs, test reports | Ensures safe operation in real-world conditions. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 8: Supporting Processes
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Ensure traceability and documentation | Maintain requirements traceability, document safety activities | Requirements traceability matrix, project documentation | Ensures all safety-related activities are documented. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

#### ISO 26262 Part 9: ASIL Decomposition
| Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- |
| Decompose system into safety-critical functions | Define and allocate ASILs to sub-functions | ASIL decomposition matrix, functional safety requirements | Ensures all sub-functions are classified according to their risk. | Interacts with ISO 21448 for ODD limitations and SOTIF evaluations. |

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Lane boundary detection within defined boundaries | Rain, low light, occlusion | Urban roads with moderate traffic density | Vehicle departure from lane | Known | Sensor performance tests, weather condition simulations | Fallback to manual driving mode | Risk reduced but not eliminated. |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Data-driven lane boundary detection | High-quality sensor data, accurate map information | Limited dataset coverage for occluded scenarios | Model uncertainty in low-light conditions | Distribution shift due to weather changes | Comprehensive validation and testing before release | Continuous monitoring of model performance | Risk reduced but requires ongoing attention. |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor failure test | Simulated sensor failure during lane detection | System failsafe mode with HMI warning | No vehicle departure from lane | Diagnostic logs, test reports | ASIL C requirement |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-line calibration | Sensor accuracy | Perform final sensor health checks | No errors detected | Calibration logs, test reports | Incident review | Ensures accurate perception in real-world conditions. |

---

### Worst-Case Scenario

#### Scenario Assumptions Table

| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time | Driver Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 50 km/h | 30 km/h | Rainy | Low visibility | Partial occlusion by parked cars | Urban road | Moderate traffic density | L2+ | 1 second | Driver takeover |

#### Accident-Chain Table

| Step | Degraded/ Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation |
| --- | --- | --- | --- | --- |
| 1 | Sensor failure | Lane boundary not detected accurately | Emergency braking initiated | Increased stopping distance, potential collision. |
| 2 | HMI warning ignored | Driver does not take over control in time | Collision occurs due to delayed response | High risk of injury or fatality. |

#### Standard-View Table

| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/ Data Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure detection and correction | ODD limitations, triggering conditions not met | Model uncertainty in low-light conditions | Fallback to manual driving mode | Diagnostic logs, test reports |

#### Engineering-Decision Table

| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement redundant sensors and HMI warnings | Yes | Ensures safe operation even if perception system fails. | No sensor failures detected during testing. | Ongoing monitoring required to ensure robustness. |

---

### Final Safety Argument

The safety case for the lane maintaining perception system is built on a combination of ISO 26262, SOTIF, and ISO 8800 principles:

- **ISO 26262** ensures that all functions are classified according to their risk and implemented with appropriate diagnostics and fallback mechanisms.
- **SOTIF** addresses the limitations in intended functionality due to ODD boundaries and triggering conditions, ensuring safe operation within defined limits.
- **ISO 8800** focuses on AI-specific safety concerns such as data coverage, model robustness, uncertainty analysis, and monitoring.

By integrating these standards, the system is designed to handle various failure modes and operational scenarios, reducing the risk of hazardous events. Ongoing monitoring and validation are critical to maintaining safety over the lifecycle of the vehicle.