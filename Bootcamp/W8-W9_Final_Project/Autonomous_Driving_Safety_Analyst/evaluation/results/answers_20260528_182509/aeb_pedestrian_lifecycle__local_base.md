### Opening Map

- **ISO 26262**: E/E malfunction risk.
- **SOTIF**: Unsafe intended functionality from limitations/ODD/triggering conditions.
- **ISO 8800**: AI/data/model assurance risk.

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|----------------------|
| Perception | Object detection and classification | Sensor failure, processing errors | Late detection, false positives/negatives | Data coverage, label quality | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Estimation | Object trajectory prediction | Model drift, latency issues | Inaccurate predictions, incorrect timing | Data coverage, model robustness | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Tracking | Object state update and management | Sensor fusion errors, data integrity issues | Inconsistent tracking, missed updates | Data coverage, model robustness | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Confidence/uncertainty | Detection reliability and confidence scores | Overconfidence, underconfidence | Inaccurate uncertainty estimates, false alarms | Data coverage, model robustness | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Health/diagnostics | System health monitoring and diagnostics | Sensor failure, processing errors | Inadequate diagnostic coverage, missed faults | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Calibration/freshness | Model and data calibration | Data drift, model staleness | Inaccurate models, outdated data | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |
| Interface/actuation | AEB activation and control signals | Software errors, hardware issues | Inaccurate actuation, delayed response | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 | Yes |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
|----------|--------|---------------------|----------------------------|-------------------------|
| Perception | Object detection and classification | Sensor failure, processing errors | Late detection, false positives/negatives | Data coverage, label quality |
| Estimation | Object trajectory prediction | Model drift, latency issues | Inaccurate predictions, incorrect timing | Data coverage, model robustness |
| Tracking | Object state update and management | Sensor fusion errors, data integrity issues | Inconsistent tracking, missed updates | Data coverage, model robustness |
| Confidence/uncertainty | Detection reliability and confidence scores | Overconfidence, underconfidence | Inaccurate uncertainty estimates, false alarms | Data coverage, model robustness |
| Health/diagnostics | System health monitoring and diagnostics | Sensor failure, processing errors | Inadequate diagnostic coverage, missed faults | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| Calibration/freshness | Model and data calibration | Data drift, model staleness | Inaccurate models, outdated data | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| Interface/actuation | AEB activation and control signals | Software errors, hardware issues | Inaccurate actuation, delayed response | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|-------------------------|----------------|----------------------|-------------|-------------|-------------|---------|------------|------------|
| Perception | Sensor failure, processing errors | Collision due to undetected pedestrian | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: pedestrian injury or death | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot avoid the collision; fallback not available | ASIL D | Uncertain due to varying sensor reliability | Detailed HARA for each sensor |
| Estimation | Model drift, latency issues | Inaccurate trajectory prediction leading to late AEB activation | Highway road, 80-130 km/h, moderate traffic, short reaction time | High severity: collision or near-miss | Frequent occurrence on highways with high speeds and dense traffic | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying model performance | Detailed HARA for each estimation algorithm |
| Tracking | Sensor fusion errors, data integrity issues | Inconsistent tracking leading to missed updates | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: collision or near-miss | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying sensor fusion algorithms | Detailed HARA for each tracking algorithm |
| Confidence/uncertainty | Overconfidence, underconfidence | False alarms or missed detections leading to incorrect AEB activation | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: collision or near-miss | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying confidence models | Detailed HARA for each uncertainty model |
| Health/diagnostics | Sensor failure, processing errors | Inadequate diagnostic coverage leading to missed faults | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: collision or near-miss | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying diagnostic algorithms | Detailed HARA for each health/diagnostics system |
| Calibration/freshness | Data drift, model staleness | Inaccurate models leading to incorrect AEB activation | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: collision or near-miss | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying calibration algorithms | Detailed HARA for each model |
| Interface/actuation | Software errors, hardware issues | Inaccurate actuation leading to delayed response | Urban road, 30-50 km/h, moderate traffic, occlusion possible | High severity: collision or near-miss | Frequent occurrence in urban areas with pedestrians and occlusions | Driver cannot react in time; fallback not available | ASIL D | Uncertain due to varying actuation systems | Detailed HARA for each interface/actuation system |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
|----|-----------------|--------------------------|-------------------------|----------------------------|--------------|
| 1  | Perception       | Undetected pedestrian    | ASIL D                  | AEB activation             | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 2  | Estimation       | Inaccurate trajectory    | ASIL D                  | Correct AEB timing         | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 3  | Tracking         | Missed updates           | ASIL D                  | Correct AEB timing         | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 4  | Confidence/uncertainty | False alarms or missed detections | ASIL D                  | Correct AEB activation     | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 5  | Health/diagnostics | Missed faults            | ASIL D                  | Correct AEB activation     | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 6  | Calibration/freshness | Inaccurate models         | ASIL D                  | Correct AEB activation     | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |
| 7  | Interface/actuation | Delayed response         | ASIL D                  | Correct AEB activation     | ISO 26262-3:2018, Clause 7; ISO 21448-10.5; ISO 8800-9.5.2 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
|----------------|----------------------------|--------------------|---------------|----------|
| Sensor failure  | AEB activation             | HMI warning         | Fallback mode  | Ensures safety even with sensor issues |
| Model drift     | Corrective action          | HMI warning         | Degraded mode  | Ensures safety in case of model errors |
| Data integrity  | Consistent tracking        | HMI warning         | Degraded mode  | Ensures safety in case of data issues |
| Overconfidence | False alarms avoided       | HMI warning         | Degraded mode  | Ensures safety in case of overconfidence |
| Underconfidence| Missed detections avoided  | HMI warning         | Degraded mode  | Ensures safety in case of underconfidence |
| Data drift      | Model recalibration        | HMI warning         | Fallback mode  | Ensures safety in case of model staleness |
| Inaccurate actuation | Corrective action | HMI warning | Degraded mode | Ensures safety in case of actuation issues |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
|-----------|---------------------|-------------------------------|------------------------------|---------------|-----------------------|
| Sensor health monitoring | Health/diagnostics system | Sensor failure, processing errors | HMI warning, fallback mode | Real-time | Diagnostic logs, sensor data analysis |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose**: Define the safety lifecycle and manage the development process.
- **Item-Specific Engineering Activities**:
  - Define safety goals and functional safety concept.
  - Develop a detailed HARA for each function.
  - Derive ASIL levels based on S/E/C ratings.
  - Create a safety plan with confirmation measures, impact analysis, release responsibilities.
