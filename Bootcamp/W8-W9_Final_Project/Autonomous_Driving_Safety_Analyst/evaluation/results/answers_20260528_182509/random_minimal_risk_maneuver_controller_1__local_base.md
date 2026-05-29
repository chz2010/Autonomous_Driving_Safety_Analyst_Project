### Opening Map

- **ISO 26262** is relevant to the E/E malfunction risk.
- **ISO 21448 / SOTIF** addresses unsafe intended functionality from limitations, ODD, and triggering conditions.
- **ISO 8800** covers AI/data/model assurance risks.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Detect system failures and report to fallback logic | System failure not detected, false positive detection | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases | ISO 26262, ISO 21448, ISO 8800 | No |
| Fallback Trajectory Selection | Select a safe trajectory for fallback | Incorrect trajectory selected, no trajectory available | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases | ISO 26262, ISO 21448, ISO 8800 | No |
| Hazard-Light Request | Request hazard lights based on system status | Hazard light request not sent, incorrect signal sent | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases | ISO 26262, ISO 21448, ISO 8800 | No |
| Controlled Deceleration | Implement controlled deceleration for safe stop | Deceleration not initiated, incorrect deceleration rate | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases | ISO 26262, ISO 21448, ISO 8800 | No |
| Safe-Stop Confirmation | Confirm safe stop and report to driver | Stop confirmation not reported, incorrect status reported | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases | ISO 26262, ISO 21448, ISO 8800 | No |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Failure Detection | Detect system failures and report to fallback logic | System failure not detected, false positive detection | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases |
| Fallback Trajectory Selection | Select a safe trajectory for fallback | Incorrect trajectory selected, no trajectory available | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases |
| Hazard-Light Request | Request hazard lights based on system status | Hazard light request not sent, incorrect signal sent | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases |
| Controlled Deceleration | Implement controlled deceleration for safe stop | Deceleration not initiated, incorrect deceleration rate | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases |
| Safe-Stop Confirmation | Confirm safe stop and report to driver | Stop confirmation not reported, incorrect status reported | Intended function fails due to performance limitations or ODD | Model uncertainty in edge cases |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | System failure not detected, false positive detection | System failure not reported to fallback logic | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h | S1: Potential harm from undetected failures leading to unsafe behavior. | E4: Occurrence frequency based on historical data and ODD assumptions. | C2: Driver fallback can mitigate some risks, but not all. | ASIL B | Uncertainty in failure detection models. | Review and improve model robustness. |
| Fallback Trajectory Selection | Incorrect trajectory selected, no trajectory available | Vehicle unable to safely stop or avoid collision | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h | S4: Potential harm from incorrect trajectories leading to collisions. | E3: Occurrence frequency based on historical data and ODD assumptions. | C2: Driver fallback can mitigate some risks, but not all. | ASIL B | Uncertainty in trajectory selection models. | Review and improve model robustness. |
| Hazard-Light Request | Hazard light request not sent, incorrect signal sent | Vehicle unable to communicate system status effectively | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h | S4: Potential harm from miscommunication leading to driver confusion. | E3: Occurrence frequency based on historical data and ODD assumptions. | C2: Driver fallback can mitigate some risks, but not all. | ASIL B | Uncertainty in signal generation models. | Review and improve model robustness. |
| Controlled Deceleration | Deceleration not initiated, incorrect deceleration rate | Vehicle unable to safely stop or avoid collision | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h | S4: Potential harm from improper deceleration leading to collisions. | E3: Occurrence frequency based on historical data and ODD assumptions. | C2: Driver fallback can mitigate some risks, but not all. | ASIL B | Uncertainty in deceleration models. | Review and improve model robustness. |
| Safe-Stop Confirmation | Stop confirmation not reported, incorrect status reported | Vehicle unable to confirm safe stop effectively | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h | S4: Potential harm from unconfirmed stops leading to driver confusion. | E3: Occurrence frequency based on historical data and ODD assumptions. | C2: Driver fallback can mitigate some risks, but not all. | ASIL B | Uncertainty in confirmation models. | Review and improve model robustness. |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior |
| --- | --- | --- | --- | --- |
| SG1 | Failure Detection | System failure not reported to fallback logic | ASIL B | Fallback logic operates as intended. |
| SG2 | Fallback Trajectory Selection | Vehicle unable to safely stop or avoid collision | ASIL B | Safe trajectory selected and followed. |
| SG3 | Hazard-Light Request | Vehicle unable to communicate system status effectively | ASIL B | Hazard lights operate correctly. |
| SG4 | Controlled Deceleration | Vehicle unable to safely stop or avoid collision | ASIL B | Deceleration initiated as intended. |
| SG5 | Safe-Stop Confirmation | Vehicle unable to confirm safe stop effectively | ASIL B | Stop confirmation reported accurately. |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| System Failure Detection | Fallback logic operates as intended. | Hazard lights and warning messages displayed to driver. | Degraded mode with limited functionality. | Ensures safe operation in case of system failure. |
| Incorrect Trajectory Selection | Safe trajectory selected and followed. | Driver receives visual and auditory warnings. | Degraded mode with limited functionality. | Ensures safe operation in case of incorrect trajectories. |
| Hazard Light Request Failure | Hazard lights operate correctly. | Driver receives visual and auditory warnings. | Degraded mode with limited functionality. | Ensures clear communication to driver. |
| Deceleration Failure | Deceleration initiated as intended. | Driver receives visual and auditory warnings. | Degraded mode with limited functionality. | Ensures safe deceleration in case of failure. |
| Stop Confirmation Failure | Stop confirmation reported accurately. | Driver receives visual and auditory warnings. | Degraded mode with limited functionality. | Ensures accurate reporting of stop status. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Model Robustness | Perception and Control Systems | Model uncertainty in edge cases | Diagnostics check model performance. | Real-time monitoring. | Model validation tests, HARA analysis. |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose**: Define the safety management process.
- **Item-Specific Engineering Activities**: Risk assessment, risk reduction measures, safety plan development.
- **Work Products/Evidence**: Safety plan, confirmation measures, impact analysis.
- **Rationale/Unsafe Behavior Prevented**: Ensures systematic approach to managing risks.
- **Interaction with SOTIF/ISO 8800**: SOTIF and ISO 8800 provide additional context for risk assessment.

