### Opening Map

**ISO 26262 = E/E malfunction risk**
- **Malfunction**: Hardware failure or software bug in the perception system.
- **Insufficiency**: Insufficient performance of the perception system under certain conditions.

**SOTIF = unsafe intended functionality from limitations/ODD/triggering conditions**
- **Limitation**: Perception system fails to detect objects within its range or under specific conditions (e.g., rain, low light).
- **Triggering Condition**: Objects are present but not detected due to sensor limitations.
- **ODD Boundary**: Operating the perception system outside defined road types and speeds.

**ISO 8800 = AI/data/model assurance risk**
- **Risk**: Data quality issues or model robustness problems leading to incorrect object detection.

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|----------------------|
| Perception | Object detection and tracking | Sensor failure, software bug | Limited perception range, low confidence in certain conditions | Data gaps, label quality issues | ISO 26262, ISO 21448, ISO 8800 | Yes |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|
| Detection | Object detection | Sensor failure, software bug | Limited perception range, low confidence in certain conditions | Data gaps, label quality issues | ISO 26262, ISO 21448, ISO 8800 |
| Tracking | Object tracking | Sensor failure, software bug | Limited perception range, low confidence in certain conditions | Data gaps, label quality issues | ISO 26262, ISO 21448, ISO 8800 |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
|----------|---------------------------|----------------|----------------------|------------|------------|------------|---------|------------|------------|
| Detection | Sensor failure, software bug | Object collision | Rainy weather, low light conditions | Risk of sensor failure leading to undetected objects | High probability due to frequent rainy and low-light conditions | Driver cannot avoid in time; fallback available but not always reliable | ASIL C | Low | Review sensor redundancy |
| Tracking | Sensor failure, software bug | Object collision | Rainy weather, low light conditions | Risk of sensor failure leading to undetected objects | High probability due to frequent rainy and low-light conditions | Driver cannot avoid in time; fallback available but not always reliable | ASIL C | Low | Review sensor redundancy |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
|----|-----------------|--------------------------|-------------------------|----------------------------|--------------|
| 1  | Detection        | Object collision          | ASIL C                  | Fallback to manual driving  | ISO 26262    |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
|-----------------|----------------------------|--------------------|---------------|----------|
| Sensor failure  | Activate fallback mode      | Warning             | Manual driving| Prevent collision risk   |

#### Technical Safety Concept Table
| Mechanism       | Allocated Component        | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
|-----------------|----------------------------|--------------------------------|------------------------------|--------------|-----------------------|
| Redundant sensors | Perception system          | Sensor failure             | Fallback to manual driving    | Real-time     | HARA, diagnostic logs |

### ISO 26262 Part 2-9 Lifecycle Assessment

#### ISO 26262 Part 2: Functional Safety Management
- **Purpose**: Define the safety lifecycle and manage functional safety activities.
- **Item-Specific Engineering Activities**: Risk assessment, risk management plan, DIA/supplier interface.
- **Work Products/Evidence**: Safety plan, confirmation measures, impact analysis.

#### ISO 26262 Part 3: Item Definition
- **Purpose**: Define the system and its functions.
- **Item-Specific Engineering Activities**: Functional decomposition, HARA, S/E/C, ASIL determination.
- **Work Products/Evidence**: Functional safety concept, technical safety concept.

#### ISO 26262 Part 4: System Development
- **Purpose**: Develop the system architecture and requirements.
- **Item-Specific Engineering Activities**: Architecture design, requirements allocation, integration, validation.
- **Work Products/Evidence**: System architecture diagram, software/hardware specifications, test plans.

#### ISO 26262 Part 5: Hardware Development
- **Purpose**: Develop hardware components.
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA, diagnostic coverage.
- **Work Products/Evidence**: Hardware design documents, FMEDA reports, diagnostic tests.

#### ISO 26262 Part 6: Software Development
- **Purpose**: Develop software components.
- **Item-Specific Engineering Activities**: Software safety requirements, architecture, freedom from interference checks.
- **Work Products/Evidence**: Software specifications, code reviews, unit/integration test plans.

#### ISO 26262 Part 7: Production, Operation, Service, Decommissioning
- **Purpose**: Ensure safe operation and service.
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, DTCs, field monitoring.
- **Work Products/Evidence**: Calibration procedures, service manuals, field feedback reports.

#### ISO 26262 Part 8: Supporting Processes
- **Purpose**: Manage the safety lifecycle processes.
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Change logs, requirement trace matrices, verification plans.

#### ISO 26262 Part 9: ASIL Decomposition
- **Purpose**: Decompose ASIL for sub-functions.
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: ASIL decomposition tables, FMEA, FTA.

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/Degradation | Residual Risk Rationale |
|---------------|--------------------------------|----------------------|------------------------|--------------|---------------------------------|----------------------------|-----------------------|-------------------------|
| Perception     | Limited perception range       | Rainy weather, low light conditions | Operating outside defined ODD | Object collision | Known but not fully validated | Sensor performance tests, field data collection | Fallback to manual driving | ASIL C risk remains due to limited sensor coverage |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|---------------------------|-----------------------|-----------------------------------|-------------------------|
| Perception          | Data-driven detection | High-quality labeled data for various scenarios | Gaps in label quality, especially in low-light and rainy conditions | Model robustness issues under varying weather conditions | Distribution shift due to changing environmental factors | Comprehensive dataset coverage, regular model retraining | Continuous monitoring of model performance, field data collection | ASIL C risk remains due to potential model drift |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|-----------------------|---------------------------------|------------------|--------------------|
| Sensor failure test | Simulated sensor failure during rainy weather | System fallback to manual driving | No collision in predefined scenarios | Diagnostic logs, HARA results | ASIL C requirement |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|--------------------------------|------------------|--------------|----------|
| End-of-line calibration | Sensor accuracy | Calibration of sensors | No errors in sensor readings | Calibration logs, diagnostic tests | Continuous monitoring | Ensure accurate object detection |

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time (s) | Driver Fallback |
|------------------|--------------------|--------|---------|----------|-----------|---------------|--------------|-----------------------------------|----------------|
| 60               | 5                   | Rainy  | Low     | None     | Urban     | Moderate      | L2             | 3                                 | Available       |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
|------|-------------------------|-----------------------|------------------|------------------|----------------|
| 1    | Sensor failure          | Object not detected   | No braking        | Collision risk   | Diagnostic logs, HARA results |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
|---------------------------|----------------------|----------------------------|--------------------|-----------------------|
| Sensor failure            | Limited perception range | Data gaps, label quality issues | Fallback to manual driving | Diagnostic logs, HARA results |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
|-------------------------|--------------|----------|---------------------------------|--------------|
| Add redundant sensors    | ASIL C       | Reduce sensor failure risk | No errors in diagnostic logs | ASIL C risk remains |

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 combined approach ensures a comprehensive safety case for the lane maintaining perception system. The HARA screening identified potential risks at ASIL C level, which are mitigated through redundant sensors and fallback mechanisms. Continuous monitoring and validation ensure that the system remains safe under various operating conditions.