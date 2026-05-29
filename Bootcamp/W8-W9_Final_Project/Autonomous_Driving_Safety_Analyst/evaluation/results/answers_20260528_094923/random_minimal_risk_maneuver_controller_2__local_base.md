### Opening Map

- **ISO 26262** = E/E malfunction risk.
- **SOTIF** = unsafe intended functionality from limitations/ODD/triggering conditions.
- **ISO 8800** = AI/data/model assurance risk.

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Ego state, sensor data | Sensor failure, software bug | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Fallback Trajectory Selection | Trajectory plan | Software bug, communication failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Hazard-Light Request | Signal to driver | Software bug, hardware failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Controlled Deceleration | Vehicle deceleration command | Software bug, actuator failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Safe-Stop Confirmation | Stop confirmation signal | Software bug, communication failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Ego state, sensor data | Sensor failure, software bug | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Fallback Trajectory Selection | Trajectory plan | Software bug, communication failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Hazard-Light Request | Signal to driver | Software bug, hardware failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Controlled Deceleration | Vehicle deceleration command | Software bug, actuator failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |
| Safe-Stop Confirmation | Stop confirmation signal | Software bug, communication failure | Performance limitation, functional insufficiency | Data quality, model robustness | ISO 26262, SOTIF, ISO 8800 | Yes |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Sensor failure, software bug | Ego state misinterpretation leading to incorrect fallback trajectory selection | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | High ego speed, high object/road-user speed | Severity: Injury or fatality due to incorrect fallback trajectory. | Exposure: Occurs frequently on highways with moderate traffic. | Controllability: Driver can take over but has limited time. | ASIL D | Uncertainty in sensor data quality and software robustness. | Perform HARA for each function. |
| Fallback Trajectory Selection | Software bug, communication failure | Incorrect trajectory leading to collision or near-miss | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | High ego speed, high object/road-user speed | Severity: Injury or fatality due to incorrect trajectory. | Exposure: Occurs frequently on highways with moderate traffic. | Controllability: Driver can take over but has limited time. | ASIL D | Uncertainty in software robustness and communication reliability. | Perform HARA for each function. |
| Hazard-Light Request | Software bug, hardware failure | Incorrect signal leading to driver confusion or panic | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | High ego speed, high object/road-user speed | Severity: Injury or fatality due to driver confusion or panic. | Exposure: Occurs frequently on highways with moderate traffic. | Controllability: Driver can take over but has limited time. | ASIL D | Uncertainty in software robustness and hardware reliability. | Perform HARA for each function. |
| Controlled Deceleration | Software bug, actuator failure | Incorrect deceleration leading to collision or near-miss | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | High ego speed, high object/road-user speed | Severity: Injury or fatality due to incorrect deceleration. | Exposure: Occurs frequently on highways with moderate traffic. | Controllability: Driver can take over but has limited time. | ASIL D | Uncertainty in software robustness and actuator reliability. | Perform HARA for each function. |
| Safe-Stop Confirmation | Software bug, communication failure | Incorrect stop confirmation leading to driver confusion or panic | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | High ego speed, high object/road-user speed | Severity: Injury or fatality due to driver confusion or panic. | Exposure: Occurs frequently on highways with moderate traffic. | Controllability: Driver can take over but has limited time. | ASIL D | Uncertainty in software robustness and communication reliability. | Perform HARA for each function. |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG01 | Failure Detection | Ego state misinterpretation leading to incorrect fallback trajectory selection | ASIL D | Correct ego state interpretation and fallback trajectory selection. | ISO 26262, SOTIF, ISO 8800 |
| SG02 | Fallback Trajectory Selection | Incorrect trajectory leading to collision or near-miss | ASIL D | Correct trajectory selection for safe fallback. | ISO 26262, SOTIF, ISO 8800 |
| SG03 | Hazard-Light Request | Incorrect signal leading to driver confusion or panic | ASIL D | Correct hazard-light signaling for driver assistance. | ISO 26262, SOTIF, ISO 8800 |
| SG04 | Controlled Deceleration | Incorrect deceleration leading to collision or near-miss | ASIL D | Correct vehicle deceleration command for safe stopping. | ISO 26262, SOTIF, ISO 8800 |
| SG05 | Safe-Stop Confirmation | Incorrect stop confirmation leading to driver confusion or panic | ASIL D | Correct stop confirmation signal for driver confidence. | ISO 26262, SOTIF, ISO 8800 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor Failure | Ego state misinterpretation leading to incorrect fallback trajectory selection | HMI warning and driver takeover request. | Fallback mode with reduced functionality. | Ensures safe operation in degraded conditions. |
| Software Bug | Incorrect trajectory, deceleration, or stop confirmation | HMI warning and driver takeover request. | Fallback mode with reduced functionality. | Ensures safe operation in degraded conditions. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Ego State Detection | Sensor Fusion Module | Sensor failure, software bug | HMI warning and driver takeover request. | Real-time response within 10 ms. | Unit tests, integration tests, diagnostic logs. |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 2.1 | Define the safety lifecycle phases and sub-phases. | Define system development, validation, production, operation, service, decommissioning. | Safety plan, confirmation measures, release responsibilities. | Prevents unsafe behavior through structured safety management. | Interacts with ISO 8800 for AI lifecycle controls. |

