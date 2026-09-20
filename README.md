# Dive Computer

Open-source dive computer project designed around a rugged aluminium enclosure, a high-visibility display, pressure/depth sensing, inertial sensors, navigation features and optional surface communication.

> **Project status:** initial specification and architecture definition.

## Project goals

The objective is to design and build a compact, robust dive computer suitable for demanding recreational and technical diving, with a modular hardware and firmware architecture.

The current target maximum operating depth is **200 m**.

The design should prioritize:

- reliability and fault tolerance
- readability underwater
- low power consumption
- robust pressure-resistant mechanical construction
- modular and replaceable electronics
- open hardware / open firmware where practical
- simple underwater interaction
- extensibility for navigation and surface communication features

---

## Initial specifications

| Function | Target / current choice | Status |
|---|---|---|
| Maximum depth | **200 m** | ✅ Requirement defined |
| Display size | **2" minimum, 3" maximum** | ✅ Requirement defined |
| Display technology | **OLED preferred**, TFT if OLED is unsuitable | 🟠 To evaluate |
| Depth sensing | Pressure sensor | 🟠 Component to select |
| Temperature | Temperature measurement, preferably integrated with pressure sensing | 🟠 Component to select |
| Compass | 3-axis magnetometer / electronic compass | 🟠 Component to select |
| Motion sensing | Accelerometer, potentially IMU | 🟠 Component to select |
| User interaction | Physical controls and/or **tap-based interaction using accelerometer** | 🟠 To evaluate |
| Radio | **900 MHz LoRa transceiver** | ✅ Architecture requirement |
| GPS | Optional | 🟠 Optional subsystem |
| Charging | **Wireless / inductive charging** | ✅ Architecture requirement |
| Enclosure | **Machined aluminium** | ✅ Architecture requirement |
| Display protection | Bezel around display | ✅ Architecture requirement |
| Display window material | To be defined | 🟠 To evaluate |

---

## Functional architecture

The dive computer is expected to contain the following major subsystems:

### Processing

A low-power microcontroller will manage:

- dive calculations
- sensor acquisition
- display rendering
- user interface
- data logging
- power management
- LoRa communication
- optional GPS

The MCU has not yet been selected.

### Depth and temperature sensing

The computer will include a pressure sensor suitable for operation down to at least **200 m seawater depth**.

The final sensor should provide sufficient safety margin beyond the nominal operating depth.

Temperature measurement may be provided by the pressure sensor itself or by an additional dedicated sensor.

Key parameters to evaluate:

- pressure range
- absolute accuracy
- resolution
- temperature compensation
- long-term drift
- package and PCB integration
- pressure-port design

### Display

Target diagonal:

**2" to 3"**

Preferred technology:

**OLED**

OLED is attractive because of:

- excellent contrast
- true black background
- simple high-visibility UI
- good viewing angles

However, TFT / IPS remains an alternative if it provides better:

- brightness
- lifetime
- availability
- power consumption in the intended UI
- pressure/mechanical integration

The UI is expected to use only a small number of colors.

### Compass and inertial sensing

The computer will include:

- a 3-axis compass / magnetometer
- an accelerometer
- optionally a full IMU with gyroscope

Potential accelerometer uses include:

- detecting taps on the enclosure
- wake-up gestures
- orientation detection
- UI interaction without additional penetrations through the pressure enclosure

Tap interaction will be evaluated experimentally before being adopted as a primary control method.

### LoRa radio

A **900 MHz LoRa transceiver** is planned.

Potential uses include surface communication such as:

- diver-to-boat signalling
- emergency beacon functionality
- transmission of GPS position after surfacing
- communication between compatible surface devices

Radio communication is intended primarily for use **at or above the water surface**. RF propagation underwater at these frequencies is extremely limited.

The exact radio chipset, frequency plan and antenna architecture remain to be selected.

### GPS

GPS is an optional subsystem.

Expected use cases:

