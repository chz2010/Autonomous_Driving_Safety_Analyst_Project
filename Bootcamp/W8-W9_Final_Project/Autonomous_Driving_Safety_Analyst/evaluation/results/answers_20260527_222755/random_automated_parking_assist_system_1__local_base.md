### Opening Map

- **ISO 26262** = E/E malfunction risk.
- **SOTIF** = unsafe intended functionality from limitations/ODD/triggering conditions.
- **ISO 8800** = AI/data/model assurance risk.

---

### Item Definition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Parking slot coordinates | Sensor failure, misalignment | Low visibility, occlusion | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Free-Space Estimation | Available parking space size | Sensor noise, false positives | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Obstacle Detection | Presence and location of obstacles | Sensor failure, occlusion | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Trajectory Generation | Optimal parking path | Algorithmic errors, sensor noise | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Low-Speed Control Handoff | Smooth transition to manual control | Software bugs, hardware failure | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |

---

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Parking slot coordinates | Sensor failure, misalignment | Low visibility, occlusion | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Free-Space Estimation | Available parking space size | Sensor noise, false positives | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Obstacle Detection | Presence and location of obstacles | Sensor failure, occlusion | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Trajectory Generation | Optimal parking path | Algorithmic errors, sensor noise | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |
| Low-Speed Control Handoff | Smooth transition to manual control | Software bugs, hardware failure | Unforeseeable obstacles | Unforeseeable misuse | ISO 26262, ISO 8800 | Yes |

---

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | S Rationale | E Rationale | C Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Sensor failure, misalignment | Incorrect slot detection leading to collision | Low visibility, occlusion | 5-10 km/h | High risk of collision if incorrect slot is chosen. | Frequent in low-light conditions and narrow spaces. | Driver can manually correct but time delay could be critical. | ASIL B | Uncertain due to varying visibility. | Detailed HARA for each scenario. |
| Free-Space Estimation | Sensor noise, false positives | Incorrect space estimation leading to collision | Unforeseeable obstacles | 5-10 km/h | High risk of collision if space is underestimated. | Frequent in cluttered parking lots. | Driver can manually correct but time delay could be critical. | ASIL B | Uncertain due to varying obstacle density. | Detailed HARA for each scenario. |
| Obstacle Detection | Sensor failure, occlusion | Incorrect obstacle detection leading to collision | Unforeseeable obstacles | 5-10 km/h | High risk of collision if undetected obstacles are present. | Frequent in cluttered parking lots and narrow spaces. | Driver can manually correct but time delay could be critical. | ASIL B | Uncertain due to varying obstacle density. | Detailed HARA for each scenario. |
| Trajectory Generation | Algorithmic errors, sensor noise | Incorrect trajectory leading to collision | Unforeseeable obstacles | 5-10 km/h | High risk of collision if incorrect path is chosen. | Frequent in cluttered parking lots and narrow spaces. | Driver can manually correct but time delay could be critical. | ASIL B | Uncertain due to varying obstacle density. | Detailed HARA for each scenario. |
| Low-Speed Control Handoff | Software bugs, hardware failure | Incorrect handoff leading to collision | Unforeseeable obstacles | 5-10 km/h | High risk of collision if incorrect handoff is performed. | Frequent in cluttered parking lots and narrow spaces. | Driver can manually correct but time delay could be critical. | ASIL B | Uncertain due to varying obstacle density. | Detailed HARA for each scenario. |

---

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG01 | Slot Detection | Incorrect slot detection leading to collision | ASIL B | Correct slot selection | ISO 26262, ISO 8800 |
| SG02 | Free-Space Estimation | Incorrect space estimation leading to collision | ASIL B | Correct space estimation | ISO 26262, ISO 8800 |
| SG03 | Obstacle Detection | Incorrect obstacle detection leading to collision | ASIL B | Correct obstacle avoidance | ISO 26262, ISO 8800 |
| SG04 | Trajectory Generation | Incorrect trajectory leading to collision | ASIL B | Correct path selection | ISO 26262, ISO 8800 |
| SG05 | Low-Speed Control Handoff | Incorrect handoff leading to collision | ASIL B | Smooth transition to manual control | ISO 26262, ISO 8800 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| Sensor failure | Emergency stop and manual control | Haptic feedback and visual alerts | Manual control mode | Ensures driver can take over in critical situations. |
| Algorithmic errors | Fallback to predefined safe trajectory | Haptic feedback and visual alerts | Safe trajectory mode | Ensures system remains functional with reduced autonomy. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Sensor validation | ECU | Sensor failure | Haptic feedback and visual alerts | Real-time | Log files, diagnostic tests |

---

### ISO 26262 Part 2-9 Lifecycle Assessment

