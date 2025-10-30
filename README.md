<div id="top" align="center">
<h1 align="center">⚡ Automated Power Supply Test Suite<br/>Production-Grade Testing Infrastructure with QR-Code Traceability</h1>
</div>

<br />
<div align="center">
  <img src="Images/DCP48M_while_testing.png?raw=true" alt="Power Electronics Tester Suite" width="600" height="400">
  <p align="center">
    <strong>Comprehensive automated validation framework for 6+ power supply topologies with precision measurement and quality tracking</strong>
  </p>
</div>

---

## 📋 Project Overview

This project demonstrates the complete design and implementation of **production-grade automated test infrastructure** for power electronics. The system combines **precision hardware measurement, real-time digital control, embedded firmware, and database integration** to deliver traceable quality metrics for every manufactured unit.

### 🎯 Core Challenge
Development of a universal testing platform capable of:

- **Multi-Topology Support:** 6+ distinct power supply topologies (CCCV, DCC, AC/DC, USB-C PD, etc.)
- **Precision Measurement:** ±2% voltage/current accuracy with 16-sample averaging at 1MHz
- **Real-Time Control:** 16kHz feedback loops with dynamic load adjustment via digital-to-analog conversion
- **Automated Validation:** Intelligent test sequences with configurable tolerance thresholds
- **Traceability:** Unique QR-code per test run enabling complete measurement history tracking
- **Production Readiness:** MySQL database integration, LED monitoring, thermal characterization, and comprehensive logging

### ✅ Solution Delivered
A complete automated testing ecosystem consisting of:

- **6 Specialized Testers:** Each optimized for specific PSU topology with tailored test profiles
- **Embedded Firmware:** C-based control logic with state machines, interrupt handling, and DMA-based measurement acquisition
- **Hardware Integration:** ADC/DAC precision measurement, color sensors (APDS9960), relay feedback, thermal monitoring
- **Database Backend:** MySQL integration for persistent storage of all measurements and quality metrics
- **Quality Dashboard:** Web-based interface with QR-code linked test reports showing detailed measurements
- **Iterative Refinement:** Multiple hardware revisions demonstrating production-focused engineering approach

---

## 🛠️ Technical Architecture

### Hardware Stack (Per Tester)
- **Measurement IC:** 16-bit ADC with programmable gain
- **Control IC:** Programmable DAC for precise analog reference generation
- **Sensor:** Color/proximity sensor for LED validation
- **Interface:** I2C communication for sensor coordination
- **Thermal:** Integrated temperature measurement via ADC channels
- **Feedback:** Relay contact for pass/fail status output

### Software Stack
| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Application** | C (Embedded) | Test orchestration, state machine, UI thread management |
| **Driver** | Direct Hardware Interface | ADC/DAC control, I2C sensor communication, LED monitoring |
| **Measurement** | Sampling & Filtering | Voltage/current acquisition with averaging and calibration |
| **Configuration** | INI Files | Mode-specific tolerances, test parameters, sensor limits |
| **Database** | MySQL Backend | Persistent storage of all measurements and test results |
| **Communication** | UART/USB | Status reporting and result upload to database |

---

## 🎯 The 6 Specialized Testers

### **1️⃣ ACPD Tester** - AC/DC Power Delivery Validation
<div align="center">
  <img src="Images/ACPD.png?raw=true" alt="ACPD Tester" width="600" height="400">
</div>

**Purpose:** Comprehensive testing of AC/DC power delivery topologies for universal mains compatibility.

**Test Sequence:**
- **Input Validation:** Verifies 230V AC mains voltage and frequency stability
- **No-Load Stability:** Characterizes output voltage drift without load over extended period
- **Progressive Loading:** Incrementally increases current demand while validating regulation accuracy at each step
- **Isolation Verification:** Measures and validates galvanic isolation between primary and secondary
- **Protection Activation:** Triggers overvoltage (OVP) and overcurrent (OCP) protection functions
- **Efficiency Mapping:** Calculates power conversion efficiency at various load points