- position acquisition after surfacing
- dive entry/exit position logging
- emergency beacon position transmission through LoRa

The GPS may be omitted from lower-power or smaller hardware variants.

### Power system

The computer will use an internal rechargeable battery.

Charging will be performed by **inductive / wireless charging** in order to avoid an external charging connector and reduce enclosure penetrations.

The battery chemistry, capacity and charging architecture remain to be defined.

Power-budget work will include:

- display consumption
- MCU consumption
- sensors
- LoRa transmission
- GPS
- sleep modes
- inductive charging losses

### Mechanical enclosure

The main enclosure will be machined from **aluminium**.

Current concept:

- CNC-machined aluminium body
- pressure-resistant display window
- bezel protecting and retaining the display window
- sealed construction suitable for a target depth of 200 m
- minimal number of enclosure penetrations

Items still to define:

- aluminium alloy
- anodizing / surface treatment
- enclosure geometry
- wall thickness
- sealing architecture
- O-ring dimensions and materials
- display-window material
- window thickness
- bezel geometry and retention
- button / control implementation

### Display window

The material has not yet been selected.

Candidate materials to investigate include:

- sapphire crystal
- mineral / chemically strengthened glass
- acrylic
- polycarbonate

The final choice will depend on:

- pressure resistance
- scratch resistance
- impact resistance
- optical quality
- manufacturability
- sealing method
- thickness
- cost

---

## User interface concept

The interface should remain usable while wearing diving gloves and under poor visibility.

Possible interaction methods:

- mechanical buttons
- magnetic buttons
- accelerometer-based taps
- combinations of the above

The accelerometer may allow some actions without adding additional mechanical penetrations through the enclosure.

Safety-critical functions should not depend on an interaction method that can be triggered accidentally.

---

## Preliminary subsystem breakdown

```text
Dive Computer
│
├── Main controller
│
├── Display
│   └── 2–3" OLED / TFT
│
├── Sensors
│   ├── Pressure
│   ├── Temperature
│   ├── Magnetometer
│   └── Accelerometer / IMU
│
├── Communication
│   ├── 900 MHz LoRa
│   └── GPS (optional)
│
├── Power
│   ├── Rechargeable battery
│   ├── Power management
│   └── Inductive charging
│
└── Mechanical
    ├── CNC aluminium enclosure
    ├── Display window
    ├── Bezel
    ├── Seals
    └── User controls
```

---

## Development status

Legend:

- ✅ requirement / choice defined
- 🟠 under evaluation / needs validation
- ❌ rejected or not working

### Current status

- ✅ Maximum operating depth target: 200 m
- ✅ Aluminium enclosure concept
- ✅ 2–3" display requirement
- 🟠 OLED vs TFT evaluation
- 🟠 Display window material selection
- 🟠 Pressure / temperature sensor selection
- 🟠 Compass selection
- 🟠 Accelerometer / IMU selection
- 🟠 Tap-based user interface validation
- ✅ 900 MHz LoRa requirement
- 🟠 LoRa chipset and antenna selection
- 🟠 Optional GPS architecture
- ✅ Inductive charging concept
- 🟠 Battery sizing and power budget
- 🟠 Pressure enclosure calculations and testing
- 🟠 Dive algorithm and firmware architecture

---

## Next design steps

The project will initially be developed subsystem by subsystem.

Priority studies are:

1. system architecture and power budget
2. display technology and display-window design
3. pressure / temperature sensor
4. MCU and main electronics
5. battery and inductive charging
6. compass and IMU
7. LoRa and optional GPS
8. aluminium enclosure and sealing
9. user controls
10. firmware architecture and decompression algorithms
11. prototype pressure testing and validation

---

## Safety notice

This project is experimental.

A dive computer is safety-critical equipment. Any prototype must be independently validated, pressure tested and extensively compared against established instrumentation before it can be considered suitable for real diving use.

Do not rely on an unvalidated prototype as the sole source of depth, decompression or life-support-related information.
