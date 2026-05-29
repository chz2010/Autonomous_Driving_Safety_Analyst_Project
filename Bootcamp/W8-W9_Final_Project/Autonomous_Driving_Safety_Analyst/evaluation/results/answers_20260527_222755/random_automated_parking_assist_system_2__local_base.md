### Opening Map

- **ISO 26262**: Focuses on E/E malfunction risk.
- **SOTIF**: Evaluates intended-function insufficiencies, performance limitations, foreseeable misuse, and triggering conditions.
- **ISO 8800**: Ensures AI safety aspects are covered in the system design.

### Item Definition

| Function | Output | Inputs | Interfaces | ODD | Safety Role |
| --- | --- | --- | --- | --- | --- |
| Slot Detection | Parking slot coordinates | LiDAR, Camera data | ECU, Perception module | Parking lots, garages, marked and unmarked spaces | Ensures safe parking in designated areas. |
| Free-Space Estimation | Available space for vehicle movement | LiDAR, Camera data | ECU, Control module | Parking lots, garages, marked and unmarked spaces | Prevents over-parking or collision with obstacles. |
| Obstacle Detection | Detected obstacles and their characteristics | LiDAR, Camera data | ECU, Perception module | Parking lots, garages, marked and unmarked spaces | Ensures safe avoidance of obstacles during parking. |
| Trajectory Generation | Optimal path for vehicle movement | Slot coordinates, Free-space estimation | ECU, Control module | Parking lots, garages, marked and unmarked spaces | Guides the vehicle to its destination safely. |
| Low-Speed Control Handoff | Vehicle speed control | Obstacle detection, Trajectory generation | ECU, Driver interface | Parking lots, garages, marked and unmarked spaces | Ensures smooth transition from autonomous to manual control. |

### Functional Decomposition

| Function | Output | Possible Malfunction | Possible SOTIF Insufficiency | Possible ISO 8800 Concern | Applicable Standard(s) | HARA Carried Forward? |
| --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Parking slot coordinates | ECU failure, sensor malfunction | Inadequate slot detection in low-visibility conditions | Data coverage for low-visibility scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |
| Free-Space Estimation | Available space for vehicle movement | ECU failure, sensor malfunction | Insufficient free-space estimation in cluttered environments | Robustness of perception model under cluttered conditions | ISO 26262, SOTIF, ISO 8800 | Yes |
| Obstacle Detection | Detected obstacles and their characteristics | ECU failure, sensor malfunction | Inadequate obstacle detection in occluded areas | Dataset gaps for occlusion scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |
| Trajectory Generation | Optimal path for vehicle movement | ECU failure, software bug | Inadequate trajectory generation due to incorrect inputs | Model uncertainty and temporal instability | ISO 26262, SOTIF, ISO 8800 | Yes |
| Low-Speed Control Handoff | Vehicle speed control | ECU failure, sensor malfunction | Inadequate handover in dynamic traffic conditions | Release gate for dynamic traffic scenarios | ISO 26262, SOTIF, ISO 8800 | Yes |

### HARA Screening

| Function | Malfunction/Insufficiency | Hazardous Event | Operational Situation | Speed Assumptions | Severity Rationale | Exposure Rationale | Controllability Rationale | ASIL/QM | Uncertainty | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | ECU failure, sensor malfunction | Vehicle parking in an incorrect slot | Low-visibility conditions (e.g., rain, fog) | 5 km/h | Risk of collision with other vehicles or obstacles. | Occasional low-visibility conditions during parking. | Driver can manually correct the parking position if necessary. | ASIL B | Uncertainty due to varying weather conditions. | Review and update data coverage for low-visibility scenarios. |
| Free-Space Estimation | ECU failure, sensor malfunction | Vehicle over-parking or collision with obstacles | Cluttered environment (e.g., multiple parked cars) | 5 km/h | Risk of damage to the vehicle or other objects. | Frequent cluttered environments in parking lots and garages. | Driver can manually adjust the vehicle position if necessary. | ASIL B | Uncertainty due to varying traffic density. | Review and update data coverage for cluttered environments. |
| Obstacle Detection | ECU failure, sensor malfunction | Vehicle collision with detected obstacles | Occluded areas (e.g., behind parked cars) | 5 km/h | Risk of injury or vehicle damage. | Frequent occlusion scenarios in parking lots and garages. | Driver can manually avoid the obstacle if necessary. | ASIL B | Uncertainty due to varying occlusion levels. | Review and update data coverage for occluded areas. |
| Trajectory Generation | ECU failure, software bug | Vehicle movement along an incorrect path | Incorrect inputs from perception module (e.g., wrong slot coordinates) | 5 km/h | Risk of collision with other vehicles or obstacles. | Occasional incorrect inputs during parking. | Driver can manually correct the vehicle's trajectory if necessary. | ASIL B | Uncertainty due to varying input quality. | Review and update model robustness for incorrect inputs. |
| Low-Speed Control Handoff | ECU failure, sensor malfunction | Inadequate handover in dynamic traffic conditions | Dynamic traffic scenarios (e.g., merging vehicles) | 5-10 km/h | Risk of collision with other vehicles or obstacles. | Frequent dynamic traffic conditions during parking. | Driver can manually take over control if necessary. | ASIL B | Uncertainty due to varying traffic dynamics. | Review and update release gate for dynamic traffic scenarios. |

