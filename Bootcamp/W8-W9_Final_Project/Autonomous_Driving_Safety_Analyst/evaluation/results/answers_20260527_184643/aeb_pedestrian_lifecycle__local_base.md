### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Addresses intended-function insufficiencies and triggering conditions.
- **ISO 8800**: Ensures AI/data/model safety.

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
|----------|--------|---------------------|------------------------------|-------------------------|----------------------|
| AEB Pedestrian Detection | Detect pedestrian and estimate distance to collision | Sensor failure, false negatives | Late detection due to occlusion or low confidence | Data quality issues, model robustness | ISO 26262-3:2018, Clause 7; SOTIF Evaluation Scheme; ISO 8800 |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
|----------|--------|---------------------|------------------------------|-------------------------|
| **1. Perception** | Detect pedestrian and estimate distance to collision | Sensor failure, false negatives | Late detection due to occlusion or low confidence | Data quality issues, model robustness |
| **2. Estimation** | Estimate time-to-collision (TTC) | Calculation errors, sensor latency | Inaccurate TTC leading to late braking | Model uncertainty, data coverage |
| **3. Tracking** | Track pedestrian movement and update distance estimate | Sensor failure, false positives | Poor tracking accuracy in occlusions or dynamic environments | Data quality issues, model robustness |
| **4. Decision-making** | Determine if AEB should be triggered | Software errors, incorrect logic | Inadequate decision-making due to low confidence or complex scenarios | Model uncertainty, data coverage |
| **5. Actuation** | Trigger AEB and control vehicle deceleration | Hardware failure, software bugs | Delayed braking response due to system latency | Data quality issues, model robustness |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM |
|----------|---------------------------|-----------------|----------------------|-------------|-------------|-------------|---------|
| 1. Perception | Sensor failure, false negatives | Late detection of pedestrian | Urban road, 30 km/h, moderate traffic, occlusion possible | High severity due to potential collision risk | Moderate exposure as pedestrians are common in urban areas | Low controllability by driver or fallback system | ASIL B |
| 2. Estimation | Calculation errors, sensor latency | Inaccurate TTC leading to late braking | Highway road, 80 km/h, clear weather, low traffic density | High severity due to potential collision risk | Low exposure as highway scenarios are less frequent | Moderate controllability by fallback system | ASIL B |
| 3. Tracking | Sensor failure, false positives | Poor tracking accuracy in occlusions or dynamic environments | Urban road, 40 km/h, moderate traffic, occlusion possible | High severity due to potential collision risk | Moderate exposure as occlusions are common in urban areas | Low controllability by driver or fallback system | ASIL B |
| 4. Decision-making | Software errors, incorrect logic | Inadequate decision-making due to low confidence or complex scenarios | Urban road, 30 km/h, moderate traffic, occlusion possible | High severity due to potential collision risk | Moderate exposure as urban scenarios are common | Low controllability by driver or fallback system | ASIL B |
| 5. Actuation | Hardware failure, software bugs | Delayed braking response due to system latency | Urban road, 30 km/h, moderate traffic, occlusion possible | High severity due to potential collision risk | Moderate exposure as urban scenarios are common | Low controllability by driver or fallback system | ASIL B |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table

| ID | Related Function | Hazardous Event Prevented | ASIL/Safety Relevance | Safe State/ Degraded Behavior |
|----|------------------|--------------------------|----------------------|------------------------------|
| 1  | Perception        | Late detection of pedestrian | B                    | Delayed AEB trigger           |
| 2  | Estimation       | Inaccurate TTC leading to late braking | B                  | Reduced stopping distance     |
| 3  | Tracking         | Poor tracking accuracy in occlusions or dynamic environments | B                   | Misleading distance estimate  |
| 4  | Decision-making   | Inadequate decision-making due to low confidence or complex scenarios | B                    | Incorrect AEB trigger        |
| 5  | Actuation        | Delayed braking response due to system latency | B                  | Reduced deceleration         |

#### Functional Safety Concept Table

| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
|-----------------|----------------------------|--------------------|---------------|-----------|
| Sensor failure  | Fallback to manual driving | Warning            | Manual control | High severity risk |
| Software error  | Degraded AEB functionality | Warning            | Reduced AEB   | Moderate severity risk |

#### Technical Safety Concept Table

