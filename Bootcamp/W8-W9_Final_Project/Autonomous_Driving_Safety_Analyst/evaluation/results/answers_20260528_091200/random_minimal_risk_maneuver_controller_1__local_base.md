### Opening Map

**ISO 26262 Malfunction Risk:** The minimal-risk maneuver controller could fail due to hardware faults or software errors, leading to incorrect behavior.

**SOTIF Insufficiency Risk:** The intended functions of the controller might be insufficient under certain operational conditions, such as sensor degradation or unexpected environmental factors.

**ISO 8800 AI/Data/Model Risk:** The perception and decision-making components could have data gaps, model robustness issues, or distribution shift that affect safe operation.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Failure Detection | Detects faults in perception and actuator systems. | E/E fault, sensor failure. | Sensor data insufficiency, model performance limitations. | Data coverage gaps, label quality issues. |
| Fallback Trajectory Selection | Selects a safe trajectory if the primary maneuver fails. | Incorrect selection due to faulty inputs or degraded sensors. | Insufficient fallback logic under certain conditions. | Model uncertainty, distribution shift in fallback scenarios. |
| Hazard-Light Request | Requests hazard lights if a potential collision is detected. | Malfunctioning light control system. | Inadequate timing of hazard-light request. | Data gaps for hazard-light behavior. |
| Controlled Deceleration | Applies controlled deceleration to avoid or mitigate collisions. | Incorrect braking due to sensor or actuator failure. | Insufficient deceleration under certain conditions. | Model robustness issues, distribution shift in braking scenarios. |
| Safe-Stop Confirmation | Confirms that the vehicle has safely stopped after a maneuver. | False confirmation of stop state. | Inadequate stopping criteria validation. | Data gaps for stop-state verification. |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Failure Detection | Detects faults in perception and actuator systems. | E/E fault, sensor failure. | Sensor data insufficiency, model performance limitations. | Data coverage gaps, label quality issues. |
| Fallback Trajectory Selection | Selects a safe trajectory if the primary maneuver fails. | Incorrect selection due to faulty inputs or degraded sensors. | Insufficient fallback logic under certain conditions. | Model uncertainty, distribution shift in fallback scenarios. |
| Hazard-Light Request | Requests hazard lights if a potential collision is detected. | Malfunctioning light control system. | Inadequate timing of hazard-light request. | Data gaps for hazard-light behavior. |
| Controlled Deceleration | Applies controlled deceleration to avoid or mitigate collisions. | Incorrect braking due to sensor or actuator failure. | Insufficient deceleration under certain conditions. | Model robustness issues, distribution shift in braking scenarios. |
| Safe-Stop Confirmation | Confirms that the vehicle has safely stopped after a maneuver. | False confirmation of stop state. | Inadequate stopping criteria validation. | Data gaps for stop-state verification. |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Sensor failure, incorrect fault detection. | Vehicle collision due to undetected faults. | Highway, L3 fallback mode, moderate traffic density. | Severity: High (potential for severe injury or death). | Exposure: Moderate (occurs in L3 fallback scenarios). | Controllability: Low (driver fallback not available). | ASIL D |
| Fallback Trajectory Selection | Incorrect trajectory selection due to degraded sensors. | Vehicle collision due to wrong trajectory. | Highway, L3 fallback mode, moderate traffic density. | Severity: High (potential for severe injury or death). | Exposure: Moderate (occurs in L3 fallback scenarios). | Controllability: Low (driver fallback not available). | ASIL D |
| Hazard-Light Request | Malfunctioning light control system. | Vehicle collision due to unlit hazard lights. | Highway, L3 fallback mode, moderate traffic density. | Severity: High (potential for severe injury or death). | Exposure: Moderate (occurs in L3 fallback scenarios). | Controllability: Low (driver fallback not available). | ASIL D |
| Controlled Deceleration | Incorrect braking due to sensor failure. | Vehicle collision due to inadequate deceleration. | Highway, L3 fallback mode, moderate traffic density. | Severity: High (potential for severe injury or death). | Exposure: Moderate (occurs in L3 fallback scenarios). | Controllability: Low (driver fallback not available). | ASIL D |
| Safe-Stop Confirmation | False confirmation of stop state. | Vehicle collision due to premature resuming. | Highway, L3 fallback mode, moderate traffic density. | Severity: High (potential for severe injury or death). | Exposure: Moderate (occurs in L3 fallback scenarios). | Controllability: Low (driver fallback not available). | ASIL D |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

