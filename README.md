# MILP-Based-EV-Charging-Scheduling-for-a-Solar-Grid-Network

## Hierarchical Energy Management and MILP-Based EV Charging Scheduling for a Solar–Grid Integrated EV Charging Network

## 1. Project Overview

This project focuses on the optimal scheduling of Electric Vehicle (EV) charging in a solar–grid integrated charging network using **Mixed-Integer Linear Programming (MILP)** in MATLAB.

The proposed framework coordinates solar photovoltaic (PV) generation and utility grid power to schedule EV charging across multiple Electric Vehicle Charging Stations (EVCSs) while satisfying battery State of Charge (SoC) requirements, charging time windows, port availability, and power capacity constraints.

A hierarchical energy management approach is considered, consisting of distribution-level energy allocation and EV charging station-level scheduling. The optimization model aims to improve solar energy utilization while considering system-level and participant-level economic objectives.

## 2. Objectives

- Develop a hierarchical energy management framework for a solar–grid integrated EV charging network.
- Optimize EV charging schedules using Mixed-Integer Linear Programming.
- Assign EVs to available charging stations and charging ports.
- Coordinate solar PV energy and grid power for EV charging.
- Maintain EV charging power, station capacity, port availability, and grid and solar power constraints.
- Satisfy the required battery SoC before each EV's departure.
- Generate a 15-minute-resolution EV charging schedule over a 24-hour horizon.

## 3. Tools and Technologies

- **MATLAB** — mathematical modelling and optimization.
- **Mixed-Integer Linear Programming (MILP)** — charging scheduling and resource allocation.
- **Optimization Toolbox (`intlinprog`)** — solving the MILP optimization problem.
- **Solar PV and utility grid modelling** — energy source coordination.
- **CSV data processing** — organizing EV charging schedule and energy allocation results.

## 4. System Configuration

The simulation considers the following charging infrastructure:

| Charging Station | Charger Configuration | Total Station Capacity |
|---|---|---:|
| EVCS-1 | 2 × 22 kW Type-2 AC | 44 kW |
| EVCS-2 | 2 × 50 kW CCS | 100 kW |
| EVCS-3 | 2 × 15 kW Bharat DC-001 | 30 kW |

**System parameters:**

- Scheduling horizon: 24 hours
- Time resolution: 15 minutes
- Total time slots: 96
- EVs in the preliminary simulation: 5
- Charging ports: 6
- Maximum grid capacity: 150 kW
- Solar allocation limit: 100 kW
- Charging efficiency: 95%
- Assumed charging tariff: ₹10/kWh
- Assumed operating cost: ₹1/kWh

The tariff, operating cost, and objective weights are study assumptions rather than verified field measurements.

## 5. Methodology

### Level 1: Distribution-Level Energy Allocation

The upper level considers the available solar PV generation, grid capacity, electricity price, and aggregate EV charging demand to determine feasible energy allocation.

### Level 2: EV Charging Station Scheduling

The lower level determines EV-to-port assignments and charging power while considering:

- EV arrival and departure times.
- Initial and required battery SoC.
- Battery capacity and maximum charging power.
- Charging-port availability and power ratings.
- Station capacity limits.
- Solar and grid power availability.

### MILP Optimization

The optimization model uses two principal types of decision variables:

- **Binary variables:** Determine whether an EV is assigned to a particular charging port during a time slot.
- **Continuous variables:** Determine total charging power, solar power, and grid power allocated to each EV.

The charging power balance is represented as:

`P_charging = P_solar + P_grid`

The SoC is updated according to the charging energy supplied and battery capacity, subject to charging efficiency. The model also enforces SoC limits and the required SoC at departure.

The economic objective combines normalized system-level profit, participant-level profit, and solar energy utilization, using weights of 0.40, 0.40, and 0.20, respectively.

## 6. Dataset and Input Parameters

The project combines time-dependent energy data with configured EV and charging station parameters.

The report describes the following inputs:

- Electricity load profile.
- Solar PV generation profile.
- Electricity price data based on an Indian Energy Exchange (IEX)-based public dataset.
- EV arrival and departure times.
- Battery capacity, initial SoC, and required SoC.
- EV charging station and port configuration.
- Grid and solar capacity limits.

The energy profiles are aligned to a common 15-minute time index to form a 96-slot daily dataset.

## 7. Preliminary Results

The mid-term presentation reports the following results for one preliminary optimization run:

| Metric | Reported Result |
|---|---:|
| Total charging energy | 135.2632 kWh |
| Solar energy supplied | 132.5658 kWh |
| Grid energy supplied | 2.6974 kWh |
| Solar share of charging energy | 98.01% |
| EVs considered | 5 |
| Charging ports | 6 |
| Scheduling slots | 96 |
| Decision variables before presolve | 12,000 |
| Reported solver status | Optimal |

These results are specific to the inputs, assumptions, and constraints used in the reported simulation. The reported optimal solver status does not, by itself, establish that every practical operating condition or economic objective has been fully validated.

**Validation note:** The supplied CSV schedule does not reproduce the final SoC values reported in the presentation. Its final recorded SoC values are below the corresponding required SoC values for all five EVs. Therefore, the schedule requires further validation before the results can be treated as a fully feasible final solution.


*Note: This is a suggested folder structure. The MATLAB scripts and result figures listed above should be added only when their actual files are available. The supplied schedule CSV and project PDFs can be placed in their corresponding folders.*

## 8. Current Status and Future Work

The mid-term project report and presentation document the implementation of the data preprocessing pipeline, MILP formulation, MATLAB optimization workflow, schedule extraction, and preliminary feasibility testing.

The remaining work includes:

- Refining fixed EV-to-station and port assignments.
- Separating port connection status from actual charging status.
- Introducing station-specific tariffs, operating costs, and switching penalties where appropriate.
- Verifying electricity price units.
- Validating the final SoC requirements and power balance.
- Comparing uncontrolled charging, grid-only charging, solar-priority charging, and MILP-based scheduling.
- Conducting sensitivity analysis for solar availability, grid capacity, EV demand, charging windows, and objective weights.
- Evaluating solar utilization, grid energy consumption, peak demand, economic performance, and solver execution time.

## 9. Conclusion

This project develops a MATLAB-based MILP framework for coordinated EV charging in a solar–grid integrated network. By combining EV-port assignment, charging power optimization, battery SoC modelling, and infrastructure constraints, the framework provides a foundation for structured energy management across multiple charging stations.

The preliminary results indicate the potential for high solar energy utilization under the configured simulation assumptions. Further validation and comparative analysis are required to establish the final feasibility and performance of the proposed scheduling framework.

