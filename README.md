# ID: 10974 - IEEE LATIN AMERICA TRANSACTIONS

# A Methodology for the Design and Validation of Hydrokinetic Energy Harvesting Systems for Rural Electrification

### Authors: 

F.S. Macedo-García, D. Mallada-Fernández, A. Fernández-Jiménez, J. Arau, M. Rico-Secades, M. Adam-Medina, and C. Aguilar.

### Affiliations:

**National Center for Research and Technological Development (CENIDET), Cuernavaca, Mexico**

**University Center for Water Research and Development (CUIDA), University of Oviedo, EP-Mieres, Spain**

**CE3I2 Research Group, University of Oviedo, EPI-Gijón, Spain** 

# Required Software

The simulations included in this repository were developed using LTspice, a SPICE simulator developed and distributed by Analog Devices. LTspice is free software that provides schematic capture, circuit simulation, and waveform visualization capabilities.

To run the models and reproduce the simulations included in this repository, a compatible installation of LTspice is required. The software can be downloaded free of charge from the official Analog Devices website:

https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html

The currently available version supports Windows and macOS, among other environments specified by the manufacturer.

# Models, Symbols, and Simulation Files

This repository includes the schematic symbols and model files required to implement and run the dynamic models developed in LTspice. The provided files allow the different models to be integrated as functional blocks within the simulation schematics.

The repository contains the elements associated with the models, including schematic symbol files (.asy), model and subcircuit files (.lib, .sub, or .cir, as applicable), as well as schematic and simulation files (.asc) required to configure and run the circuits.

These files allow the model structure to be reconstructed, the interconnections between the different subsystems to be established, and the simulations presented in the research work to be reproduced. The symbols are associated with their corresponding models and subcircuits, facilitating their direct integration into LTspice schematics.

# Supplementary Material

**Fig_1_10974** 

Presents an integrated representation of the main considerations required to configure and reproduce the simulations of the hydrokinetic system developed in LTspice. The figure complements the proposed methodology and provides a combined view of the input variables, dynamic models, operating conditions, energy conversion stages, and criteria used for system evaluation.

**Folder "LTSpice Integral Model With Battery**

In this folder, you can find the LTspice integral model of the hydrokinetic energy harvesting system for a turbine operating in a water channel, where you can change the battery voltage value and test different configurations.

**Folder "LTSpice Integral Model WITHOUT Battery"**

In this folder, you can find the LTspice integral model of the hydrokinetic energy harvesting system for a turbine operating in a water channel WITHOUT battery.

# Steps 

First, the **electrical demand of the off-grid rural household** is considered, since the generation system must be evaluated according to the electrical requirements it is intended to supply. For the residential load profile considered, the daily energy demand is 4.366 kWh/day and the critical instantaneous power is 661 W. These two parameters are used for different purposes: the daily energy demand is used to establish the storage requirements, whereas the critical power is used to evaluate the instantaneous capability of the energy conversion system.

The second block represents the **hydraulic resource**. The simulation configuration requires the definition of the equivalent hydraulic geometry and inlet operating conditions, including the equivalent width (beqv), inlet water depth (hi), inlet water velocity (Vwi), flow rate (Q), gravitational acceleration (g), inlet Froude number (Fri), and blockage factor (Kb). These parameters are used to determine the available hydraulic power and characterize the flow conditions under which the turbine operates. In particular, the model adopts an equivalent rectangular cross-section to represent channels that may present other geometries, as established in the proposed methodology.

The third block represents the **power extraction limits**. The proposed methodology is not based exclusively on the classical power coefficient but incorporates the extended power coefficient Cpx and blockage factor (Kb) to evaluate the available and extractable power from the channel. Based on the Froude-number analysis, the optimal condition Fri_opt (approx 0.30937) is considered, while the theoretical extraction limit corresponds to Cpx_max=0.345196 under the theoretical conditions established in the paper. These values provide reference conditions for the subsequent evaluation of the dynamic model.

