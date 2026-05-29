### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Evaluates intended-function insufficiencies, performance limitations, foreseeable misuse, and triggering conditions.
- **ISO 8800**: Ensures AI/data/model assurance.

---

### Item Definition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Side Object Detection | Object detection and classification | Sensor failure, false negatives/positives | Inadequate perception performance under low visibility conditions | Dataset gaps in low-visibility scenarios | ISO 26262, ISO 21448, ISO 8800 | Yes |
| Relative Velocity Estimation | Velocity estimation | Calculation errors due to sensor noise | Performance limitations at high/low velocities | Unknown | ISO 26262, ISO 21448 | No |
| Blind-Zone Occupancy | Zone occupancy status | False positives/negatives | Inaccurate occupancy detection under occlusion | Unknown | ISO 26262, ISO 21448 | Yes |
| Driver Warning | Visual and audio warnings | Malfunctioning warning system | Misleading or insufficient warnings to the driver | Unknown | ISO 26262, ISO 21448 | No |
| Interface Output | Displayed information | Data transmission errors | Inconsistent interface behavior under network issues | Unknown | ISO 26262, ISO 21448 | Yes |

---

### Functional Decomposition
| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern |
| --- | --- | --- | --- | --- |
| Side Object Detection | Object detection and classification | Sensor failure, false negatives/positives | Inadequate perception performance under low visibility conditions | Dataset gaps in low-visibility scenarios |
| Relative Velocity Estimation | Velocity estimation | Calculation errors due to sensor noise | Performance limitations at high/low velocities | Unknown |
| Blind-Zone Occupancy | Zone occupancy status | False positives/negatives | Inaccurate occupancy detection under occlusion | Unknown |
| Driver Warning | Visual and audio warnings | Malfunctioning warning system | Misleading or insufficient warnings to the driver | Unknown |
| Interface Output | Displayed information | Data transmission errors | Inconsistent interface behavior under network issues | Unknown |

---

### HARA Screening
| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity (S) | Exposure (E) | Controllability (C) | ASIL/QM |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side Object Detection | Sensor failure, false negatives/positives | Collision with detected object | Urban and highway lane changes, day/night, moderate rain | 30-50 km/h, 80-130 km/h | S4: Severe harm (injury/death) | E2: Occasional but not frequent | C3: Driver can avoid with fallback | ASIL B |
| Relative Velocity Estimation | Calculation errors due to sensor noise | Incorrect speed-based warnings | Urban and highway lane changes, day/night, moderate rain | 30-50 km/h, 80-130 km/h | S2: Moderate harm (property damage) | E4: Frequent but not critical | C3: Driver can avoid with fallback | ASIL B |
| Blind-Zone Occupancy | False positives/negatives | Misleading driver warnings | Urban and highway lane changes, day/night, moderate rain | 30-50 km/h, 80-130 km/h | S2: Moderate harm (property damage) | E4: Frequent but not critical | C3: Driver can avoid with fallback | ASIL B |
| Driver Warning | Malfunctioning warning system | Driver misinformed or uninformed | Urban and highway lane changes, day/night, moderate rain | 30-50 km/h, 80-130 km/h | S4: Severe harm (injury/death) | E2: Occasional but not frequent | C3: Driver can avoid with fallback | ASIL B |
| Interface Output | Data transmission errors | Inconsistent interface behavior | Urban and highway lane changes, day/night, moderate rain | 30-50 km/h, 80-130 km/h | S2: Moderate harm (property damage) | E4: Frequent but not critical | C3: Driver can avoid with fallback | ASIL B |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG01 | Side Object Detection | Collision with detected object | ASIL B | No collision, reduced speed | ISO 26262-3:2018, Clause 7.5.1 |
| SG02 | Relative Velocity Estimation | Incorrect speed-based warnings | ASIL B | Correct warnings, no driver misinformed | ISO 26262-3:2018, Clause 7.5.1 |
| SG03 | Blind-Zone Occupancy | Misleading driver warnings | ASIL B | Clear and accurate warnings | ISO 26262-3:2018, Clause 7.5.1 |
| SG04 | Driver Warning | Driver misinformed or uninformed | ASIL B | Timely and clear warnings | ISO 26262-3:2018, Clause 7.5.1 |
| SG05 | Interface Output | Inconsistent interface behavior | ASIL B | Consistent and reliable display | ISO 26262-3:2018, Clause 7.5.1 |

---