### Safety Goals, Functional Safety Concept, and Technical Safety Concept

#### Safety Goals Table
| ID | Related Function | Hazardous Event Prevented | ASIL or Safety Relevance | Safe State/ Degraded Behavior | Main Standard |
| --- | --- | --- | --- | --- | --- |
| SG1 | Slot Detection | Vehicle parking in an incorrect slot | ASIL B | Correct slot detection and parking position. | ISO 26262, SOTIF, ISO 8800 |
| SG2 | Free-Space Estimation | Vehicle over-parking or collision with obstacles | ASIL B | Correct free-space estimation for safe movement. | ISO 26262, SOTIF, ISO 8800 |
| SG3 | Obstacle Detection | Vehicle collision with detected obstacles | ASIL B | Correct obstacle detection and avoidance. | ISO 26262, SOTIF, ISO 8800 |
| SG4 | Trajectory Generation | Vehicle movement along an incorrect path | ASIL B | Correct trajectory generation for safe movement. | ISO 26262, SOTIF, ISO 8800 |
| SG5 | Low-Speed Control Handoff | Inadequate handover in dynamic traffic conditions | ASIL B | Smooth and safe transition to manual control. | ISO 26262, SOTIF, ISO 8800 |

#### Functional Safety Concept Table
| Fault/Condition | Vehicle-Level Safe Response | Driver/HMI Response | Degraded Mode | Rationale |
| --- | --- | --- | --- | --- |
| ECU failure | Disable parking function and alert driver. | HMI displays error message and prompts manual intervention. | Manual control mode with reduced speed limits. | Ensures safe operation even in case of E/E failures. |
| Sensor malfunction | Use backup sensors or fallback to manual control. | HMI alerts the driver and provides instructions for manual control. | Manual control mode with reduced speed limits. | Ensures safe operation even if primary sensors fail. |

#### Technical Safety Concept Table
| Mechanism | Allocated Component | Fault or Limitation Addressed | Diagnostic/Fallback Behavior | Timing Target | Verification Evidence |
| --- | --- | --- | --- | --- | --- |
| Slot Detection | Perception module | Sensor failure, ECU failure | Backup sensor data and fallback to manual control. | Real-time detection of slot coordinates. | HARA analysis, diagnostic tests, and real-world validation. |
| Free-Space Estimation | Control module | Cluttered environment, sensor malfunction | Use backup sensors or fallback to manual control. | Real-time estimation of available space. | HARA analysis, diagnostic tests, and real-world validation. |
| Obstacle Detection | Perception module | Occluded areas, sensor malfunction | Use backup sensors or fallback to manual control. | Real-time detection of obstacles. | HARA analysis, diagnostic tests, and real-world validation. |
| Trajectory Generation | Control module | Incorrect inputs from perception module | Use fallback trajectory generation logic. | Real-time path planning for safe movement. | HARA analysis, diagnostic tests, and real-world validation. |
| Low-Speed Control Handoff | ECU | Dynamic traffic conditions, sensor malfunction | Fallback to manual control with reduced speed limits. | Smooth transition between autonomous and manual modes. | HARA analysis, diagnostic tests, and real-world validation. |

### ISO 26262 Part 2-9 Lifecycle Assessment