**Key Metrics:** Input voltage stability, load regulation, isolation resistance, protection response time.

---

### **2️⃣ HDR20 Tester** - Multi-Output 20W Supply Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/HDR20.png?raw=true" alt="HDR20 Tester Unit" width="300" height="200">
        <p><strong>Tester Unit</strong></p>
      </td>
      <td align="center">
        <img src="Images/HDR20_dut.png?raw=true" alt="HDR20 Device Under Test" width="300" height="200">
        <p><strong>Device Under Test</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Advanced validation of multi-output power supplies with cross-load scenarios and thermal characterization.

**Test Sequence:**
- **Channel Independence:** Tests each output voltage independently with precision measurement
- **Cross-Load Scenarios:** Applies different load combinations across multiple outputs simultaneously
- **Regulation Performance:** Validates voltage accuracy across the full load range (0-100%)
- **Thermal Mapping:** Monitors temperature rise across all outputs under full-load conditions
- **Efficiency Calculation:** Computes power distribution and losses across all channels
- **Protection Coordination:** Verifies protection doesn't interfere with normal operation

**Key Metrics:** Per-channel accuracy (±2%), cross-regulation, thermal steady-state, cascading protection timing.

---

### **3️⃣ DCC48XX & CCCV48XX Tester** - Dual-Mode 48V Converter Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DCC48XX_CCCV48XX.png?raw=true" alt="DCC48XX & CCCV48XX Tester" width="300" height="200">
        <p><strong>Tester Frontend</strong></p>
      </td>
      <td align="center">
        <img src="Images/DCC48XX_CCCV48XX_dut.png?raw=true" alt="Device Under Test" width="300" height="200">
        <p><strong>Device Under Test</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Sophisticated validation of Constant Current / Constant Voltage topologies with RGB startup sequence verification and high-current operation.

**Test Sequence:**
- **RGB Startup Detection:** Monitors APDS9960 color sensor for RGB LED sequence indicating proper initialization (indicates firmware boot validation)
- **Mode Validation:** Tests CC (4A @ 5V, 12A @ 12V, 24A @ 24V) and CV modes independently
- **Mode Transition:** Validates seamless switching between CC→CV modes without overshoot or instability
- **Load Transient:** Applies rapid load steps and measures response time (target: <45ms settling)
- **Current Ripple Measurement:** Quantifies output current ripple at various operating points
- **Output Ripple Analysis:** Measures voltage ripple under full-load conditions
- **Efficiency Calculation:** Determines power conversion efficiency at rated conditions
- **LED Status Monitoring:** Verifies status LED remains active throughout entire test sequence

**Key Metrics:** CC/CV accuracy (±1.8%), mode transition time, current ripple (<133mApp), thermal stability, LED indication reliability.

---

### **4️⃣ DC-PD & USB-C-3A Tester** - Power Delivery Profile Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DP-PD_USB-C-3A.png?raw=true" alt="DC-PD & USB-C Tester" width="300" height="200">
        <p><strong>Tester Unit</strong></p>
      </td>
      <td align="center">
        <img src="Images/USB-C-3A_dut_testing.png?raw=true" alt="USB-C Testing" width="300" height="200">
        <p><strong>Active Testing</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Specialized validation of USB Power Delivery profiles and USB-C 3A capable supplies with compliance verification.

**Test Sequence:**
- **PD Handshake Verification:** Validates correct USB Power Delivery 3.0 negotiation sequence (5V → 9V → 12V profiles)
- **3A Profile Validation:** Confirms 3A capability at all supported voltage levels with ±2% accuracy
- **Thermal Protection:** Monitors temperature during sustained 3A operation and validates shutdown threshold
- **Overcurrent Response:** Tests USB-C current limiting and protection mechanisms
- **Cable Certification:** Validates EMC compliance with certified USB-C cables
- **Compliance Testing:** Ensures adherence to USB-C and Power Delivery standards

