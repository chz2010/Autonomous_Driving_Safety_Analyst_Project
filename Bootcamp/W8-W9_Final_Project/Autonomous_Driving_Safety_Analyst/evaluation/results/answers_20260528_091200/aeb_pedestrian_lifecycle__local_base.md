### Opening Map

- **ISO 26262**: Focus on E/E malfunction risk.
- **SOTIF**: Address intended-function insufficiencies and ODD limitations.
- **ISO 8800**: Ensure AI/data/model safety, robustness, and uncertainty.

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|----------------------|
| AEB      | Braking command, warning signal | ECU failure, sensor malfunction | Late detection, insufficient deceleration | Data coverage, model robustness | ISO 26262, ISO 21448, ISO 8800 | Yes |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|
| Perception | Object detection, classification | Sensor failure, ECU processing error | Late detection, incorrect classification | Data coverage, label quality | ISO 26262, ISO 8800 |
| Estimation | Distance, speed estimation | Sensor noise, ECU processing error | Inaccurate distance/speed estimation | Model robustness, uncertainty | ISO 26262, ISO 8800 |
| Tracking | Object trajectory prediction | Sensor failure, ECU processing error | Unreliable trajectory prediction | Data coverage, model robustness | ISO 26262, ISO 8800 |
| Confidence/uncertainty | Detection confidence, uncertainty estimation | Sensor noise, ECU processing error | Overconfidence, underconfidence | Model robustness, uncertainty | ISO 26262, ISO 8800 |
| Health/diagnostics | System health monitoring | Sensor failure, ECU failure | Inadequate diagnostics | ISO 26262 | Yes |
| Calibration/freshness | Sensor calibration, model retraining | Sensor drift, outdated models | Data freshness, model retraining | ISO 8800 | Yes |
| Interface/actuation | Braking command, warning signal | ECU failure, actuator malfunction | Inaccurate braking, false warnings | ISO 26262 | Yes |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|-----------------|----------------------|-------------|-------------|-------------|---------|------------|------------|
| Perception | Sensor failure, ECU processing error | Late detection, incorrect classification | Urban road, 30 km/h, pedestrian crossing | Pedestrian collision risk | High exposure in urban areas with pedestrians | Driver fallback possible but limited reaction time | ASIL B | Low uncertainty | Review sensor and ECU reliability |
| Estimation | Sensor noise, ECU processing error | Inaccurate distance/speed estimation | Highway road, 80 km/h, moderate traffic | Reduced stopping distance, increased risk of collision | High exposure on highways with high speeds | Driver fallback limited due to short reaction time | ASIL C | Moderate uncertainty | Validate distance and speed estimation models |
| Tracking | Sensor failure, ECU processing error | Unreliable trajectory prediction | Urban road, 30 km/h, pedestrian crossing | Pedestrian collision risk | High exposure in urban areas with pedestrians | Driver fallback possible but limited reaction time | ASIL B | Low uncertainty | Improve tracking algorithms and sensor fusion |
| Confidence/uncertainty | Sensor noise, ECU processing error | Overconfidence, underconfidence | Urban road, 30 km/h, pedestrian crossing | Increased risk of false positives/negatives | High exposure in urban areas with pedestrians | Driver fallback possible but limited reaction time | ASIL B | Low uncertainty | Calibrate confidence thresholds |
| Health/diagnostics | Sensor failure, ECU failure | Inadequate diagnostics | Urban road, 30 km/h, pedestrian crossing | Delayed detection of system failures | High exposure due to critical safety functions | Driver fallback limited due to short reaction time | ASIL B | Low uncertainty | Implement robust diagnostic checks |
| Calibration/freshness | Sensor drift, outdated models | Data freshness, model retraining | Urban road, 30 km/h, pedestrian crossing | Reduced AEB effectiveness over time | High exposure in urban areas with pedestrians | Driver fallback limited due to short reaction time | ASIL B | Moderate uncertainty | Ensure regular data updates and retraining |
| Interface/actuation | ECU failure, actuator malfunction | Inaccurate braking, false warnings | Urban road, 30 km/h, pedestrian crossing | Pedestrian collision risk or false alarms | High exposure in urban areas with pedestrians | Driver fallback possible but limited reaction time | ASIL B | Low uncertainty | Validate actuator and ECU reliability |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
|----|-----------------|--------------------------|-------------------------|----------------------------|--------------|
| 1  | Perception       | Late detection           | ASIL B                  | Early warning              | ISO 26262    |
| 2  | Estimation       | Inaccurate distance      | ASIL C                  | Reduced stopping distance  | ISO 26262    |
| 3  | Tracking         | Unreliable trajectory   | ASIL B                  | Predicted path errors     | ISO 26262    |
| 4  | Confidence       | Overconfidence/underconf | ASIL B                  | Balanced confidence        | ISO 26262    |
| 5  | Health/Diagnostics | Inadequate diagnostics  | ASIL B                  | Timely system health checks| ISO 26262    |
| 6  | Calibration     | Data freshness           | ASIL B                  | Regular data updates      | ISO 8800     |
| 7  | Interface/Actuation | Inaccurate braking       | ASIL B                  | Accurate actuator response| ISO 26262    |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
|-----------------|----------------------------|--------------------|---------------|-----------|
| Sensor failure  | Braking command disabled    | Warning signal     | Manual braking | Ensure safety-critical functions are prioritized |
| ECU processing error | Reduced AEB functionality | Warning signal   | Driver fallback | Provide clear feedback to driver for safe operation |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
|-----------|--------------------|-------------------------------|------------------------------|---------------|-----------------------|
| Sensor health monitoring | ECU | Sensor failure | Diagnostics and alerts | Real-time | Log files, diagnostic tests |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Define safety goals, functional decomposition, HARA.
- **Work Products/Evidence**: Safety plan, DIA/supplier interface, confirmation measures.
- **Rationale/Unsafe Behavior Prevented**: Ensure all functions are covered and risks are mitigated.

