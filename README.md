
<!-- Add the main Battery-Pack-Modules block diagram or assembled-pack render here. -->

# Project Overview

Battery-Pack-Modules is an experimental battery-management and power-distribution platform developed to explore the design of compact, modular and production-oriented lithium-ion battery packs.

The project combines cell monitoring, electrical protection, high-current switching, embedded diagnostics and mechanical pack integration into a documented hardware platform.

The current design is centered around a **12-series lithium-ion battery pack** intended for approximately **1 kW-class applications**, with a high-current path designed for loads in the **20 A to 30 A range**. The exact continuous and peak ratings will be established through electrical, thermal and long-duration validation.

The project is intended to document not only the completed battery pack, but also the engineering decisions behind its protection architecture, component selection, PCB layout, cell interconnection, manufacturing and testing.

## Project Objectives

* Develop a modular battery-management platform for multi-series lithium-ion packs.
* Monitor individual cell-group voltages and pack temperature.
* Protect the battery against electrical and thermal fault conditions.
* Control the connection between the cells, charger and external load.
* Measure charge and discharge current through a dedicated shunt.
* Support controlled pre-charge and pre-discharge sequences.
* Integrate embedded monitoring, communication and diagnostics.
* Design a compact PCB capable of carrying significant current.
* Document the complete schematic, PCB, firmware and validation process.
* Evaluate the design as a foundation for future battery-pack variants.

## Custom Electronics

The platform is built around a custom battery-management PCB designed specifically for the electrical requirements of a multi-cell lithium-ion battery pack.

The board combines:

* Cell-voltage monitoring.
* Temperature sensing.
* Charge and discharge protection.
* High-current MOSFET switching.
* Current measurement.
* Pre-charge and pre-discharge circuitry.
* Embedded control and communication.
* Low-voltage power conversion.
* Programming and diagnostic interfaces.

The objective is to produce a compact electronic assembly that can be installed directly inside the battery enclosure while remaining accessible for testing, firmware development and future revisions.


<img width="1723" height="1022" alt="BMS Render" src="https://github.com/user-attachments/assets/cd61fde7-8abe-42a8-86bb-0849b05fccb6" />



## Battery-Pack Architecture

The current platform is designed around a **12S lithium-ion configuration**.

A complete battery-pack assembly consists of:

* Twelve series-connected cell groups.
* One custom battery-management board.
* A high-current charge and discharge path.
* A dedicated current-sense resistor.
* Cell-voltage and temperature-sensing connections.
* Main battery and pack-output connections.
* One or more temperature sensors.
* A mechanical cell holder or structural enclosure.
* Cell interconnects, busbars or welded nickel conductors.
* Embedded firmware for monitoring and diagnostics.

The architecture is intended to remain adaptable. While the first implementation targets a 12S pack, the design process is structured so that future variants can reuse the same development approach for different capacities, current ratings and mechanical formats.

## Development Direction

The long-term goal is to determine whether a compact custom battery-management platform can provide:

* Reliable monitoring of every series-connected cell group.
* Controlled charge and discharge switching.
* Accurate current and temperature measurements.
* Predictable fault response.
* Safe connection to capacitive loads and chargers.
* Useful embedded diagnostics.
* Practical thermal performance at elevated current.
* Repeatable PCBA and pack assembly.
* A reusable architecture for future battery systems.

The project will progressively move from schematic validation to assembled-PCB testing, controlled bench operation, pack integration and long-duration load testing.

Performance limits will be established experimentally rather than assumed from component ratings alone.

---

## Electronics Development

The electronics are divided into several functional areas:

* Battery monitoring and protection.
* High-current switching.
* Current measurement.
* Pre-charge and pre-discharge control.
* Low-voltage power conversion.
* Embedded processing and communication.
* Cell, temperature and pack connections.

The project documents the complete electronics-development process, including component selection, schematic capture, PCB layout, thermal analysis, design-for-manufacturing decisions, PCBA review, firmware development and validation.

<img width="2200" height="1700" alt="EG12S1K Schematic-1" src="https://github.com/user-attachments/assets/755445ab-d00c-49e3-9d18-6c1fecb3ade2" />