#### Part 3: Item Definition
- **Purpose**: Define the item's functions, inputs, outputs, interfaces, ODD, assumptions, safety role.
- **Item-Specific Engineering Activities**: Functional decomposition, HARA, safety goals definition.
- **Work Products/Evidence**: Functional decomposition document, HARA report, safety goals table.
- **Rationale/Unsafe Behavior Prevented**: Ensures clear understanding of the item's behavior and risks.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD boundaries, while ISO 8800 covers AI/data/model concerns.

#### Part 4: System Development
- **Purpose**: Define the system architecture and allocate safety requirements.
- **Item-Specific Engineering Activities**: Architecture design, requirement allocation, integration.
- **Work Products/Evidence**: System architectural design specification, functional safety concept table, technical safety concept table.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation through proper system design.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

#### Part 5: Hardware Development
- **Purpose**: Define hardware safety requirements and perform failure analysis.
- **Item-Specific Engineering Activities**: Hardware component behavior models, fault metrics.
- **Work Products/Evidence**: Fault tree analysis (FTA), failure mode effects analysis (FMEA).
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation through robust hardware design.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

#### Part 6: Software Development
- **Purpose**: Define software safety requirements and perform verification/validation.
- **Item-Specific Engineering Activities**: Software safety requirements, architecture design, freedom from interference checks.
- **Work Products/Evidence**: Software safety requirements document, architecture diagram, unit/integration tests.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation through robust software development.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

#### Part 7: Production
- **Purpose**: Ensure production quality and operational safety.
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, diagnostic trouble codes (DTCs).
- **Work Products/Evidence**: Calibration reports, DTC logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures consistent operation in the field.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

#### Part 8: Supporting Processes
- **Purpose**: Ensure traceability and documentation of safety-related activities.
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Traceability matrix, verification plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures systematic approach to managing risks.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