#### Part 2: Functional Safety Management
- **Purpose**: Define the safety goals and functional safety concept.
- **Item-Specific Engineering Activities**:
  - Define ASIL levels for each function.
  - Develop HARA tables.
  - Perform fault tree analysis (FTA) and failure mode effects analysis (FMEA).
- **Work Products/Evidence**:
  - Safety goals table.
  - Functional safety concept table.
  - Technical safety concept table.
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation in all scenarios.
- **Interaction with SOTIF/ISO 8800**: ISO 26262 ensures E/E system reliability, while SOTIF and ISO 8800 ensure AI robustness.

#### Part 3: Item Definition
- **Purpose**: Define the item's functions, inputs, outputs, interfaces, ODD, assumptions, safety role.
- **Item-Specific Engineering Activities**:
  - Detailed functional decomposition.
  - Hazard analysis.
  - Safety goal definition.
- **Work Products/Evidence**:
  - Functional decomposition table.
  - Safety goals table.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system operates safely within its defined ODD.

#### Part 4: System Development
- **Purpose**: Develop and integrate the system components.
- **Item-Specific Engineering Activities**:
  - Software development.
  - Hardware design.
  - Integration testing.
- **Work Products/Evidence**:
  - Software architecture diagram.
  - Hardware design documentation.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system integrates safely and functions as intended.

#### Part 5: Hardware Development
- **Purpose**: Develop hardware components.
- **Item-Specific Engineering Activities**:
  - Fault tree analysis (FTA).
  - Failure mode effects analysis (FMEA).
  - Diagnostic coverage assessment.
- **Work Products/Evidence**:
  - FTA and FMEA reports.
  - Diagnostic test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures hardware reliability.

#### Part 6: Software Development
- **Purpose**: Develop software components.
- **Item-Specific Engineering Activities**:
  - Unit testing.
  - Integration testing.
  - Random hardware metrics assessment.
- **Work Products/Evidence**:
  - Test reports.
  - Diagnostic logs.
- **Rationale/Unsafe Behavior Prevented**: Ensures software reliability.

#### Part 7: Production
- **Purpose**: Ensure safe production and operation.
- **Item-Specific Engineering Activities**:
  - End-of-line calibration.
  - Service recalibration.
  - Diagnostic test execution.
- **Work Products/Evidence**:
  - Calibration logs.
  - Diagnostic test results.
- **Rationale/Unsafe Behavior Prevented**: Ensures the system operates safely in production.

#### Part 8: Supporting Processes
- **Purpose**: Ensure traceability and documentation.
- **Item-Specific Engineering Activities**:
  - Requirements traceability matrix (RTM).
  - Verification planning.
  - Documentation review.
- **Work Products/Evidence**:
  - RTM.
  - Verification plan.
- **Rationale/Unsafe Behavior Prevented**: Ensures all activities are documented and traceable.

#### Part 9: ASIL Decomposition
- **Purpose**: Ensure safe operation in all scenarios.
- **Item-Specific Engineering Activities**:
  - ASIL decomposition.
  - Dependent failure analysis.
  - Common-cause/cascading failure analysis.
- **Work Products/Evidence**:
  - ASIL decomposition table.
  - Failure mode effects analysis (FMEA).
- **Rationale/Unsafe Behavior Prevented**: Ensures safe operation in all scenarios.

---

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Low visibility, occlusion | Poor lighting conditions, narrow spaces | Parking lot with low visibility | Incorrect slot detection leading to collision | Known | HARA and sensor validation tests. | Fallback to manual control mode. | ASIL B risk remains due to varying visibility conditions. |
| Free-Space Estimation | Sensor noise, false positives | Unforeseeable obstacles | Cluttered parking lot | Incorrect space estimation leading to collision | Known | Perception validation using nuScenes dataset. | Fallback to manual control mode. | ASIL B risk remains due to varying obstacle density. |
| Obstacle Detection | Sensor failure, occlusion | Unforeseeable obstacles | Narrow spaces with occlusions | Incorrect obstacle detection leading to collision | Known | Perception validation using nuScenes dataset. | Fallback to manual control mode. | ASIL B risk remains due to varying obstacle density. |
| Trajectory Generation | Algorithmic errors, sensor noise | Unforeseeable obstacles | Cluttered parking lot and narrow spaces | Incorrect trajectory leading to collision | Known | Perception validation using nuScenes dataset. | Fallback to predefined safe trajectory mode. | ASIL B risk remains due to varying obstacle density. |
| Low-Speed Control Handoff | Software bugs, hardware failure | Unforeseeable obstacles | Narrow spaces with occlusions | Incorrect handoff leading to collision | Known | HARA and sensor validation tests. | Fallback to manual control mode. | ASIL B risk remains due to varying obstacle density. |