| ISO 26262 Part | Purpose | Item-Specific Engineering Activities | Work Products/Evidence | Rationale/Unsafe Behavior Prevented | Interaction with SOTIF/ISO 8800 |
| --- | --- | --- | --- | --- | --- |
| Part 2: Functional Safety Management | Define the safety-related requirements and manage the development process. | Define safety goals, functional safety concept, technical safety concept. | Safety goals table, functional safety concept table, technical safety concept table. | Prevents E/E malfunctions from causing hazardous events. | Interacts with SOTIF by ensuring that intended functions are safe under all operating conditions. |
| Part 3: Item Definition | Define the item and its interfaces, including ODD assumptions. | Define slot detection, free-space estimation, obstacle detection, trajectory generation, low-speed control handoff functions. | Functional decomposition table. | Ensures clear definition of functions to prevent unsafe behavior. | Interacts with ISO 8800 by ensuring that AI safety aspects are covered in the system design. |
| Part 4: System Development | Develop the system architecture and allocate functional safety requirements. | Design the perception, control, and ECU modules. | System architectural design specification. | Ensures safe operation of the system through proper allocation of functions. | Interacts with SOTIF by ensuring that intended functions are safe under all operating conditions. |
| Part 5: Hardware Development | Develop hardware components and ensure their safety. | Design and test ECU, perception module, control module. | FMEDA reports, random hardware metrics. | Ensures reliable operation of hardware components. | Interacts with ISO 8800 by ensuring that AI safety aspects are covered in the system design. |
| Part 6: Software Development | Develop software components and ensure their safety. | Design and test perception algorithms, control logic. | Software safety requirements, unit tests, integration tests. | Ensures reliable operation of software components. | Interacts with SOTIF by ensuring that intended functions are safe under all operating conditions. |
| Part 7: Production | Ensure the production process meets safety standards. | Calibrate ECU, perception module, control module. | End-of-line calibration reports, DTCs. | Ensures consistent and reliable operation of the system in production. | Interacts with ISO 8800 by ensuring that AI safety aspects are covered in the system design. |
| Part 8: Supporting Processes | Ensure traceability and documentation of safety-related activities. | Maintain requirements traceability, verification planning. | Requirements traceability matrix, verification plan. | Ensures clear traceability and documentation of safety-related activities. | Interacts with SOTIF by ensuring that intended functions are safe under all operating conditions. |
| Part 9: ASIL Decomposition | Decompose the system into sub-systems and allocate ASIL levels. | Define ASIL levels for each function. | ASIL decomposition table, dependent failure analysis. | Ensures proper allocation of safety requirements to prevent hazardous events. | Interacts with SOTIF by ensuring that intended functions are safe under all operating conditions. |

### ISO 21448 (SOTIF) Function Analysis

| Item Function | Intended Performance Limitation | Triggering Condition | ODD Boundary/Assumption | Unsafe Effect | Known or Unknown Scenario Status | Validation Evidence Needed | Mitigation/ Degradation | Residual Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Inadequate slot detection in low-visibility conditions | Rain, fog, night-time lighting | Low-visibility parking lots and garages | Vehicle parking in an incorrect slot | Known scenario | Review and update data coverage for low-visibility scenarios. | Backup sensor data and fallback to manual control. | Uncertainty due to varying weather conditions. |
| Free-Space Estimation | Insufficient free-space estimation in cluttered environments | Multiple parked cars, narrow spaces | Cluttered parking lots and garages | Vehicle over-parking or collision with obstacles | Known scenario | Review and update data coverage for cluttered environments. | Use backup sensors or fallback to manual control. | Uncertainty due to varying traffic density. |
| Obstacle Detection | Inadequate obstacle detection in occluded areas | Occlusion behind parked cars, buses | Parking lots and garages with occlusions | Vehicle collision with detected obstacles | Known scenario | Review and update data coverage for occluded areas. | Use backup sensors or fallback to manual control. | Uncertainty due to varying occlusion levels. |
| Trajectory Generation | Inadequate trajectory generation due to incorrect inputs | Incorrect slot coordinates, wrong free-space estimation | Parking lots and garages with dynamic conditions | Vehicle movement along an incorrect path | Known scenario | Review and update model robustness for incorrect inputs. | Use fallback trajectory generation logic. | Uncertainty due to varying input quality. |
| Low-Speed Control Handoff | Inadequate handover in dynamic traffic conditions | Merging vehicles, changing traffic flow | Dynamic parking lots and garages with merging traffic | Vehicle collision with other vehicles or obstacles | Known scenario | Review and update release gate for dynamic traffic scenarios. | Fallback to manual control with reduced speed limits. | Uncertainty due to varying traffic dynamics. |

