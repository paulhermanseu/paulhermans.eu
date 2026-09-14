---
layout: default
title: Configuring JK BMS
date: 2026-09-14
categories: Victron
---

# Configuring JK BMS (for LFP Battery Cells)

The default settings on a JK Inverter BMS (JK-PB Series) are not good for connecting to your Victron Inverter / Charger.

You will run into errors like: "High cell voltage alarm".

Note: These settings are for LiFePO4 (LFP) battery cells.

## Basic Settings

| Name                        | Description                                                                       | Default Value | Suggested Value                         |
| --------------------------- | --------------------------------------------------------------------------------- | ------------- | --------------------------------------- |
| Cell Count                  | Number of cells connected in series                                               | 16            | **Your actual cell count**                                        |
| Battery Capacity (Ah)       | Nominal battery capacity used by the BMS for SOC calculation                      | 100           | **Your actual capacity**                |
| Balance Trigger Voltage     | Minimum cell-voltage difference before balancing starts                           | 0.010 V       | 0.010 V                                 |
| Start Balance Voltage       | Cell voltage above which active balancing can start                               | 3.300 V       | **3.400 V**                                 |
| Max Balance Current         | Maximum active balancing current                                                  | 2.0 A         | 2.0 A                                   |

## Advanced Settings

| Name                        | Description                                                                       | Default Value | Suggested Value                         |
| --------------------------- | --------------------------------------------------------------------------------- | ------------- | --------------------------------------- |
| Cell OVP                    | Cell Over Voltage Protection; disconnects charging if a cell exceeds this voltage | 3.650 V       | **3.600 V**                                 |
| Voltage Cell RCV            | Requested Charge Voltage; BMS asks the charger/inverter for this voltage per cell | 3.500 V       | **3.450 V**                             |
| SOC-100% Voltage            | Cell voltage used as the threshold for resetting SOC to 100%                      | 3.475 V       | **3.449 V**                             |
| Cell OVPR                   | Voltage below which an OVP fault can recover                                      | 3.450 V       | **3.448 V**                             |
| Cell UVPR                   | Voltage above which an undervoltage fault can recover                             | 3.100 V       | **2.650 V**                             |
| SOC-0% Voltage              | Cell voltage below which SOC is reset to 0%                                       | 3.000 V       | **2.640 V**                             |
| Cell UVP                    | Cell Under Voltage Protection; disconnects load if a cell falls below this        | 2.800 V       | **2.600 V**                                 |
| Power Off Voltage           | Cell voltage at which the BMS shuts down completely                               | 2.500 V       | 2.500 V                                 |
| Voltage Cell RFV            | Requested Float Voltage after the battery reaches 100%                            | 3.400 V       | **3.350 V**                             |


| Name                        | Description                                                                       | Default Value | Suggested Value                         |
| --------------------------- | --------------------------------------------------------------------------------- | ------------- | --------------------------------------- |
| Voltage Smart Sleep         | Cell voltage associated with Smart Sleep                                          | 3.500 V       | **3.285 V**                             |
| Time Smart Sleep            | Time condition for Smart Sleep                                                    | 24 h          | 24 h                                    |
| Continued Charge Current    | Maximum continuous charging current; BMS reports ~95% of this to the charger      | 100 A         | **105 A**                               |
| Charge OCP Delay            | Time an excessive charging current is tolerated before protection activates       | 3 s           | 5 s                                     |
| Charge OCPR Time            | Time charging remains disabled after an overcurrent event                         | 60 s          | 60 s                                    |
| Continued Discharge Current | Maximum continuous discharge current; BMS reports ~95% of this to inverter        | 100 A         | **100 A**                               |
| Discharge OCP Delay         | Time an excessive discharge current is tolerated                                  | 10 s          | **300 s**                               |
| Discharge OCPR Time         | Time discharge remains disabled after overcurrent protection                      | 60 s          | 60 s                                    |
| Charge OTP                  | Over-temperature protection for charging                                          | 50 °C         | 50 °C                                   |
| Charge OTPR                 | Temperature at which charging is allowed again                                    | 45 °C         | 45 °C                                   |
| Discharge OTP               | Over-temperature protection for discharging                                       | 50 °C         | 50 °C                                   |
| Discharge OTPR              | Temperature at which discharging is allowed again                                 | 45 °C         | 45 °C                                   |
| Charge UTP                  | Under-temperature protection for charging                                         | 10 °C         | **2 °C**                                |
| Charge UTPR                 | Temperature at which charging is allowed again                                    | 12 °C         | **5 °C**                                |
| MOS OTP                     | MOSFET over-temperature protection                                                | 80 °C         | 80 °C                                   |
| MOS OTPR                    | MOSFET temperature required for recovery                                          | 70 °C         | 70 °C                                   |
| SCP Delay                   | Short-circuit protection delay                                                    | 1500 µs       | 1500 µs                                 |
| SCPR Time                   | Recovery delay after short-circuit protection                                     | 30 s          | **5 s**                                 |
| Device Address              | Address used for communication / parallel BMS configuration                       | 0             | 1                                       |
| Data Stored Period          | Interval for storing internal data                                                | 3600 s        | 864000 s                                |
| RCV Time                    | Time the BMS maintains RCV voltage before switching to float                      | 0.5 h         | **1.0 h**                               |
| RFV Time                    | Time the BMS remains at float voltage before requesting RCV again                 | 12 h          | **6.0 h**                               |
| Emergency Time              | Duration for emergency operation below UVP                                        | 30 min        | 30 min                                  |
| User Private Data           | User-defined identification text                                                  | JK-BMS        | put Userdata                            |
| User Data 2                 | Additional user-defined data                                                      | JK-BMS        | put Userdata                            |
| UART1 Protocol              | Protocol used on UART1                                                            | 0             | 0                                       |
| UART2 Protocol              | Protocol used on UART2                                                            | 0             | 1                                       |
| CAN Protocol                | CAN communication protocol                                                        | 0             | **4**                                   |
| LCD Buzzer Trigger          | Condition that activates the buzzer                                               | 1             | 1                                       |
| LCD Buzzer Trigger Value    | Value at which buzzer activates                                                   | 20            | 20                                      |
| LCD Buzzer Release Value    | Value at which buzzer stops                                                       | 25            | 25                                      |
| DRY1 Trigger                | Trigger condition for dry-contact relay 1                                         | 0             | 4                                       |
| DRY1 Trigger Value          | Trigger value for relay 1                                                         | 0             | 3600                                    |
| DRY1 Release Value          | Release value for relay 1                                                         | 0             | 3550                                    |
| DRY2 Trigger                | Trigger condition for dry-contact relay 2                                         | 0             | 0                                       |
| DRY2 Trigger Value          | Trigger value for relay 2                                                         | 0             | 45                                      |
| DRY2 Release Value          | Release value for relay 2                                                         | 0             | 40                                      |
| Con. Wire Resistance        | Continuous-wire resistance compensation                                           | 0.00 mΩ       | 0.00 mΩ                                 |


This post is under construction.

See also this website: [https://off-grid-garage.com/my-settings/](https://off-grid-garage.com/my-settings/)
