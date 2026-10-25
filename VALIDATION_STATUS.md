# Validation status and scientific limitations

| Evidence | Status | Interpretation |
|---|---|---|
| Internal protocol and source/hash checks | Checked | Confirms internal record consistency, not scientific truth |
| 72 training + 72 held-out synthetic trials | Complete | 24 paired scenarios across 3 controller arms |
| 96 hover-feasible actuator-cap trials | Complete | Short saturation transients, not sustained robustness |
| Control-family hyperparameter fairness | Limited | Shared tuning budget only for 2 parameters; prior development unequal |
| Independently calibrated plant / external dynamics | Not established | In-house uncalibrated Euler-state model |
| PX4/Gazebo communications and read-only motor shadow | Exploratory | Interfaces and static feasibility only |
| V3 controlled PX4 closed-loop flight | **Not performed** | No PX4 flight-performance comparison against PID |
| Physical flight and field testing | **Not performed** | No hardware safety or deployment claims |
| Independent V3 technical peer review | **Not established** | No reviewer endorsement |

Notes:

1. **Effective mass** need not equal physical payload mass. Unknown rotor thrust coefficients and disturbances may be confounded with mass.
2. The 95% paired-bootstrap intervals in the report characterize variation under the chosen synthetic scenario generator, not generalized robustness to real-world airframes.
3. A higher-performing in-house benchmark is a valid bounded computational finding, not an externally verified state-of-the-art controller.
4. There are no grounds for claiming rotor-actuator safety from the read-only shadow telemetry tests.