#### Part 3: Item Definition
- **Item-Specific Engineering Activities**: Define safety goals, functional decomposition, HARA.
- **Work Products/Evidence**: Safety plan, DIA/supplier interface, confirmation measures.
- **Rationale/Unsafe Behavior Prevented**: Ensure all functions are covered and risks are mitigated.

#### Part 4: System Development
- **Item-Specific Engineering Activities**: Architecture design, requirements allocation, integration, validation.
- **Work Products/Evidence**: Software architecture, system-level tests, integration tests.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system is robust and reliable.

#### Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA, diagnostic coverage.
- **Work Products/Evidence**: Hardware design, diagnostic tests, failure modes analysis.
- **Rationale/Unsafe Behavior Prevented**: Ensure hardware reliability and diagnostics are effective.

#### Part 6: Software Development
- **Item-Specific Engineering Activities**: Software safety requirements, architecture, freedom from interference.
- **Work Products/Evidence**: Code reviews, unit tests, integration tests.
- **Rationale/Unsafe Behavior Prevented**: Ensure software is free from faults and reliable.

#### Part 7: Production, Operation, Service, Decommissioning
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, DTCs.
- **Work Products/Evidence**: Calibration logs, service records, diagnostic trouble codes (DTCs).
- **Rationale/Unsafe Behavior Prevented**: Ensure the system operates safely and reliably in production.

#### Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability.
- **Work Products/Evidence**: Traceability matrices, configuration logs.
- **Rationale/Unsafe Behavior Prevented**: Ensure all changes are managed and tracked.

#### Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: Failure modes analysis, risk matrices.
- **Rationale/Unsafe Behavior Prevented**: Ensure the system is robust against dependent failures.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|------------------------|--------------|-------------------------------|---------------------------|-----------------------|-------------------------|
| Perception    | Late detection                  | Occlusion, sensor failure | Urban areas with pedestrians | Pedestrian collision risk | Known | Scenario catalogue entry, confidence/uncertainty calibration | Early warning system | Low residual risk due to fallback |
| Estimation    | Inaccurate distance/speed       | Sensor noise, ECU processing error | Highway road, 80 km/h | Reduced stopping distance | Unknown | Field testing under various conditions | Driver fallback | Moderate residual risk |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|-------------------------------|-----------------------------|------------------------|------------------------------------|---------------------------|
| Perception          | Data-driven detection | High-resolution LiDAR, camera data | Occlusion, label quality issues | Overconfidence in clear conditions | Unknown deployment limits | Regular validation under various scenarios | Continuous monitoring of model performance | Low residual risk due to fallback |
| Estimation          | Distance/speed estimation | Sensor data, map data | Inconsistent speed labels | Underestimating vehicle speed | Rare weather conditions | Field testing and real-world feedback | Real-time monitoring of system health | Moderate residual risk |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|-----------------------|---------------------------------|------------------|--------------------|
| Perception | Occlusion                    | Early warning signal  | Confidence threshold met         | Log files        | ASIL B             |
| Estimation | Sensor noise                 | Accurate distance     | Distance estimation error < 10%  | Unit tests       | ASIL C             |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|------------------|--------------|-----------|
| End-of-Line Calibration | Sensor accuracy | Calibrate sensors | Pass/fail based on sensor readings | Calibration logs | Continuous monitoring | Ensure accurate perception |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
|------------------|--------------------|--------|---------|----------|-----------|---------------|--------------|-----------------------------------|-----------------------------|
| 30               | 5                   | Clear  | Daylight | None     | Urban     | Moderate      | L2            | 1.5                               | Limited reaction time       |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
|------|------------------------|-----------------------|------------------|------------------|----------------|
| 1    | Occlusion               | Late detection        | No braking        | Pedestrian collision risk | Scenario catalogue entry, confidence calibration |
| 2    | Inaccurate distance     | Reduced stopping distance | Delayed braking | Increased risk of collision | Field testing under various conditions |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
|---------------------------|---------------------|----------------------------|--------------------|-----------------------|
| Sensor failure            | Late detection      | Data coverage issues       | Early warning system | Log files, diagnostic tests |
| ECU processing error      | Inaccurate distance | Model robustness           | Driver fallback     | Field testing under various conditions |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
|-------------------------|--------------|----------|---------------------------------|---------------|
| Implement redundant sensors | High         | Reduce occlusion risk | Pass/fail based on sensor readings | Low residual risk due to fallback |

---

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 lifecycle approach ensures that the AEB pedestrian system is robust against E/E malfunctions, intended-function insufficiencies, and AI/data/model weaknesses. The HARA screening identifies key risks and safety goals are defined to mitigate these hazards. Verification through extensive testing and monitoring ensures the system operates safely in various scenarios.