| Mechanism       | Allocated Component        | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
|-----------------|----------------------------|------------------------------|------------------------------|---------------|-----------------------|
| Perception      | LiDAR, camera              | Sensor failure               | Redundant sensors            | Real-time     | HARA, diagnostic logs  |
| Estimation      | Controller                 | Calculation errors           | Software redundancy          | Real-time     | Unit tests, validation |
| Tracking        | Kalman filter              | False positives              | Fallback to manual driving   | Real-time     | HMI feedback, logs    |
| Decision-making | Logic gate                 | Incorrect logic              | Degraded AEB mode            | Real-time     | Formal verification   |
| Actuation       | Brake system               | Hardware failure             | Manual override              | Real-time     | Diagnostic checks     |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Define safety goals, HARA, S/E/C, ASIL.
- **Work Products/Evidence**: HARA table, S/E/C ratings, ASIL determination.
- **Rationale/Unsafe Behavior Prevented**: High severity risks from late detection and inadequate response.
- **Interaction with SOTIF/ISO 8800**: Ensure alignment of safety goals with SOTIF requirements.

#### Part 3: Item Definition
- **Item-Specific Engineering Activities**: Define functions, ODD, HARA, S/E/C, ASIL.
- **Work Products/Evidence**: Functional decomposition table, HARA screening table.
- **Rationale/Unsafe Behavior Prevented**: Address high severity risks from late detection and inadequate response.

#### Part 4: System Development
- **Item-Specific Engineering Activities**: Architecture design, requirements allocation, integration, validation.
- **Work Products/Evidence**: System architecture diagram, functional safety concept, technical safety concept.
- **Rationale/Unsafe Behavior Prevented**: Ensure robust system design to handle sensor failures and software errors.

#### Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA, diagnostic coverage.
- **Work Products/Evidence**: Hardware safety plan, diagnostic test results.
- **Rationale/Unsafe Behavior Prevented**: Ensure hardware reliability through redundancy and diagnostics.

#### Part 6: Software Development
- **Item-Specific Engineering Activities**: Software safety requirements, architecture, freedom from interference.
- **Work Products/Evidence**: Software design documents, unit tests, integration tests.
- **Rationale/Unsafe Behavior Prevented**: Ensure software robustness to handle sensor failures and calculation errors.

#### Part 7: Production
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration, DTCs.
- **Work Products/Evidence**: Calibration logs, diagnostic trouble codes (DTC) records.
- **Rationale/Unsafe Behavior Prevented**: Ensure consistent system performance through production checks.

#### Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability, verification planning.
- **Work Products/Evidence**: Change control logs, requirement trace matrix.
- **Rationale/Unsafe Behavior Prevented**: Maintain consistency and traceability in development processes.

#### Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: Failure modes and effects analysis (FMEA), fault tree analysis (FTA).
- **Rationale/Unsafe Behavior Prevented**: Identify and mitigate dependent failures to ensure overall system safety.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
|---------------|--------------------------------|----------------------|------------------------|--------------|-------------------------------|---------------------------|-------------------------|-----------------------|
| Perception    | Late detection due to occlusion  | Occlusion in urban areas | Urban roads, moderate traffic density | Collision risk | Known                         | Scenario catalogue entry, confidence/uncertainty calibration | Fallback to manual driving | ASIL B |
| Estimation    | Inaccurate TTC leading to late braking | Low sensor latency or high calculation errors | Highway road, clear weather, low traffic density | Reduced stopping distance | Known                         | Validation results under rain/night/occlusion | Degraded AEB functionality | ASIL B |
| Tracking      | Poor tracking accuracy in occlusions or dynamic environments | Occlusions and dynamic pedestrian movement | Urban roads, moderate traffic density, occlusions possible | Misleading distance estimate | Known                         | HMI feedback, logs     | Manual control fallback | ASIL B |
| Decision-making | Inadequate decision-making due to low confidence or complex scenarios | Low confidence in sensor data or complex scenario handling | Urban roads, occlusions, dynamic environments | Incorrect AEB trigger | Known                         | Formal verification    | Degraded AEB mode      | ASIL B |
| Actuation     | Delayed braking response due to system latency | System latency issues | Urban roads, moderate traffic density, occlusions possible | Reduced deceleration | Known                         | Diagnostic checks      | Manual override        | ASIL B |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|-------------------------------|---------------------------|-----------------------|------------------------------------|---------------------------|
| Perception          | Data-driven detection | High-resolution LiDAR and camera data | Occlusions, low-contrast scenarios | Model robustness in occlusions | Distribution shift due to varying weather conditions | Model performance under rain/night/occlusion | Regular model retraining, field monitoring | ASIL B |
| Estimation          | Time-to-collision estimation | Sensor fusion data | Calculation errors, sensor latency | Robustness against sensor failures | OOD scenarios in urban environments | Validation results under diverse driving conditions | Continuous monitoring of system performance | ASIL B |
| Tracking            | Pedestrian tracking and movement prediction | Historical pedestrian trajectories | False positives, occlusions | Model uncertainty in dynamic environments | Distribution shift due to changing traffic patterns | Regular model retraining, field feedback | Real-time monitoring of tracking accuracy | ASIL B |
| Decision-making     | AEB decision logic | Sensor data, historical collision scenarios | Low confidence in sensor data | Uncertainty in complex urban scenarios | OOD scenarios involving unexpected pedestrian behavior | Formal verification, scenario-based testing | Continuous monitoring and fallback system performance | ASIL B |
| Actuation           | Braking control | Vehicle actuator signals | System latency issues | Robustness against hardware failures | ODD restrictions based on traffic conditions | Diagnostic checks, field feedback | Real-time monitoring of braking response | ASIL B |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|-----------------------------|------------------------|---------------------------------|------------------|--------------------|
| Perception | Occlusion in urban area      | Detect pedestrian       | Detection rate > 95%             | HARA, diagnostic logs | ASIL B |
| Estimation | Low sensor latency          | Estimate TTC accurately | TTC error < 1 second            | Unit tests, validation results | ASIL B |
| Tracking   | Occlusions and dynamic movement | Track pedestrian        | Tracking accuracy > 80%         | HMI feedback, logs | ASIL B |
| Decision-making | Low confidence in sensor data | Trigger AEB appropriately | AEB trigger rate < 5% false positives | Formal verification, scenario-based testing | ASIL B |
| Actuation   | System latency issues       | Decelerate vehicle      | Braking response time < 0.2 seconds | Diagnostic checks, field feedback | ASIL B |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|-------------------------------|------------------|--------------|-----------|
| End-of-Line Calibration | Sensor accuracy | Calibrate sensors | Calibration within tolerance | Calibration logs | Continuous monitoring | Ensure consistent sensor performance |
| Sensor Health Checks | System reliability | Monitor health | No critical failures detected | Diagnostic test results | Real-time alerts | Maintain system integrity |
| Software/Model Version Traceability | Code safety | Track versions | Correct version deployed | Change control logs | Regular audits | Prevent code drift and ensure safety |
| Service Recalibration | Sensor accuracy | Recalibrate sensors | Calibration within tolerance | Calibration logs | Continuous monitoring | Ensure consistent sensor performance |
| DTCs | System diagnostics | Monitor DTCs | No critical faults present | Diagnostic trouble codes (DTC) records | Real-time alerts | Detect and address issues early |
| Field Feedback | User experience | Collect feedback | Positive user ratings | Customer surveys, support logs | Continuous improvement | Enhance system performance |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time | Driver Fallback Assumption |
|-----------|-------------|--------|---------|----------|----------|---------------|----------------|-------------------------------|-----------------------------|
| 30 km/h   | 4 km/h      | Clear  | Day     | Yes      | Urban    | Moderate      | L2+            | 1 second                      | Manual control fallback    |

#### Accident-Chain Table
| Step | Degraded/ Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
|------|--------------------------|-----------------------|------------------|------------------|----------------|
| 1    | Occlusion                 | False negative         | No AEB trigger   | Collision risk   | HARA, diagnostic logs |
| 2    | Late detection            | Delayed braking       | Reduced deceleration | Increased collision risk | Validation results under occlusions |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
|---------------------------|----------------------|----------------------------|---------------------|-----------------------|
| Sensor failure            | Late detection       | Data quality issues        | Fallback to manual driving | HARA, diagnostic logs |
| Software error            | Inaccurate TTC       | Model robustness           | Degraded AEB functionality | Unit tests, validation |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
|-------------------------|--------------|----------|---------------------------------|---------------|
| Implement redundant sensors | High         | Reduce sensor failure risk | Detection rate > 95% | ASIL B |

---

### Final Safety Argument

The ISO 26262, SOTIF, and ISO 8800 safety lifecycle approach ensures that the AEB pedestrian system is designed to handle various operational situations with appropriate safety measures. The HARA screening identifies high severity risks from late detection and inadequate response, which are mitigated through robust design, fallback mechanisms, and continuous monitoring. The verification and validation matrix provides measurable criteria to ensure safe operation, while production controls maintain consistent performance. The worst-case scenario analysis highlights potential hazards and the necessary mitigation strategies. Overall, this safety lifecycle approach ensures that the AEB system is reliable and safe for deployment in urban environments.