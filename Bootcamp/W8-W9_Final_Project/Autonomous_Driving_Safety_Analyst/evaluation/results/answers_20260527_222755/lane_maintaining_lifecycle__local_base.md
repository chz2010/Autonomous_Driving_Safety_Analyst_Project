### Opening Map

- **ISO 26262 = E/E malfunction risk**: The system can fail due to hardware faults.
- **SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**: The lane maintaining perception system may not perform as expected under certain operational situations.
- **ISO 8800 = AI/data/model assurance risk**: The AI model might exhibit weaknesses in data coverage, robustness, or uncertainty.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
| --- | --- | --- | --- | --- | --- |
| Perception | Object detection and tracking | Sensor failure, processing errors | Performance limitations under adverse conditions (e.g., rain, low light) | Data coverage gaps, model robustness issues | ISO 26262, SOTIF, ISO 8800 |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Perception | Object detection and tracking | Sensor failure, processing errors | Performance limitations under adverse conditions (e.g., rain, low light) | Data coverage gaps, model robustness issues |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Sensor failure, processing errors | Collision or near-miss | Adverse weather conditions (rain, low light) | Ego speed: 80-120 km/h; Object speed: 3-5 km/h | Severity: Risk of severe injury or death due to collision. | Exposure: High exposure in urban and highway environments with varying traffic density. | Controllability: Driver fallback is limited, but autonomous system can reduce speed and increase headway. | ASIL D | Uncertainty: Need for more detailed testing under various weather conditions. | Further HARA analysis required |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Perception | Collision due to object detection failure | ASIL D | Degraded behavior: Reduce speed and increase headway. | ISO 26262 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure, processing errors | Reduce speed and increase headway | HMI warning: "Reducing speed due to sensor issues." | Fallback mode: Manual control. | Ensures safe operation even with partial system failures. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Redundant sensors | Perception module | Sensor failure | Diagnostics: Check sensor health. | Real-time monitoring | Unit tests, integration tests |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### ISO 26262 Part 2
- **Purpose**: Define the project and establish a safety plan.
- **Item-Specific Engineering Activities**: Safety risk assessment, supplier interface management, DIA development.
- **Work Products/Evidence**: Safety plan, DIA.

#### ISO 26262 Part 3
- **Purpose**: Define the system and its functional safety requirements.
- **Item-Specific Engineering Activities**: HARA, S/E/C analysis, ASIL determination, safety goals definition.
- **Work Products/Evidence**: HARA report, S/E/C matrix, ASIL classification.

#### ISO 26262 Part 4
- **Purpose**: Define the system architecture and allocate functional safety requirements.
- **Item-Specific Engineering Activities**: System design, technical safety concept development, integration planning.
- **Work Products/Evidence**: Architecture diagram, technical safety concept document.

#### ISO 26262 Part 5
- **Purpose**: Develop hardware components and ensure their safety.
- **Item-Specific Engineering Activities**: Hardware design, FMEDA, diagnostic coverage analysis.
- **Work Products/Evidence**: Hardware design documentation, FMEDA report.

#### ISO 26262 Part 6
- **Purpose**: Develop software components and ensure their safety.
- **Item-Specific Engineering Activities**: Software development, freedom from interference checks, watchdog implementation.
- **Work Products/Evidence**: Software code, unit tests, integration tests.

#### ISO 26262 Part 7
- **Purpose**: Ensure safe production, operation, service, and decommissioning.
- **Item-Specific Engineering Activities**: End-of-line calibration, field monitoring, DTC management.
- **Work Products/Evidence**: Calibration records, field feedback reports.

#### ISO 26262 Part 8
- **Purpose**: Support safety-related processes.
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Change logs, test plans, documentation.

#### ISO 26262 Part 9
- **Purpose**: Decompose ASIL and perform dependent failure analysis.
- **Item-Specific Engineering Activities**: ASIL decomposition, common-cause/failure analysis.
- **Work Products/Evidence**: ASIL decomposition report, FMEA.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Depreciation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Performance limitations under adverse conditions (e.g., rain, low light) | Adverse weather conditions | Ego speed: 80-120 km/h; Object speed: 3-5 km/h | Reduced object detection accuracy leading to potential collisions. | Known scenario status | Scenario tests, timing analysis | Reduce speed and increase headway when perception confidence drops. | Mitigation reduces risk but does not eliminate it entirely due to varying weather conditions. |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Perception | Data-driven object detection and tracking | High-quality labeled data for various weather conditions. | Gaps in dataset coverage, especially for rare events (e.g., occlusion). | Model uncertainty under varying lighting and weather conditions. | Distribution shift due to changing environmental factors. | Robustness tests, model validation. | Continuous monitoring of performance degradation. | Mitigation reduces risk but does not fully eliminate it due to potential distribution shifts.

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Accept Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor failure test | Simulated sensor failure during object detection. | System reduces speed and increases headway. | Reduced speed and increased headway within 1 second of failure. | Diagnostic logs, unit tests. | ISO 26262-8:2018 |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor health check | Perform end-of-line calibration. | All sensors pass health checks. | Calibration records, diagnostic logs. | Continuous monitoring of sensor performance. | Ensures system reliability before deployment.

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 80-120 | 3-5 | Rainy conditions | Dim lighting | Partial occlusion by parked cars | Highway | Moderate | Autonomous |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation |
| --- | --- | --- | --- | --- |
| 1 | Sensor failure | Reduced object detection accuracy. | Reduce speed and increase headway. | Increased risk of collision due to delayed response. |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure leading to reduced object detection. | Performance limitations under adverse conditions (e.g., rain, low light). | Data coverage gaps and model robustness issues. | Reduce speed and increase headway when perception confidence drops. | Diagnostic logs, unit tests, integration tests.

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Accept Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement redundant sensors and diagnostic checks. | Reduced risk of collision due to sensor failure. | Diagnostic logs show no failures within 1 year. | No critical system failures reported in field tests. | Mitigation reduces but does not eliminate all risks.

### Final Safety Argument

The lane maintaining perception system is designed with multiple layers of safety measures, including hardware redundancy, software diagnostics, and robust AI models. The HARA analysis identifies potential hazards under adverse conditions, which are mitigated through specific design and operational controls. ISO 26262 ensures the system meets functional safety requirements, SOTIF addresses intended-function limitations and triggering conditions, and ISO 8800 focuses on AI/data/model assurance. Continuous monitoring and validation ensure that the system remains safe throughout its lifecycle.

### Summary

The lane maintaining perception system is developed according to ISO 26262, ISO 21448 (SOTIF), and ISO 8800 standards. The HARA analysis identifies potential hazards, which are mitigated through specific design and operational controls. Continuous monitoring and validation ensure the system remains safe under various conditions.