### ISO 8800 Function Assurance

| AI-Related Function | AI Safety Role | Data Requirement | Dataset/Label-Quality Gap | Robustness or Uncertainty Risk | OOD/Distribution-Shift Risk | Release Gate Criterion | Monitoring/Change-Control Evidence | Residual AI Risk Rationale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Slot Detection | Data coverage for low-visibility scenarios | Low-visibility conditions (e.g., rain, fog) | Limited data in low-visibility conditions. | Model uncertainty due to varying weather conditions. | Review and update data coverage for low-visibility scenarios. | Regular monitoring of model performance under different weather conditions. | Uncertainty due to varying weather conditions. |
| Free-Space Estimation | Data coverage for cluttered environments | Cluttered parking lots and garages (e.g., multiple parked cars) | Limited data in cluttered environments. | Model uncertainty due to varying traffic density. | Review and update data coverage for cluttered environments. | Regular monitoring of model performance under different traffic conditions. | Uncertainty due to varying traffic density. |
| Obstacle Detection | Data coverage for occluded areas | Occlusion behind parked cars, buses (e.g., dark clothing at night) | Limited data in occluded areas. | Model uncertainty due to varying occlusion levels. | Review and update data coverage for occluded areas. | Regular monitoring of model performance under different occlusion conditions. | Uncertainty due to varying occlusion levels. |
| Trajectory Generation | Robustness of perception model under cluttered conditions | Cluttered parking lots and garages (e.g., multiple parked cars) | Limited robustness in cluttered environments. | Model uncertainty due to varying input quality. | Review and update model robustness for incorrect inputs. | Regular monitoring of model performance under different cluttered conditions. | Uncertainty due to varying input quality. |
| Low-Speed Control Handoff | Release gate for dynamic traffic scenarios | Dynamic parking lots and garages with merging traffic (e.g., changing traffic flow) | Limited release gates in dynamic traffic scenarios. | Model uncertainty due to varying traffic dynamics. | Review and update release gate for dynamic traffic scenarios. | Regular monitoring of model performance under different traffic conditions. | Uncertainty due to varying traffic dynamics. |

### Verification and Validation Matrix

| Test Case | Injected Condition/Scenario | Expected Safe Behavior | Measurable Acceptance Criterion | Evidence Artifact | Linked Requirement |
| --- | --- | --- | --- | --- | --- |
| Slot Detection | Low-visibility conditions (e.g., rain, fog) | Correct slot detection and parking position. | High accuracy in low-visibility scenarios. | HARA analysis, diagnostic tests, real-world validation. | Safety goal SG1. |
| Free-Space Estimation | Cluttered environment (e.g., multiple parked cars) | Correct free-space estimation for safe movement. | Low error rate in cluttered environments. | HARA analysis, diagnostic tests, real-world validation. | Safety goal SG2. |
| Obstacle Detection | Occluded areas (e.g., behind parked cars) | Correct obstacle detection and avoidance. | High accuracy in occluded areas. | HARA analysis, diagnostic tests, real-world validation. | Safety goal SG3. |
| Trajectory Generation | Incorrect inputs from perception module (e.g., wrong slot coordinates) | Correct trajectory generation for safe movement. | Low error rate in incorrect input scenarios. | HARA analysis, diagnostic tests, real-world validation. | Safety goal SG4. |
| Low-Speed Control Handoff | Dynamic traffic conditions (e.g., merging vehicles) | Smooth and safe transition to manual control. | High success rate in dynamic traffic scenarios. | HARA analysis, diagnostic tests, real-world validation. | Safety goal SG5. |

### Production and Operation Controls

| Lifecycle Stage | Operational Risk | Control Activity | Pass/Fail or Release Criterion | Evidence Artifact | Feedback Loop | Rationale |
| --- | --- | --- | --- | --- | --- | --- |
| End-of-Line Calibration | Sensor health checks | Perform end-of-line calibration of ECU, perception module, control module. | No DTCs reported. | Calibration reports, DTC logs. | Continuous monitoring and corrective actions. | Ensures consistent operation of the system in production. |
| Sensor Health Checks | Regular sensor health checks | Conduct regular health checks on sensors and modules. | No critical failures detected. | Sensor health check logs, diagnostic tests. | Continuous monitoring and corrective actions. | Ensures reliable operation of the system during service. |

### Worst-Case Scenario

1