- **Work Products/Evidence**: Safety goals table, HARA screening results, ASIL levels, safety plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures that all functions are covered and risks are managed throughout the development process.

#### Part 3: Item Definition
- **Purpose**: Define the item's scope, inputs, outputs, interfaces, ODD, assumptions, and safety role.
- **Item-Specific Engineering Activities**:
  - Decompose the AEB system into perception, estimation, tracking, confidence/uncertainty, health/diagnostics, calibration/freshness, and interface/actuation functions.
  - Define the item's scope and inputs/outputs.
  - Identify ODD assumptions and safety role.
- **Work Products/Evidence**: Functional decomposition table, item definition document.
- **Rationale/Unsafe Behavior Prevented**: Ensures that all relevant functions are identified and their interactions are well-defined.

#### Part 4: System Development
- **Purpose**: Develop the system architecture, allocate functional safety requirements, integrate components, validate functionality, ensure vehicle-level behavior.
- **Item-Specific Engineering Activities**:
  - Design the perception, estimation, tracking, confidence/uncertainty, health/diagnostics, calibration/freshness, and interface/actuation systems.
  - Allocate functional safety requirements to each component.
  - Integrate and test the components for correct implementation of ASIL methods.
- **Work Products/Evidence**: System architecture diagram, integration test results, vehicle-level behavior verification reports.
- **Rationale/Unsafe Behavior Prevented**: Ensures that all components are correctly implemented and integrated to meet safety goals.