| ID | Related Function | Hazardous Event Prevented | ASIL/QM | Safe State/ Degraded Behavior |
| --- | --- | --- | --- | --- |
| 1 | Failure Detection | Undetected faults leading to collisions. | ASIL D | E/E fault detection and isolation. |
| 2 | Fallback Trajectory Selection | Incorrect trajectory selection causing collisions. | ASIL D | Safe fallback trajectories prioritized. |
| 3 | Hazard-Light Request | Unlit hazard lights during potential collisions. | ASIL D | Timely hazard-light requests. |
| 4 | Controlled Deceleration | Inadequate braking leading to collisions. | ASIL D | Controlled deceleration with fallback logic. |
| 5 | Safe-Stop Confirmation | False confirmation of stop state causing premature resuming. | ASIL D | Accurate stop-state verification. |

### ISO 26262 Part 2-9 Lifecycle Assessment

| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| **Part 2** | Functional Safety Management | Define safety goals, manage supplier interfaces. | Safety plan, confirmation measures. | Ensure all functions meet ASIL D requirements. | Interacts with ISO 21448 for ODD and SOTIF limitations. |
| **Part 3** | Item Definition | Define system architecture, allocate safety goals. | HARA, S/E/C, ASIL. | Identify critical functions and their risks. | Interacts with ISO 21448 for performance limitations and ISO 8800 for AI/data/model concerns. |
| **Part 4** | System Development | Design system architecture, allocate requirements. | Architecture, integration, validation. | Ensure safe operation under all conditions. | Interacts with ISO 21448 for ODD assumptions and ISO 8800 for data coverage. |
| **Part 5** | Hardware Development | Define hardware safety requirements, perform FMEDA. | Hardware safety requirements, diagnostic coverage. | Ensure robust hardware design. | Interacts with ISO 21448 for E/E system interactions. |
| **Part 6** | Software Development | Define software safety requirements, perform unit tests. | Software safety requirements, diagnostics. | Ensure safe and reliable software operation. | Interacts with ISO 21448 for software performance limitations. |
| **Part 7** | Production | Perform end-of-line calibration, service recalibration. | Calibration plans, DTCs. | Ensure consistent system behavior post-production. | Interacts with ISO 21448 for production testing and ISO 8800 for AI model validation. |
| **Part 8** | Supporting Processes | Manage configuration, trace requirements. | Verification planning, documentation. | Ensure all development activities align with safety goals. | Interacts with ISO 21448 for lifecycle management. |
| **Part 9** | ASIL Decomposition | Perform dependent failure analysis. | ASIL decomposition tables. | Ensure comprehensive coverage of potential failures. | Interacts with ISO 21448 for ODD and SOTIF limitations. |

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Sensor data insufficiency. | High traffic density, occlusion. | Highway, L3 fallback mode. | Undetected faults leading to collisions. | Known | HARA and sensor validation tests. | E/E redundancy, diagnostic checks. | Low residual risk due to multiple layers of safety mechanisms. |
| Fallback Trajectory Selection | Insufficient fallback logic. | Degraded sensors, high traffic density. | Highway, L3 fallback mode. | Incorrect trajectory selection causing collisions. | Known | HARA and sensor validation tests. | Safe fallback trajectories prioritized. | Low residual risk due to fallback logic design. |
| Hazard-Light Request | Inadequate timing of hazard-light request. | Sensor failure, occlusion. | Highway, L3 fallback mode. | Unlit hazard lights during potential collisions. | Known | HARA and sensor validation tests. | Timely hazard-light requests. | Low residual risk due to timely response design. |
| Controlled Deceleration | Insufficient deceleration under certain conditions. | Degraded sensors, occlusion. | Highway, L3 fallback mode. | Inadequate braking leading to collisions. | Known | HARA and sensor validation tests. | Controlled deceleration with fallback logic. | Low residual risk due to controlled deceleration design. |
| Safe-Stop Confirmation | False confirmation of stop state. | Sensor failure, occlusion. | Highway, L3 fallback mode. | Premature resuming causing collisions. | Known | HARA and sensor validation tests. | Accurate stop-state verification. | Low residual risk due to robust stop-state checks. |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Failure Detection | Data-driven fault detection. | High-resolution sensor data, labeled faults. | Limited coverage of rare fault scenarios. | Model uncertainty in detecting complex faults. | Distribution shift due to varying fault types. | Comprehensive dataset with diverse fault cases. | Regular model retraining and validation. | Low residual risk due to robust model design and monitoring. |
| Fallback Trajectory Selection | Safe fallback logic. | High-resolution sensor data, labeled trajectories. | Limited coverage of complex traffic scenarios. | Model uncertainty in selecting safe trajectories. | Distribution shift due to varying traffic conditions. | Comprehensive dataset with diverse trajectory cases. | Regular model retraining and validation. | Low residual risk due to robust model design and monitoring. |
| Hazard-Light Request | Timely hazard-light request. | High-resolution sensor data, labeled light requests. | Limited coverage of complex occlusion scenarios. | Model uncertainty in timing the request. | Distribution shift due to varying occlusion conditions. | Comprehensive dataset with diverse occlusion cases. | Regular model retraining and validation. | Low residual risk due to robust model design and monitoring. |
| Controlled Deceleration | Safe deceleration logic. | High-resolution sensor data, labeled braking scenarios. | Limited coverage of complex braking scenarios. | Model uncertainty in applying appropriate deceleration. | Distribution shift due to varying braking conditions. | Comprehensive dataset with diverse braking cases. | Regular model retraining and validation. | Low residual risk due to robust model design and monitoring. |
| Safe-Stop Confirmation | Accurate stop-state verification. | High-resolution sensor data, labeled stop states. | Limited coverage of complex stop scenarios. | Model uncertainty in verifying the state. | Distribution shift due to varying stop conditions. | Comprehensive dataset with diverse stop cases. | Regular model retraining and validation. | Low residual risk due to robust model design and monitoring. |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| E/E Fault Detection | Sensor failure during maneuver. | Correct fault detection and isolation. | False positive rate < 0.1%. | Diagnostic logs, test reports. | ASIL D requirement for E/E safety. |
| Fallback Trajectory Selection | Degraded sensors in high traffic density. | Safe fallback trajectory selection. | Accuracy > 95% under degraded conditions. | HARA and sensor validation tests. | ASIL D requirement for safe operation. |
| Hazard-Light Request | Occlusion during potential collision. | Timely hazard-light request. | Response time < 100 ms. | Sensor logs, test reports. | ASIL D requirement for safety-critical behavior. |
| Controlled Deceleration | Degraded sensors in occluded environment. | Appropriate deceleration applied. | Deceleration rate > 5 m/s² under degraded conditions. | HARA and sensor validation tests. | ASIL D requirement for safe operation. |
| Safe-Stop Confirmation | Sensor failure during stop state verification. | Correct confirmation of stop state. | False positive rate < 0.1%. | Diagnostic logs, test reports. | ASIL D requirement for E/E safety. |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor calibration drift. | Perform end-of-line sensor calibration. | Calibration accuracy within ±1%. | Calibration logs, test reports. | Regular recalibration checks. | Ensure consistent system performance post-production. |
| Sensor Health Checks | Degraded sensors. | Periodic sensor health checks. | Sensor functionality > 95% of nominal value. | Sensor logs, test reports. | Real-time monitoring and alerts. | Prevent failures due to degraded sensors. |
| Software/Model Version Traceability | Inconsistent software versions. | Maintain version control database. | All vehicles have latest approved version. | Version control logs, deployment records. | Regular audits and updates. | Ensure consistent system behavior across fleet. |
| DTCs (Diagnostic Trouble Codes) | Unresolved faults. | Monitor and address DTCs. | No unresolved critical DTCs. | Diagnostic logs, service reports. | Real-time monitoring and alerts. | Prevent undetected faults leading to collisions. |