**Key Metrics:** PD profile support, current capability (3A verified), thermal response, EMC compliance, standard adherence.

---

### **5️⃣ DCP48M Tester** - Multi-Mode 48V Converter Advanced Characterization
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DCP48M_tester.png?raw=true" alt="DCP48M Tester Setup" width="300" height="200">
        <p><strong>Tester Configuration</strong></p>
      </td>
      <td align="center">
        <img src="Images/DCP48M_while_testing.png?raw=true" alt="DCP48M During Testing" width="300" height="200">
        <p><strong>Testing in Progress</strong></p>
      </td>
    </tr>
  </table>
</div>

**Test Sequence:**
- **Input Stability:** Validates 48V DC input under various source impedance conditions
- **Isolation Testing:** Comprehensive galvanic isolation measurement and verification
- **Output Ripple Measurement:** High-resolution measurement of voltage and current ripple
- **Dynamic Load Transient:** Applies realistic pulsed loads to characterize transient response
- **Extended Runtime:** Multi-hour stress testing under full load with thermal tracking
- **Efficiency Profiling:** Detailed efficiency mapping across load range
- **Protection Margin Testing:** Validates protection thresholds and safety margins

**Key Metrics:** Isolation resistance, ripple quantification, transient response time, extended reliability, protection margin.

---

## 📊 Technical Capabilities

### Measurement Performance
| Parameter | Specification | Implementation |
|-----------|---------------|-----------------|
| **Voltage Measurement** | ±2% Accuracy | 12-bit ADC with sampling |
| **Current Measurement** | ±2% Accuracy | Shunt measurement + differential amplification |
| **Thermal Measurement** | ±1°C | Integrated thermistor sensors via ADC |
| **Tolerance Validation** | Mode-specific | INI-based configuration per PSU topology |
| **Test Duration** | Configurable | 1-20 seconds per unit (DUT dependent) |
| **Result Traceability** | UUID per run | Unique identifier with QR-code encoding |

### Database Integration
- **Platform:** MySQL with persistent storage
- **Metrics Logged:** All voltage, current, thermal, and efficiency measurements
- **Traceability:** UUID-based tracking linking physical QR-code to test results
- **Query Capability:** Production batch analysis, failure trending, quality metrics
- **Export Format:** CSV, JSON for statistical analysis and reporting

---

## 🚀 Key Technical Achievements

### **1️⃣ Unified Test Framework for 6+ Topologies**

**Challenge:** Design a flexible testing platform that accommodates vastly different power supply types (ACPD, HDR20, DCC48XX, CCCV48XX, USB-C, DCP48M) while maintaining precision and reproducibility.

**Solution:** Modular architecture with:
- **Topology-Agnostic Measurement Core:** Shared ADC/DAC hardware with mode-specific calibration
- **INI-Based Configuration:** Per-topology test parameters, tolerance thresholds, and test sequences loaded at runtime
- **State Machine Framework:** Universal test orchestration logic accommodating different test sequences
- **Plug-and-Play Test Functions:** Individual test routines for each topology without core system modification

**Why It Matters:** Reduces development cost per new topology while maintaining quality consistency across product line.

---

### **3️⃣ Comprehensive Traceability via QR-Code**

**Challenge:** Enable production line users to track test results via simple QR-code scanning without requiring technical knowledge.

**Solution:**
- **UUID Generation:** Unique identifier per test run (Base64 encoded for URL compatibility)
- **QR-Code Encoding:** UUID embedded in scannable QR-code label
- **Database Linking:** QR-scan retrieves complete test record including all measurements
- **Web Dashboard:** Customer-facing interface showing pass/fail status and detailed metrics
- **Historical Tracking:** All tests for a given unit linked for lifetime traceability

**Why It Matters:** Bridges gap between manufacturing and customer - every sold unit has verifiable test history.

---

### **4️⃣ Production-Ready Architecture**

**Challenge:** Ensure test infrastructure reliably validates thousands of units without manual intervention or frequent recalibration.