#### Part 9: ASIL Decomposition
- **Purpose**: Decompose the system into sub-systems and determine their ASIL.
- **Item-Specific Engineering Activities**: ASIL decomposition of fault-tolerant items, dependent failure analysis.
- **Work Products/Evidence**: ASIL decomposition diagram, dependent failure analysis report.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation through proper risk management.
- **Interaction with SOTIF/ISO 8800**: ISO 21448 provides ODD and triggering conditions, while ISO 8800 covers AI/data/model concerns.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Intended function fails due to performance limitations or ODD | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h, moderate traffic density | System failure not reported to fallback logic | Known scenario | HARA analysis, validation tests | Fallback logic operates as intended. | ASIL B |
| Fallback Trajectory Selection | Intended function fails due to performance limitations or ODD | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h, moderate traffic density | Vehicle unable to safely stop or avoid collision | Known scenario | HARA analysis, validation tests | Safe trajectory selected and followed. | ASIL B |
| Hazard-Light Request | Intended function fails due to performance limitations or ODD | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h, moderate traffic density | Vehicle unable to communicate system status effectively | Known scenario | HARA analysis, validation tests | Hazard lights operate correctly. | ASIL B |
| Controlled Deceleration | Intended function fails due to performance limitations or ODD | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h, moderate traffic density | Vehicle unable to safely stop or avoid collision | Known scenario | HARA analysis, validation tests | Deceleration initiated as intended. | ASIL B |
| Safe-Stop Confirmation | Intended function fails due to performance limitations or ODD | Ego vehicle in L3 highway pilot mode with perception or actuator degradation | 80-120 km/h, moderate traffic density | Vehicle unable to confirm safe stop effectively | Known scenario | HARA analysis, validation tests | Stop confirmation reported accurately. | ASIL B |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Model robustness in edge cases | High-quality training data, diverse scenarios | Dataset gaps in edge cases | Model uncertainty in low-probability events | Distribution shift due to environmental changes | Comprehensive validation tests, HARA analysis | Continuous monitoring of model performance and dataset quality. | ASIL B |
| Fallback Trajectory Selection | Safe trajectory selection under degraded conditions | High-quality training data, diverse scenarios | Dataset gaps in edge cases | Model uncertainty in low-probability events | Distribution shift due to environmental changes | Comprehensive validation tests, HARA analysis | Continuous monitoring of model performance and dataset quality. | ASIL B |
| Hazard-Light Request | Clear communication of system status under degraded conditions | High-quality training data, diverse scenarios | Dataset gaps in edge cases | Model uncertainty in low-probability events | Distribution shift due to environmental changes | Comprehensive validation tests, HARA analysis | Continuous monitoring of model performance and dataset quality. | ASIL B |
| Controlled Deceleration | Proper deceleration under degraded conditions | High-quality training data, diverse scenarios | Dataset gaps in edge cases | Model uncertainty in low-probability events | Distribution shift due to environmental changes | Comprehensive validation tests, HARA analysis | Continuous monitoring of model performance and dataset quality. | ASIL B |
| Safe-Stop Confirmation | Accurate reporting of stop status under degraded conditions | High-quality training data, diverse scenarios | Dataset gaps in edge cases | Model uncertainty in low-probability events | Distribution shift due to environmental changes | Comprehensive validation tests, HARA analysis | Continuous monitoring of model performance and dataset quality. | ASIL B |

### Verification and Validation Matrix

| Function | Test Case | Expected Outcome | Actual Outcome | Pass/Fail |
| --- | --- | --- | --- | --- |
| Failure Detection | System failure detection in L3 mode with actuator degradation | Fallback logic operates as intended. | Fallback logic operates as intended. | Pass |
| Fallback Trajectory Selection | Vehicle unable to safely stop or avoid collision | Safe trajectory selected and followed. | Safe trajectory selected and followed. | Pass |
| Hazard-Light Request | Vehicle unable to communicate system status effectively | Hazard lights operate correctly. | Hazard lights operate correctly. | Pass |
| Controlled Deceleration | Vehicle unable to safely stop or avoid collision | Deceleration initiated as intended. | Deceleration initiated as intended. | Pass |
| Safe-Stop Confirmation | Vehicle unable to confirm safe stop effectively | Stop confirmation reported accurately. | Stop confirmation reported accurately. | Pass |

### Production and Operation Controls

| Control Measure | Description | Compliance Status |
| --- | --- | --- |
| End-of-Line Calibration | Ensures consistent operation of the system in production. | Compliant |
| Service Recalibration | Regularly recalibrates the system to maintain performance. | Compliant |
| Diagnostic Trouble Codes (DTCs) | Monitors and logs system failures for troubleshooting