### ISO 26262 Part 2-9 Lifecycle Assessment
| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| **Part 2** | Functional Safety Management | Define safety goals, manage supplier interfaces, develop a safety plan | Safety goals document, supplier interface agreements, safety plan | Ensure no E/E malfunction leads to hazardous events | SOTIF and ISO 8800 address functional limitations. |
| **Part 3** | Item Definition | Decompose item into functions, define inputs/outputs, ODD assumptions | Functional decomposition diagram, input/output specification, ODD document | Prevent unsafe behavior by defining clear functions and boundaries | SOTIF and ISO 8800 ensure intended functionality is safe. |
| **Part 4** | System Development | Design architecture, allocate safety requirements to hardware/software elements, integrate system | Architecture design document, safety requirement allocation matrix, integration plan | Ensure no E/E malfunction leads to hazardous events | SOTIF and ISO 8800 address performance limitations. |
| **Part 5** | Hardware Development | Develop hardware components, perform FMEDA, ensure diagnostic coverage | Hardware development plan, FMEDA report, diagnostic test results | Ensure hardware reliability and diagnostics cover potential failures | SOTIF and ISO 8800 address hardware-specific issues. |
| **Part 6** | Software Development | Develop software components, ensure freedom from interference, implement watchdogs | Software development plan, interference checks, watchdog logic implementation | Ensure no E/E malfunction leads to hazardous events | SOTIF and ISO 8800 address software-specific issues. |
| **Part 7** | Production | Perform end-of-line calibration, service recalibration, monitor DTCs | Calibration procedures, service recalibration plan, diagnostic trouble code (DTC) logs | Ensure no E/E malfunction leads to hazardous events during production | SOTIF and ISO 8800 address production-specific issues. |
| **Part 8** | Supporting Processes | Manage configuration/change, ensure requirements traceability, develop verification planning | Configuration management plan, change control procedures, verification plan | Ensure no E/E malfunction leads to hazardous events through process management | SOTIF and ISO 8800 address process-related issues. |
| **Part 9** | ASIL Decomposition | Decompose system into sub-systems, analyze dependent failures | ASIL decomposition matrix, dependent failure analysis report | Ensure no E/E malfunction leads to hazardous events at the system level | SOTIF and ISO 8800 address system-level issues. |

---

### ISO 21448 (SOTIF) Function Analysis
| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side Object Detection | Inadequate performance under low visibility conditions | Poor weather, rain, fog | Urban and highway lane changes, day/night, moderate rain | Missed detection leading to collision | Known | Visibility distribution analysis, dataset coverage review | Enhanced sensor fusion, fallback logic | Low residual risk due to fallback mechanisms. |
| Relative Velocity Estimation | Performance limitations at high/low velocities | High/low velocity scenarios | Urban and highway lane changes, day/night, moderate rain | Incorrect warnings leading to driver misinformed | Unknown | Scenario-based testing, real-world validation | Real-time monitoring of system performance | Moderate residual risk due to unknown scenarios. |
| Blind-Zone Occupancy | Inaccurate occupancy detection under occlusion | Occlusion behind parked cars or buses | Urban and highway lane changes, day/night, moderate rain | Misleading driver warnings leading to collision | Known | Occlusion testing, dataset coverage review | Improved sensor calibration, fallback logic | Low residual risk due to fallback mechanisms. |
| Driver Warning | Insufficient or misleading warnings | Network issues, system malfunction | Urban and highway lane changes, day/night, moderate rain | Driver misinformed or uninformed leading to collision | Known | Network testing, diagnostic checks | Real-time monitoring of network status | Moderate residual risk due to known issues. |

---

### ISO 8800 Function Assurance
| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Side Object Detection | Perception accuracy | High-resolution sensor data, diverse weather conditions | Dataset gaps in low-visibility scenarios | Model robustness under varying weather conditions | Unknown | Real-world validation, scenario-based testing | Continuous monitoring of model performance and dataset updates | Low residual risk due to fallback mechanisms. |
| Relative Velocity Estimation | Speed estimation accuracy | Sensor fusion data, high/low velocity scenarios | Performance limitations at high/low velocities | Model uncertainty in extreme speed conditions | Unknown | Scenario-based testing, real-world validation | Real-time monitoring of system performance | Moderate residual risk due to unknown scenarios. |
| Blind-Zone Occupancy | Zone occupancy status | Sensor data, occlusion detection | Inaccurate occupancy detection under occlusion | Model robustness under occlusion conditions | Known | Occlusion testing, dataset coverage review | Improved sensor calibration and fallback logic | Low residual risk due to fallback mechanisms. |
| Driver Warning | Warnings accuracy | Network data, system health status | Insufficient or misleading warnings | Model uncertainty in network issues | Unknown | Network testing, diagnostic checks | Real-time monitoring of network status | Moderate residual risk due to known issues. |

---

### Verification and Validation Matrix
| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Side Object Detection | Low visibility conditions (rain, fog) | No collision with detected object | Collision rate < 1% in low-visibility scenarios | Sensor performance logs, dataset coverage report | SG01 |
| Relative Velocity Estimation | High/low velocity scenarios | Correct speed-based warnings | Warning accuracy > 95% at high/low velocities | Real-time warning system logs, scenario testing results | SG02 |
| Blind-Zone Occupancy | Occlusion behind parked cars or buses | Clear and accurate warnings | Warnings issued correctly in occluded zones | Occlusion testing report, dataset coverage review | SG03 |
| Driver Warning | Network issues, system malfunction | Timely and clear warnings | Driver informed accurately during network issues | Network testing logs, diagnostic checks | SG04 |
| Interface Output | Data transmission errors | Consistent and reliable display | Display accuracy > 95% under varying conditions | Interface performance logs, real-world validation results | SG05 |