---

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release-Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Ensuring correct slot selection | High-resolution sensor data, accurate parking slot coordinates | Sensor misalignment, occlusion | Algorithmic errors in low-visibility conditions | Unforeseeable obstacles leading to incorrect slot detection | Comprehensive dataset covering various lighting and occlusion scenarios. | Regular model retraining and validation using nuScenes dataset. | ASIL B risk remains due to varying visibility conditions. |
| Free-Space Estimation | Ensuring correct space estimation | High-resolution sensor data, accurate parking space size | Sensor noise, false positives | Algorithmic errors in cluttered environments | Unforeseeable obstacles leading to incorrect space estimation | Comprehensive dataset covering various obstacle densities and clutter levels. | Regular model retraining and validation using nuScenes dataset. | ASIL B risk remains due to varying obstacle density. |
| Obstacle Detection | Ensuring correct obstacle detection | High-resolution sensor data, accurate obstacle location | Sensor failure, occlusion | Algorithmic errors in narrow spaces with occlusions | Unforeseeable obstacles leading to incorrect obstacle detection | Comprehensive dataset covering various obstacle types and clutter levels. | Regular model retraining and validation using nuScenes dataset. | ASIL B risk remains due to varying obstacle density. |
| Trajectory Generation | Ensuring correct trajectory selection | High-resolution sensor data, accurate path planning | Algorithmic errors, sensor noise | Unforeseeable obstacles leading to incorrect trajectory generation | Narrow spaces with occlusions and cluttered environments | Comprehensive dataset covering various obstacle types and clutter levels. | Regular model retraining and validation using nuScenes dataset. | ASIL B risk remains due to varying obstacle density. |
| Low-Speed Control Handoff | Ensuring smooth transition to manual control | High-resolution sensor data, accurate handoff timing | Software bugs, hardware failure | Unforeseeable obstacles leading to incorrect handoff | Narrow spaces with occlusions and cluttered environments | Comprehensive dataset covering various obstacle types and clutter levels. | Regular model retraining and validation using nuScenes dataset. | ASIL B risk remains due to varying obstacle density. |

---

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Slot Detection | Low visibility, occlusion | Correct slot selection | No incorrect slot detection leading to collision | HARA and sensor validation tests. | SG01 |
| Free-Space Estimation | Sensor noise, false positives | Correct space estimation | No incorrect space estimation leading to collision | Perception validation using nuScenes dataset. | SG02 |
| Obstacle Detection | Sensor failure, occlusion | Correct obstacle detection | No incorrect obstacle detection leading to collision | Perception validation using nuScenes dataset. | SG03 |
| Trajectory Generation | Algorithmic errors, sensor noise | Correct trajectory selection | No incorrect trajectory leading to collision | Perception validation using nuScenes dataset. | SG04 |
| Low-Speed Control Handoff | Software bugs, hardware failure | Smooth transition to manual control | No incorrect handoff leading to collision | HARA and sensor validation tests. | SG05 |

---

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor accuracy | Calibrate sensors at end of production line. | No calibration errors detected. | Calibration logs. | Continuous monitoring and re-calibration. | Ensures sensor accuracy for safe operation. |
| Sensor Health Checks | Sensor failure | Regularly check sensor health during operation. | No critical failures reported. | Diagnostic test results. | Real-time monitoring and alerts. | Ensures sensors operate within specifications. |
| Software/Model Version Traceability | Model drift | Maintain traceability of software/model versions in use. | Correct version in use for all units. | Software/version control logs. | Regular audits and updates. | Ensures consistent model performance across fleet. |
| Service Recalibration | Sensor accuracy degradation | Recalibrate sensors during service intervals. | No calibration errors detected. | Calibration logs. | Continuous monitoring and re-calibration. | Ensures sensor accuracy for safe operation. |
| DTCs | Diagnostic trouble codes | Monitor and address diagnostic trouble codes (DTCs). | No critical DTCs reported. | DTC logs. | Real-time monitoring and alerts. | Ensures system operates within safety margins. |

---

### Worst-Case Scenario

#### Scenario Assumptions Table
| Ego Speed | Object Speed | Weather | Lighting | Occlusion | Road Type | Traffic Density | Automation Mode | TTC or Available Sensing Time | Driver Fallback Assumption |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 5-10 km/h | Unforeseeable obstacles | Rainy conditions | Dim lighting | Narrow spaces with occlusions | Parking lot | High density | Autonomous mode | 2 seconds | Driver can take over control. |

#### Accident-Chain Table
| Step | Degraded/Missing Signal | System Interpretation | Vehicle Response | Hazard Escalation | Evidence Needed |
| --- | --- | --- | --- | --- | --- |
| 1 | Sensor failure, occlusion | Incorrect slot detection | Emergency stop and manual control mode engaged. | Collision risk reduced but not eliminated. | HARA and sensor validation tests. |
| 2 | Incorrect trajectory generation | Incorrect path selection | Vehicle