[EG12S1K Schematic.pdf](https://github.com/user-attachments/files/30072429/EG12S1K.Schematic.pdf)


---

## Battery Monitoring and Protection — BQ76952

The BQ76952 acts as the central battery-monitoring and protection device.

It measures the voltage of each series-connected cell group and provides the signals required to manage the battery’s charge and discharge paths.

The monitoring system is designed around:

* Individual cell-group voltage measurement.
* Pack-voltage supervision.
* Charge and discharge current monitoring.
* External temperature-sensor inputs.
* Overvoltage and undervoltage protection.
* Charge and discharge overcurrent detection.
* Short-circuit protection.
* Charge and discharge MOSFET control.
* Communication with the embedded controller.
* Configurable fault thresholds and recovery behavior.

The BQ76952 provides the dedicated battery-protection functions, while the microcontroller supports higher-level monitoring, communication, configuration and data handling.

Particular attention is given to the cell-input filtering network, current-sense routing, ground references, communication connections and the separation between low-level measurement circuitry and the high-current power path.

<!-- Add a close-up schematic image of the BQ76952 and cell-input network here. -->

---

## Cell-Voltage Measurement Network

Each series-connected cell group is connected to the battery monitor through a dedicated measurement and filtering network.

This section of the design must accurately measure small differences between adjacent cell nodes while operating across the full pack voltage.

The cell-monitoring network considers:

* Input resistor and capacitor selection.
* Voltage-rating margins.
* Cell-connection sequencing.
* Connector pin order.
* Noise filtering.
* Open-wire detection.
* Routing symmetry.
* Separation from switching nodes.
* Protection during assembly and troubleshooting.
* Accessibility for voltage verification.

The cell-sense wiring is treated as a precision measurement system rather than as ordinary low-current wiring.

Connector orientation, wire order and assembly documentation are especially important because an incorrect cell-tap connection can expose the monitoring circuitry to damaging voltages.

<!-- Add the cell-input schematic and connector pinout here. -->

---

## High-Current Switching Path

The battery is connected to the external pack terminals through controlled power MOSFETs.

The switching architecture allows the monitoring system to interrupt charging, discharging or both when an unsafe operating condition is detected.

The high-current path is designed around:

* Low-resistance power MOSFETs.
* Independent charge and discharge control.
* Bidirectional current flow during normal operation.
* Controlled fault isolation.
* Low conduction losses.
* Compact source and drain connections.
* Appropriate gate resistors and protection components.
* Short, wide copper paths.
* Thermal spreading around the MOSFET packages.
* Mechanical integration with the battery and output conductors.

The MOSFET current rating alone does not define the practical pack rating. The final current capability depends on MOSFET conduction losses, copper resistance, connector resistance, PCB geometry, ambient temperature, enclosure airflow and the available thermal path.

<!-- Add the charge and discharge MOSFET schematic here. -->

<!-- Add a close-up image of the MOSFET PCB layout and drain-to-drain copper region here. -->

---

## Current Measurement — Low-Side Shunt

Pack current is measured using a precision low-resistance shunt installed in the main negative current path.

The voltage developed across the shunt is measured by the battery-monitoring device and used for protection, current reporting and accumulated charge calculations.

The current-sense design focuses on:

* Appropriate resistance for the target current range.
* Power dissipation during continuous operation.
* Short-duration overload capability.
* Kelvin sensing.
* Symmetrical sense routing.
* Separation between measurement traces and load-current copper.
* Temperature coefficient.
* Measurement accuracy.
* Mechanical and solder-joint reliability.
* Clear distinction between the cell-negative and pack-negative reference nodes.

Kelvin connections are routed directly from the shunt terminals to the current-sense inputs so that voltage drops in the surrounding high-current copper do not become part of the measurement.

<!-- Add the current-shunt schematic and PCB layout here. -->

---

## Pre-Charge and Pre-Discharge Circuits

Controlled pre-charge and pre-discharge paths are included to limit inrush current when the battery is connected to external equipment.

A capacitive load can initially appear close to a short circuit. Connecting it directly through the main MOSFETs can create a large current transient, connector arcing and unnecessary stress on the power path.

The pre-charge path allows the external load capacitance to charge through a current-limiting resistor before the main discharge MOSFET is enabled.

The pre-discharge or charger-detection path can provide similar controlled behavior when connecting the pack to charging equipment or when managing voltage differences across the switching stage.

The design considers:

* Initial inrush current.
* External load capacitance.
* Resistor pulse energy.
* Pre-charge duration.
* Acceptable voltage difference before main connection.
* MOSFET safe operating area.
* Resistor package size.
* Repeated connection cycles.
* Firmware-controlled timing.
* Fault detection if the external voltage does not rise as expected.

The resistors are selected according to pulse-energy capability and transient thermal behavior, not only their continuous power rating.

<!-- Add the pre-charge and pre-discharge schematic here. -->

---

## Embedded Controller — ESP32-C6

An ESP32-C6 module provides the higher-level embedded control and communication functions.

The microcontroller does not replace the dedicated hardware protections of the BQ76952. Instead, it adds configuration, reporting, diagnostics and application-level behavior.

The embedded controller can manage:

* Communication with the battery-monitoring device.
* Pack-voltage and individual-cell reporting.
* Current and temperature reporting.
* State-of-charge estimation.
* Fault logging.
* Operating-history storage.
* Pre-charge sequencing.
* Charger and load detection.
* USB programming and diagnostics.
* Wireless communication.
* Future web-based monitoring.
* Firmware updates and system configuration.

The ESP32-C6 was selected as a flexible development platform with sufficient processing capability, communication interfaces and software support for continued experimentation.

Selected signals are exposed through test points or headers to simplify firmware development, oscilloscope measurements and hardware troubleshooting.

<!-- Add the ESP32-C6 schematic section here. -->

---

## Low-Voltage Power Supply — LMR38020

The embedded electronics require a regulated low-voltage supply derived from the battery pack.

An LMR38020 step-down converter generates the logic supply used by the ESP32-C6 and supporting circuitry.

The regulator design focuses on:

* Operation across the complete battery-voltage range.
* Conversion to a stable low-voltage rail.
* Low standby consumption.
* Sufficient transient response for wireless activity.
* Input-voltage margin.
* Inductor current capability.
* Input and output capacitor selection.
* Compact switching-loop geometry.
* Controlled startup behavior.
* Separation from sensitive analog measurements.

Because the converter operates directly from the battery pack, component voltage ratings and switching-node layout are especially important.

The high-frequency current loops are kept short, and the feedback network is routed away from the switching node, MOSFET gates and current-sense traces.

<!-- Add the LMR38020 schematic and PCB layout here. -->

---

## USB Programming and Diagnostics

A USB-C connection provides a convenient interface for firmware programming, serial diagnostics and communication with the embedded controller.

The interface is designed so that its ground reference matches the low-voltage electronics and battery-monitoring system.

The USB section considers:

* Direct communication with the ESP32-C6.
* Electrostatic-discharge protection.
* Series resistors on the data lines.
* Correct USB-C configuration resistors.
* Connector shielding and grounding.
* Prevention of unwanted backfeeding.
* Clear behavior when USB and battery power are both present.
* Programming while the main high-current output is disabled.
* Accessibility after the PCB is installed inside the enclosure.

The USB interface is intended primarily for development and diagnostics. Its final accessibility and isolation requirements will depend on the mechanical pack design and intended use environment.

<!-- Add the USB-C schematic and connector-layout image here. -->

---

## Temperature Monitoring

Temperature measurement is required to evaluate both cell conditions and electronic-component heating.

The battery-monitoring device supports external thermistors placed near important thermal regions.

Possible measurement locations include:

* The center of the cell assembly.
* Cell groups with limited airflow.
* The main charge and discharge MOSFETs.
* The current-sense resistor.
* The pre-charge resistor.
* The low-voltage power supply.
* External pack terminals or busbars.

Temperature information can be used to limit charging, limit discharging, open the protection MOSFETs or log abnormal thermal behavior.

Sensor placement will be refined through practical testing because the hottest electrical component or cell group may not be obvious from the schematic alone.

<!-- Add the thermistor-input schematic and sensor-placement diagram here. -->

---

## Connector Selection and Pack Modularity

Connector selection is a critical part of the battery-pack architecture.

Different connections have very different electrical and mechanical requirements. The main output terminals must carry significant current, while cell-sense and temperature connectors must prioritize reliability, pin ordering and resistance to accidental disconnection.

Connector decisions consider:

* Continuous and peak current ratings.
* Maximum pack voltage.
* Contact resistance.
* Mechanical retention.
* Polarization and keying.
* Touch protection.
* Cable and crimp availability.
* Assembly tooling.
* Vibration resistance.
* Serviceability.
* PCB footprint size.
* Repeated connection cycles.
* Prevention of incorrect cell-tap sequencing.
* Compatibility with professional cable-harness assembly.

High-current connectors are evaluated as part of the complete thermal path because contact resistance can produce significant local heating.

<!-- Add images of the main battery, pack-output, cell-tap and temperature connectors here. -->

---

## High-Current PCB Design

The PCB must carry the full pack current while also supporting sensitive voltage and current measurements.

The high-current layout is designed around:

* Wide copper pours.
* Short current paths.
* Minimal neck-down regions.
* Copper on multiple layers where practical.
* Via arrays between current-carrying layers.
* Large solderable cable-termination areas.
* Controlled current flow through the shunt.
* Low-resistance MOSFET interconnection.
* Separation from precision analog traces.
* Mechanical support for heavy wires and connectors.
* Predictable heat spreading.
* Accessibility for current and voltage measurements.

The copper layout is evaluated as part of the electrical circuit. Trace geometry, layer transitions, solder thickness, MOSFET pads and connector joints all contribute to resistance and heat generation.

Particular attention is given to the drain-to-drain connection between the main MOSFETs because it carries the complete pack current and can become a concentrated thermal region.

<!-- Add a high-resolution image of the high-current PCB layers here. -->

---

## Thermal Design

Thermal performance is one of the main factors that determines the practical current rating of the battery-management board.

Heat can be generated by:

* MOSFET conduction losses.
* Current-shunt losses.
* PCB copper resistance.
* Connector contact resistance.
* Cable terminations.
* Pre-charge resistor pulses.
* Low-voltage power conversion.
* Cell internal resistance.
* Imbalance between parallel cell connections.

The thermal design considers:

* MOSFET junction-to-board thermal paths.
* Copper spreading around power packages.
* Internal copper-plane participation.
* Thermal vias.
* PCB thickness and copper weight.
* Enclosure airflow.
* Conduction into cables, busbars or mechanical structures.
* Temperature-sensor placement.
* Maximum ambient temperature.
* Continuous versus intermittent current.
* Thermal accumulation during charging and discharging.

The design current will be validated under realistic enclosure conditions. Open-air bench measurements alone will not be treated as sufficient proof of continuous pack capability.

<!-- Add thermal-camera images or temperature plots here after testing. -->

---

## Cell Assembly and Interconnection

The battery-management electronics form only one part of the completed battery pack.

Cell selection and interconnection directly affect current sharing, voltage balance, thermal behavior and long-term reliability.

The pack assembly considers:

* Cell chemistry and manufacturer specifications.
* Series and parallel configuration.
* Cell matching.
* Spot-welded nickel or copper interconnects.
* Busbar resistance.
* Parallel-group current sharing.
* Insulating rings and barriers.
* Fish-paper and enclosure insulation.
* Strain relief.
* Fuse-wire or cell-level protection options.
* Mechanical compression and vibration.
* Clearance from sharp conductive edges.
* Routing of cell-sense wiring.
* Pack serviceability.

The cell interconnection will be documented with the same level of detail as the PCB because the finished battery is a complete electromechanical system.

<!-- Add the cell-group layout, welded interconnects and mechanical assembly images here. -->

---

## Safety and Fault Management

A battery-management system reduces risk, but it does not make a battery pack inherently safe on its own.

The complete system must combine suitable cells, electrical protection, thermal design, mechanical protection, correct assembly and controlled validation.

Fault-management development includes:

* Cell overvoltage.
* Cell undervoltage.
* Charge overcurrent.
* Discharge overcurrent.
* Short-circuit current.
* Excessive charging temperature.
* Excessive discharging temperature.
* MOSFET overheating.
* Open thermistor connections.
* Open or miswired cell-sense connections.
* Charger connection faults.
* Pre-charge timeout.
* Communication loss.
* Unexpected reset or firmware failure.
* Reverse or incorrect external connection.

Hardware protection thresholds are configured independently from user-interface or wireless functions so that the essential protection system does not rely solely on application firmware.

The prototype platform is intended for controlled engineering development and will require complete validation before being considered for product use.

---

## Mechanical Integration

The battery-management board must fit within the battery enclosure without compromising insulation, cooling or serviceability.

Mechanical integration considers:

* PCB mounting points.
* Clearance from cells and conductive busbars.
* Insulating barriers.
* Cable bend radius.
* Connector accessibility.
* USB and test-point accessibility.
* Protection from vibration.
* Strain relief for high-current wiring.
* Enclosure ventilation.
* Heat transfer to the enclosure.
* Assembly sequence.
* Disassembly and service procedures.
* Protection against accidental tool contact.

The enclosure is treated as part of the electrical and thermal design rather than as a separate cosmetic component.

<!-- Add the enclosure model, internal arrangement and exploded assembly here. -->

---

## Design for Manufacturing

The battery-management PCB is developed with manufacturing constraints considered from the beginning of the design process.

Design-for-manufacturing work includes:

* Standardized component packages where practical.
* Component availability and sourcing risk.
* Pick-and-place compatibility.
* Appropriate courtyard and assembly clearances.
* Manufacturer-supported trace, spacing, drill and via dimensions.
* Solder-mask and paste-mask design.
* Exposed-pad assembly requirements.
* High-current solder-joint design.
* Test-point accessibility.
* Connector mechanical support.
* Consistent component orientation.
* Panelization and board-edge constraints.
* Clear polarity and cell-order markings.
* Revision identification.
* Manufacturing part numbers.
* Assembly notes and inspection points.

Special attention is given to components that may require manual installation, including high-current connectors, large resistors, busbars, cables and unsupported mechanical parts.

These decisions are intended to reduce assembly risk, improve repeatability and make future revisions easier to manufacture at larger quantities.

---

## PCBA and Prototype Manufacturing

Prototype boards are fabricated and assembled using professional PCB and PCBA services where practical.

The manufacturing process includes:

1. Schematic verification and electrical-rule checking.
2. PCB layout and design-rule checking.
3. Review of high-voltage and high-current clearances.
4. Generation of Gerber, drill and fabrication files.
5. Preparation of the bill of materials.
6. Generation of component-placement files.
7. Manufacturer design-for-manufacturing review.
8. PCB fabrication.
9. Automated component assembly.
10. Visual inspection.
11. Manual assembly of high-current or unsupported components.
12. Resistance and continuity checks before power is applied.
13. Firmware programming.
14. Controlled low-voltage functional testing.
15. Integration with a current-limited battery or cell simulator.
16. Final installation into the battery pack.

Using a PCBA service allows the project to evaluate production-oriented component selection, assembly tolerances and manufacturing documentation while still operating at prototype quantities.

<!-- Add PCB fabrication and assembled-board images here. -->

---

## Bring-Up and Validation

Each hardware revision will be tested progressively before it is connected to a complete battery pack.

Initial validation will use current-limited equipment, simulated cell voltages or a controlled battery source wherever practical.

Testing will include:

* Visual inspection.
* Resistance checks before power-up.
* Verification of the low-voltage supply.
* USB programming and communication.
* BQ76952 communication.
* Individual cell-voltage accuracy.
* Pack-voltage measurement.
* Current-sense offset and calibration.
* Temperature-sensor verification.
* Charge-MOSFET operation.
* Discharge-MOSFET operation.
* Pre-charge and pre-discharge sequencing.
* Overvoltage and undervoltage response.
* Charge and discharge overcurrent response.
* Short-circuit protection behavior.
* Communication-loss behavior.
* Sleep and standby current.
* MOSFET conduction losses.
* Shunt-resistor heating.
* Connector and cable heating.
* PCB temperature distribution.
* Continuous-current testing.
* Transient-load testing.
* Charger compatibility.
* Long-duration cycling.

The validation sequence will move from low-energy tests toward higher-energy operation only after the earlier stages have been completed successfully.

<!-- Add oscilloscope captures, thermal measurements and validation tables here. -->

---

## Firmware and Data Logging

Firmware will provide a structured interface between the battery-monitoring hardware and the user.

Planned firmware functions include:

* Battery-monitor configuration.
* Cell-voltage reporting.
* Pack-voltage and current reporting.
* Temperature reporting.
* Fault and warning messages.
* State-of-charge estimation.
* Charge and discharge status.
* Pre-charge control.
* Event logging.
* Operating-time counters.
* Maximum and minimum recorded values.
* USB diagnostics.
* Wireless monitoring.
* Configuration storage.
* Firmware version reporting.
* Hardware-revision compatibility checks.

The firmware will distinguish between raw measurements, warning conditions and protection events so that the behavior of the pack can be understood during testing.

Logged data will be used to compare calculated losses with real operating temperatures and to guide future hardware revisions.

---

## Revision Control and Documentation

Each hardware revision will receive a unique project identifier, schematic revision, PCB revision and firmware compatibility record.

Documentation will include:

* System block diagrams.
* Electrical schematics.
* PCB renders.
* PCB layer images.
* Bills of materials.
* Manufacturing files.
* Connector pinouts.
* Cell-assembly drawings.
* Firmware releases.
* Configuration files.
* Bring-up procedures.
* Test results.
* Known limitations.
* Changes between revisions.

The current 12S, approximately 1 kW-class design establishes the first reference platform for the Battery-Pack-Modules project.

Future revisions may modify the cell configuration, current rating, mechanical format or communication features while preserving a consistent documentation and part-numbering structure.

---

## Project Status

Battery-Pack-Modules is currently an engineering-development platform.

The schematic, PCB, firmware, cell assembly and test procedures will continue to evolve as the design is manufactured and validated.

Published ratings will remain provisional until they are supported by electrical measurements, thermal testing and long-duration operation in the completed enclosure.

The results of each revision will be documented and used to guide the next schematic, PCB, firmware and mechanical iteration.