The fourth block corresponds to the **turbine–PMG dynamic model**. The turbine and permanent magnet generator are represented using an equivalent dynamic model that enables the hydraulic, mechanical, and electrical domains to be integrated within the LTspice environment. The mechanical behavior is determined by the inertia, friction, and torque parameters, while the PMG model incorporates parameters such as the voltage–speed coefficient (Kv), number of pole pairs (pp), inertia, and friction. This representation allows the turbine operating conditions to be related to the generator angular speed and electrical frequency.

The fifth block represents the **power electronics and energy storage subsystem**. The system incorporates an AC/DC rectification stage and a DC/DC conversion stage to condition the generated energy and establish the interface with the DC bus. At the system level, simplified and averaged converter models are employed; therefore, switching losses, magnetic losses, and all parasitic elements are not explicitly represented. This simplification allows the analysis to focus on the dynamic interaction among the hydraulic, mechanical, electrical, and power electronic subsystems. Three storage configurations are considered: a 24 V battery, a 12 V battery, and battery-free operation.

Finally, the sixth block represents the **frequency-based quasi-MPPT strategy**. The PMG electrical frequency (Fe) is used as the reference variable because of its direct relationship with generator rotational speed and, consequently, with the turbine operating conditions. The strategy employs a two-state logic: initially, the system remains in the startup condition without power extraction until the minimum required frequency is reached; subsequently, the quasi-MPPT operating region is enabled. In this way, the power and control references can be generated without requiring an additional mechanical speed sensor.

The central section of the figure summarizes the **integration of these subsystems within LTspice**, from the hydraulic input and available/extractable power calculation, through the turbine–PMG dynamic model and quasi-MPPT controller, to the DC/DC converter, DC bus, storage, and residential load. This integration enables the system to be evaluated as a coupled system rather than as a set of independently analyzed subsystems.

Finally, the figure identifies the **specific conditions used for simulation-based validation**. The system starts with a water velocity of 0 m/s during the first 10 s to represent the initial standstill condition and evaluate the startup process. Subsequently, controlled water-velocity variations of 1.0, 0.7, 0.6, and 0.8 m/s are applied. The same hydraulic excitation is maintained for the different storage configurations, allowing their behavior to be compared under equivalent hydraulic conditions. From the LTspice simulations, the extractable hydraulic power, DC-bus output power, PMG electrical frequency, rotational speed, and quasi-MPPT operating state are evaluated.

Overall, this representation provides a **configuration and reproducibility guide for the integrated model**, identifying the elements that must be defined before running the simulations and illustrating how the hydraulic, mechanical, electrical, and control variables are interconnected within the LTspice model.

# Interpretation of Physical Quantities Represented in LTspice

It should be noted that LTspice is an electrical circuit simulation environment and, therefore, the variables obtained directly from the simulations are expressed in terms of electrical quantities, primarily voltage and current. In the proposed model, these variables are used as **electrical analogues of the physical quantities associated with the hydraulic and mechanical subsystems**.

For this reason, the simulation results must be interpreted carefully by considering the correspondence established between each electrical variable in the model and the physical quantity it represents. In particular, variables such as angular speed, torque, inertia, friction, hydraulic power, and other mechanical or hydraulic quantities may be represented by equivalent electrical variables within the LTspice circuit.

Consequently, **the values displayed by LTspice should not be directly interpreted as physical electrical quantities of the system in every case**. For each result, the analogy used in the model must first be identified, and the corresponding conversion relationship must be applied before assigning a physical interpretation to the simulated variable. This consideration is particularly important when analyzing transient responses and the order of magnitude of mechanical and hydraulic variables represented through the equivalent circuit.

This approach enables the hydraulic, mechanical, electrical, and power electronic domains to be integrated within a single simulation environment; however, it requires an explicit interpretation of the correspondence between the simulated electrical variables and the physical quantities of the hydrokinetic system.


## Citation and contact

Please cite the associated manuscript when using this material. For questions about reproduction, contact the authors through the affiliation above.