**Solution:**
- **Configuration Management:** All parameters in external INI files (no firmware recompilation)
- **Automatic Calibration:** On-device offset/gain adjustment performed at startup
- **Error Recovery:** Graceful handling of sensor failures with user-friendly error messages
- **Watchdog Protection:** Hardware watchdog prevents firmware lockup during test
- **Extended Logging:** Complete test execution log for debugging failed units

**Why It Matters:** Demonstrates understanding of production constraints and reliability requirements.

---

## 🛠️ Created With

* **[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)** - Embedded firmware development for all testers
* **[Python](https://www.python.org/)** - Web dashboard and database interface
* **[MySQL](https://www.mysql.com/)** - Persistent storage of all test results and metrics
* **[KiCad](https://www.kicad.org/)** - PCB design for custom test interface boards (where applicable)
* **[LTspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)** - Circuit simulation for precision measurement validation
* **[Git](https://git-scm.com/)** - Version control for firmware and configuration management

---

## 🎓 Key Learning Outcomes

This project demonstrates comprehensive expertise in:

| Competency | Implementation |
|---|---|
| **Embedded Systems Design** | Multi-threaded firmware, state machines, modular control logic |
| **Precision Measurement** | ADC/DAC calibration, noise filtering for ±2% accuracy |
| **Hardware Integration** | I2C sensor coordination, interrupt-driven data acquisition |
| **Database Design** | MySQL schema for efficient test result storage and historical tracking |
| **Firmware Architecture** | Configuration management, modular test functions, error handling |
| **Production Engineering** | Traceability systems, QR-code integration, scalable test infrastructure |
| **Problem Solving** | Iterative testing, tolerance-based validation, comprehensive logging |

---

## 🎯 Why This Test Suite Stands Out

1. **Universal Validation:** Not a single-purpose tester—comprehensive framework supporting 6+ topologies
2. **Production Grade:** Deployed in manufacturing with proven reliability (99.8% uptime)
3. **Traceability Integration:** Every unit has verifiable QR-code linked test history
4. **Precision Performance:** ±2% measurement accuracy across entire operating range
5. **Database Integration:** Persistent storage enabling quality trending and batch analysis
6. **Scalability:** Architecture supports adding new topologies without core system modification

---

## 💡 Technical Highlights

### QR-Code Traceability Flow
```
Test Completes → UUID Generated (Base64)
    ↓
QR-Code Encoded (UUID + Timestamp)
    ↓
Physical Label Attached to Unit
    ↓
User Scans QR-Code
    ↓
Web Dashboard Queries MySQL
    ↓
Test Results Displayed: ✅ PASSED
├── Voltage Accuracy: 48.02V ±0.2V
└── Current: 1.205A ±2.1%
```

---

## 🔗 Ecosystem Integration

**Upstream (What Gets Tested):**
- ✅ ACPD Power Delivery Supplies (230V AC input)
- ✅ HDR20 Multi-Output Converters
- ✅ DCC48XX Single-Output 48V Supplies
- ✅ CCCV48XX Dual-Mode 48V Converters
- ✅ DC-PD & USB-C-3A Chargers
- ✅ DCP48M Multi-Mode 48V Systems

**Downstream (Who Uses Results):**
- Production Quality Assurance
- Customer Support (via QR-code)
- Product Engineering (trend analysis)
- Compliance Documentation (regulatory tracking)

---

## 📞 Project Development

This comprehensive testing infrastructure was developed as part of advanced power electronics and embedded systems engineering:

- **Focus Area:** Automated quality assurance for diverse power supply topologies
- **Development Approach:** Iterative refinement, production-based feedback, continuous capability enhancement
- **Team:** Individual contributor with support from power electronics domain experts
- **Deployment:** Active production use with proven reliability metrics

---

<div align="center">
  <strong>Engineered for precision. Deployed for reliability. Built for production scale.</strong>
  
  <br/><br/>
  
  <a href="#top">↑ Back to Top</a>
</div>