---

### Production and Operation Controls
| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Hardware reliability | Perform end-of-line calibration | No hardware failures detected | Calibration logs, diagnostic test results | Real-time monitoring of production line | Ensure no E/E malfunction during production. |
| Sensor Health Checks | Sensor performance | Regular sensor health checks | Sensors functioning within specifications | Sensor performance logs, real-world validation results | Continuous monitoring and maintenance | Ensure sensors operate reliably under varying conditions. |
| Software/Model Version Traceability | Software/model version accuracy | Maintain software/model version traceability | Correct versions installed on all units | Version control logs, deployment records | Real-time monitoring of system updates | Prevent incorrect software/models from causing issues. |
| Service Recalibration | System performance degradation | Perform service recalibration | No significant performance degradation | Recalibration logs, diagnostic checks | Continuous monitoring and maintenance | Ensure system performance remains reliable over time. |
| DTCs | Diagnostic trouble codes | Monitor DTCs | No critical DTCs present | DTC logs, diagnostic test results | Real-time monitoring of system health | Identify and address E/E malfunctions early. |
| Field Feedback | User feedback | Collect user feedback | Positive user experience reported | User survey results, support logs | Continuous improvement process | Enhance product reliability based on real-world usage. |
| Incident/Near-Miss Review | Safety incidents/near-misses | Conduct incident review | Lessons learned documented | Incident reports, corrective action plans | Root cause analysis and mitigation planning | Prevent recurrence of similar issues. |
| OTA Gates | Over-the-Air updates | Implement OTA gates | No critical issues during update process | Update logs, real-time monitoring tools | Continuous monitoring and validation | Ensure safe deployment of software updates. |

---

### Worst-Case Scenario
| Assumption | Value | Impact on Safety Analysis |
| --- | --- | --- |
| Ego Speed | 30-50 km/h, 80-130 km/h | Higher speeds increase severity but reduce exposure due to faster reaction times. |
| Object/road-user speed | 3-15 km/h | Lower speeds decrease severity and exposure. |
| Weather | Moderate rain | Reduces visibility, increasing severity and exposure. |
| Lighting | Day/night | Nighttime increases severity due to reduced visibility. |
| Occlusion | Behind parked cars or buses | Increases exposure by creating blind spots. |

| Step | Degraded/missing signal | System interpretation | Vehicle response | Hazard escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure, low visibility | Missed detection of object | No warning issued | Collision risk increases | Sensor performance logs, dataset coverage report |
| 2 | Incorrect velocity estimation | Misleading speed-based warnings | Driver misinformed or uninformed | Increased risk of collision | Real-time warning system logs, scenario testing results |
| 3 | Occlusion behind parked cars | Inaccurate occupancy detection | Misleading driver warnings | Collision risk increases | Occlusion testing report, dataset coverage review |
| 4 | Network issues, system malfunction | Insufficient or misleading warnings | Driver misinformed or uninformed | Increased risk of collision | Network testing logs, diagnostic checks |

| ISO 26262 Malfunction View | SOTIF Limitation View | ISO 8800 AI/Data/Model View | Expected Mitigation | Verification Evidence |
| --- | --- | --- | --- | --- |
| Sensor failure leading to missed detection | Inadequate performance under low visibility conditions | Model robustness under varying weather conditions | Enhanced sensor fusion, fallback logic | Continuous monitoring of model performance and dataset updates |

| Design/Process Decision | Risk Reduced | Rationale | Measurable Acceptance Criterion | Residual Risk |
| --- | --- | --- | --- | --- |
| Implement enhanced sensor fusion and fallback logic | Low residual risk due to fallback mechanisms. | Ensure no E/E malfunction leads to hazardous events during production. | Collision rate < 1% in low-visibility scenarios, warning accuracy > 95% at high/low velocities, clear and accurate warnings issued correctly in occluded zones, display accuracy > 95% under varying conditions. | Moderate residual risk due to unknown scenarios. |

---

### Final Safety Argument
The final safety argument is based on a comprehensive analysis across ISO 26262, SOTIF (ISO 21448), and ISO 8800 standards. The system has been designed with multiple layers of redundancy and fallback mechanisms to ensure no single point of failure leads to hazardous events. Key measures include:

- **Sensor Fusion**: Ensures robust object detection even under low visibility conditions.
- **Fallback Logic**: Provides clear warnings in case of sensor or network issues.
- **Real-Time Monitoring**: Continuously monitors system performance and updates models based on real-world data.

These measures, combined with rigorous testing and validation processes, ensure the system operates safely across various operational scenarios. The residual risks are managed through continuous monitoring, feedback loops, and proactive mitigation strategies.