#### Part 3: Item Definition
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 3.1 | Define the system and hardware configurations. | Define safety goals, functional safety concept, technical safety concept. | Safety goals table, functional safety concept table, technical safety concept table. | Prevents unsafe behavior through clear safety objectives and concepts. | Interacts with ISO 8800 for AI data management.

#### Part 4: System Development
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 4.1 | Define the system architecture and requirements allocation. | Allocate safety goals, functional safety concept, technical safety concept to hardware and software components. | System architectural design specification, safety requirements specification. | Prevents unsafe behavior through proper system architecture and requirements. | Interacts with ISO 8800 for AI model validation.

#### Part 5: Hardware Development
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 5.1 | Define the hardware safety requirements and FMEDA. | Define hardware safety requirements, perform FMEDA for fault detection and isolation. | Hardware safety requirements specification, FMEDA report. | Prevents unsafe behavior through robust hardware design. | Interacts with ISO 8800 for AI model validation.

#### Part 6: Software Development
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 6.1 | Define the software safety requirements and architecture. | Allocate safety goals, functional safety concept, technical safety concept to software components. | Software safety requirements specification, architectural design. | Prevents unsafe behavior through proper software architecture and requirements. | Interacts with ISO 8800 for AI model validation.

#### Part 7: Production
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 7.1 | Define the production process and end-of-line calibration. | Perform end-of-line calibration, service recalibration, DTCs. | End-of-line calibration report, service recalibration plan, diagnostic trouble codes (DTCs). | Prevents unsafe behavior through robust production processes. | Interacts with ISO 8800 for AI model validation.

#### Part 8: Supporting Processes
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 8.1 | Define the verification and validation planning, documentation, tool or component qualification. | Perform verification and validation activities, document results, qualify tools/components. | Verification plan, validation report, tool/component qualification report. | Prevents unsafe behavior through robust verification and validation processes. | Interacts with ISO 8800 for AI model validation.

#### Part 9: ASIL Decomposition
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| 9.1 | Decompose the ASIL for each function. | Perform ASIL decomposition, derive dependent failure analysis. | ASIL decomposition table, dependent failure analysis report. | Prevents unsafe behavior through proper ASIL classification and decomposition. | Interacts with ISO 8800 for AI model validation.

---

### SOTIF Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Sensor failure, software bug | High ego speed, high object/road-user speed | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | Ego state misinterpretation leading to incorrect fallback trajectory selection. | Known scenario status. | Unit tests, integration tests, diagnostic logs. | Fallback mode with reduced functionality. | Residual risk is managed through robust sensor fusion and software diagnostics. |
| Fallback Trajectory Selection | Software bug, communication failure | High ego speed, high object/road-user speed | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | Incorrect trajectory leading to collision or near-miss. | Known scenario status. | Unit tests, integration tests, diagnostic logs. | Fallback mode with reduced functionality. | Residual risk is managed through robust software diagnostics and communication redundancy. |
| Hazard-Light Request | Software bug, hardware failure | High ego speed, high object/road-user speed | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | Incorrect signal leading to driver confusion or panic. | Known scenario status. | Unit tests, integration tests, diagnostic logs. | Fallback mode with reduced functionality. | Residual risk is managed through robust software diagnostics and hardware redundancy. |
| Controlled Deceleration | Software bug, actuator failure | High ego speed, high object/road-user speed | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | Incorrect deceleration leading to collision or near-miss. | Known scenario status. | Unit tests, integration tests, diagnostic logs. | Fallback mode with reduced functionality. | Residual risk is managed through robust software diagnostics and actuator redundancy. |
| Safe-Stop Confirmation | Software bug, communication failure | High ego speed, high object/road-user speed | Highway, 80-130 km/h, moderate traffic density, driver fallback expectation | Incorrect stop confirmation leading to driver confusion or panic. | Known scenario status. | Unit tests, integration tests, diagnostic logs. | Fallback mode with reduced functionality. | Residual risk is managed through robust software diagnostics and communication redundancy. |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Data validation, model robustness | High-quality sensor data, labeled scenarios. | Dataset coverage for occlusion, low visibility, and sensor contamination. | Model robustness to handle degraded sensor performance. | OOD risk from distribution shift in sensor data. | Model performance meets safety-relevant KPIs. | Continuous monitoring of model performance and dataset quality. | Residual AI risk is managed through robust model validation and continuous monitoring.

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Sensor Data Injection | Degraded sensor performance (e.g., low visibility, occlusion) | Correct ego state interpretation and fallback trajectory selection. | Ego state misinterpretation rate < 1%. | Diagnostic logs, unit tests, integration tests. | SG01 |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor calibration drift | Perform end-of-line sensor calibration. | Calibration error < 1%. | Calibration report, diagnostic logs. | Continuous monitoring of sensor performance. | Ensures accurate sensor data for safe operation.

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object/ Road-User Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 120 | 40 | Rain