#### Part 5: Hardware Development
- **Purpose**: Develop the hardware with appropriate safety requirements, perform FMEDA, ensure diagnostic coverage, manage random hardware metrics.
- **Item-Specific Engineering Activities**:
  - Design the hardware for each component with fault-tolerant mechanisms.
  - Perform a Failure Modes and Effects Analysis (FMEA) to identify potential faults.
  - Ensure diagnostic coverage for all critical components.
- **Work Products/Evidence**: Hardware design documents, FMEA report, diagnostic test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures that hardware is designed with fault-tolerant mechanisms and diagnostics are in place.

#### Part 6: Software Development
- **Purpose**: Develop the software with appropriate safety requirements, ensure freedom from interference, manage model freshness, implement watchdogs and degraded-mode logic.
- **Item-Specific Engineering Activities**:
  - Develop the perception, estimation, tracking, confidence/uncertainty, health/diagnostics, calibration/freshness, and interface/actuation algorithms.
  - Ensure software is free from interference with other systems.
  - Implement model freshness checks and watchdogs for critical functions.
- **Work Products/Evidence**: Software development documentation, model validation reports, watchdog logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures that the software is robust and can handle unexpected conditions.

#### Part 7: Production
- **Purpose**: Ensure production processes meet safety requirements, perform end-of-line calibration, service recalibration, manage DTCs, field monitoring.
- **Item-Specific Engineering Activities**:
  - Perform final hardware and software calibrations.
  - Implement a robust production process with quality checks.
  - Manage diagnostic trouble codes (DTCs) for fault detection.
- **Work Products/Evidence**: Production calibration reports, DTC logs, field monitoring data.
- **Rationale/Unsafe Behavior Prevented**: Ensures that the final product meets all safety requirements.

#### Part 8: Supporting Processes
- **Purpose**: Ensure traceability of requirements, verification planning, documentation, tool or component qualification, manage safety case evidence.
- **Item-Specific Engineering Activities**:
  - Trace requirements through development phases.
  - Plan and execute verification activities.
  - Document all safety-related processes and decisions.
- **Work Products/Evidence**: Requirements traceability matrix, verification plan, documentation logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures that all safety-relevant aspects are documented and traceable.

#### Part 9: ASIL Decomposition
- **Purpose**: Ensure correct allocation of ASIL levels to each component.
- **Item-Specific Engineering Activities**:
  - Perform detailed HARA for each function.
  - Derive ASIL levels based on S/E/C ratings.
- **Work Products/Evidence**: Detailed HARA results, ASIL decomposition table.
- **Rationale/Unsafe Behavior Prevented**: Ensures that all components are correctly allocated to appropriate ASIL levels.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|------------------------|--------------|-------------------------------|---------------------------|-----------------------|-------------------------|
| Perception    | Late detection                   | Occlusion, low visibility conditions | Urban road, 30-50 km/h, moderate traffic | Collision or near-miss | Known but rare scenario | Sensor data analysis, occlusion testing | Fallback mode activation | Reduced risk through fallback |
| Estimation    | Inaccurate trajectory prediction | High-speed scenarios, dense traffic | Highway road, 80-130 km/h, moderate traffic | Late AEB activation or collision | Unknown but possible scenario | Trajectory simulation, high-speed testing | HMI warning and corrective action | Reduced risk through HMI intervention |
| Tracking      | Inconsistent tracking           | Sensor fusion errors, data integrity issues | Urban road, 30-50 km/h, moderate traffic | Missed updates or incorrect AEB timing | Known but rare scenario | Sensor fusion analysis, data integrity testing | Fallback mode activation | Reduced risk through fallback |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release