### Worst-Case Scenario

**Scenario:** A vehicle in L3 fallback mode encounters a complex traffic scenario with occluded sensors and degraded actuator systems.

**Analysis:**
1. **Failure Detection**: The system detects the fault but fails to isolate it correctly.
2. **Fallback Trajectory Selection**: Incorrect trajectory is selected due to sensor degradation.
3. **Hazard-Light Request**: Hazard lights are not requested in time due to occlusion.
4. **Controlled Deceleration**: Inadequate deceleration applied, leading to a collision.

**Mitigation:**
- E/E redundancy and diagnostic checks ensure correct fault isolation.
- Safe fallback trajectories prioritized under degraded conditions.
- Timely hazard-light requests implemented with robust timing logic.
- Controlled deceleration designed with fallback logic for complex scenarios.

### Final Safety Argument

The minimal-risk maneuver controller has been rigorously analyzed across ISO 26262, ISO 21448 (SOTIF), and ISO 8800 to ensure safe operation under all conditions. The system meets ASIL D requirements through comprehensive safety mechanisms, robust fallback logic, and continuous monitoring of AI components. The final risk assessment indicates low residual risks due to multiple layers of safety design and regular validation processes.

This structured approach ensures that the controller operates safely in L3 fallback mode, minimizing the potential for collisions and ensuring driver and passenger safety.