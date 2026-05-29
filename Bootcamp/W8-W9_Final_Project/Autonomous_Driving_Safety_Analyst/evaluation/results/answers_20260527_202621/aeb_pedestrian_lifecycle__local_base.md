### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Addresses intended-function insufficiencies and triggering conditions.
- **ISO 8800**: Ensures AI/data/model safety, particularly in perception and decision-making.

---

### Item Definition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) |
|----------|--------|---------------------|----------------------------|-------------------------|-----------------------|
| Perception | Object detection, classification | Sensor failure, incorrect object classification | Late pedestrian detection, insufficient stopping distance | Data coverage, model robustness | ISO 26262-3:2018, ISO 21448, ISO 8800 |

---

### Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
|----------|--------|---------------------|----------------------------|-------------------------|
| Perception | Object detection, classification | Sensor failure, incorrect object classification | Late pedestrian detection, insufficient stopping distance | Data coverage, model robustness |

---

### HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | S Rationale | E Rationale | C Rationale | ASIL/QM |
|----------|---------------------------|-----------------|----------------------|-------------|-------------|-------------|---------|
| Perception | Sensor failure, incorrect object classification | Late pedestrian detection, insufficient stopping distance | Urban road, 30 km/h, pedestrian at 5 km/h, moderate traffic, short TTC | E/E malfunction could lead to wrong perception output | Exposure is high due to frequent pedestrian interactions in urban areas | Controllability relies on fallback driver and AEB system | ASIL B |
| Perception | Late pedestrian detection, insufficient stopping distance | Collision with pedestrian | Urban road, 30 km/h, pedestrian at 5 km/h, moderate traffic, short TTC | Exposure is high due to frequent pedestrian interactions in urban areas | Controllability relies on fallback driver and AEB system | ASIL B |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept
#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior |
|----|------------------|--------------------------|-------------------------|------------------------------|
| S1 | Perception | Late pedestrian detection, insufficient stopping distance | ASIL B | Degraded behavior: Reduced speed and warning to driver |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
|-----------------|----------------------------|--------------------|---------------|----------|
| Sensor failure  | E-stop and warning          | Warning            | Manual control | Ensures safety in case of sensor failure |

#### Technical Safety Concept Table
| Mechanism       | Allocated Component        | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
|-----------------|---------------------------|-------------------------------|------------------------------|--------------|-----------------------|
| Perception      | LiDAR, camera              | Sensor failure                | E-stop and warning           | Real-time    | HARA, diagnostic tests |

---

### ISO 26262 Part 2-9 Lifecycle Assessment
#### ISO 26262 Part 2: Functional Safety Management
- **Item-Specific Engineering Activities**: Risk assessment, supplier interface management.
- **Work Products/Evidence**: HARA, SOTIF analysis.
- **Rationale/Unsafe Behavior Prevented**: Ensures safety goals are met through functional decomposition and HARA.

#### ISO 26262 Part 3: Item Definition
- **Item-Specific Engineering Activities**: Functional requirements definition, ODD assumptions.
- **Work Products/Evidence**: Safety goals, functional safety concept.
- **Rationale/Unsafe Behavior Prevented**: Defines safe states and degraded behaviors to prevent hazardous events.

#### ISO 26262 Part 4: System Development
- **Item-Specific Engineering Activities**: Architecture design, requirements allocation, integration.
- **Work Products/Evidence**: Technical safety concept, architecture diagram.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is designed to meet safety goals.

#### ISO 26262 Part 5: Hardware Development
- **Item-Specific Engineering Activities**: Hardware safety requirements, FMEDA.
- **Work Products/Evidence**: Hardware safety analysis report.
- **Rationale/Unsafe Behavior Prevented**: Identifies and mitigates hardware failures that could impact perception accuracy.

#### ISO 26262 Part 6: Software Development
- **Item-Specific Engineering Activities**: Software safety requirements, architecture design.
- **Work Products/Evidence**: Software safety analysis report.
- **Rationale/Unsafe Behavior Prevented**: Ensures software is robust and failsafe in critical situations.

#### ISO 26262 Part 7: Production
- **Item-Specific Engineering Activities**: End-of-line calibration, service recalibration.
- **Work Products/Evidence**: Calibration reports, service logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is calibrated and ready for production.

#### ISO 26262 Part 8: Supporting Processes
- **Item-Specific Engineering Activities**: Configuration/change management, requirements traceability.
- **Work Products/Evidence**: Traceability matrix, configuration logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is developed and maintained according to safety goals.

#### ISO 26262 Part 9: ASIL Decomposition
- **Item-Specific Engineering Activities**: Dependent failure analysis, common-cause/cascading failure analysis.
- **Work Products/Evidence**: ASIL decomposition table.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system is decomposed to meet safety goals.

---

### ISO 21448 (SOTIF) Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
|---------------|---------------------------------|----------------------|------------------------|---------------|-------------------------------|---------------------------|-------------------------|-----------------------|
| Perception     | Late pedestrian detection       | Short TTC            | Urban road, 30 km/h    | Collision risk | Known                         | Scenario catalogue entry, confidence calibration | E-stop and warning      | ASIL B |

---

### ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness/Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
|---------------------|---------------|------------------|--------------------------|----------------------------|---------------------------|------------------------|-----------------------------------|-----------------------------|
| Perception          | Data-driven perception | High-quality pedestrian data, diverse scenarios | Limited dataset coverage for occluded pedestrians | Model overfitting to training data | Distribution shift in weather conditions | Comprehensive validation under various scenarios | Continuous monitoring and field feedback | ASIL B |

---

### Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
|-----------|----------------------------|-----------------------|---------------------------------|------------------|--------------------|
| Perception | Occluded pedestrian         | Correct detection     | Detection rate > 95%             | HARA, test logs   | S1                 |

---

### Production and Operation Controls
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
|-----------------|------------------|------------------|--------------------------------|--------------------|--------------|-----------|
| End-of-Line Calibration | Sensor accuracy | Calibration check | Pass/fail based on test results | Calibration report | Continuous monitoring | Ensures sensor accuracy |

---

### Worst-Case Scenario
#### Scenario Assumptions Table
| Ego Speed (km/h) | Object Speed (km/h) | Weather | Lighting | Occlusion | Road Type | Traffic Density | TTC or Available Sensing Time (s) | Driver Fallback Assumption |
|------------------|--------------------|--------|----------|----------|-----------|---------------|-----------------------------------|-----------------------------|
| 30               | 5                   | Clear  | Daylight | None     | Urban     | Moderate      | 2.5                               | Manual control             |

#### Accident-Chain Table
| Step | Degraded/ Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
|------|--------------------------|-----------------------|------------------|------------------|----------------|
| 1    | Sensor failure           | Incorrect pedestrian detection | Late AEB trigger | Collision risk   | HARA, diagnostic logs |

#### Standard-View Table
| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
|---------------------------|----------------------|----------------------------|--------------------|-----------------------|
| Sensor failure            | Late pedestrian detection | Model overfitting          | E-stop and warning | HARA, diagnostic logs |

#### Engineering-Decision Table
| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
|-------------------------|--------------|----------|---------------------------------|---------------|
| Implement redundant sensors | ASIL B        | Ensures robust perception | Detection rate > 95% | ASIL B |

---

### Final Safety Argument
The AEB pedestrian system is designed to meet ISO 26262, SOTIF, and ISO 8800 requirements. The system includes robust perception, safety goals, functional safety concepts, technical safety concepts, comprehensive validation, and continuous monitoring. The worst-case scenario analysis ensures that the system can handle edge cases with reduced risk.