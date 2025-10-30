<div id="top" align="center">
<h1 align="center">⚡ Automated Power Supply Test Suite<br/>Production-Grade Testing Infrastructure with QR-Code Traceability</h1>
</div>

<br />
<div align="center">
  <img src="Images/DCP48M_while_testing_11zon.jpg?raw=true" alt="Power Electronics Tester Suite" width="800" height="600">
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
  <img src="Images/ACPD_1.webp?raw=true" alt="ACPD Tester" width="600" height="400">
</div>

**Purpose:** Comprehensive testing of AC/DC power delivery topologies for universal mains compatibility.

**Test Sequence:**
- **AC Input Connection:** 230V AC mains voltage connected at primary input
- **USB-C Power Delivery:** PD voltage profiles (5V, 9V, 12V) applied via USB-C connector
- **Connector Rotation:** USB-C cable rotated 180° during testing to verify bi-directional contact integrity
- **Full-Load Testing:** All PD voltage levels tested under full-load conditions with continuous measurement
- **Status LED Monitoring:** Verifies status LED remains active throughout entire test execution
- **Voltage Stability:** Verifies output voltage regulation and frequency stability throughout test sequence
- **Isolation Verification:** Galvanic isolation validated between primary and secondary sides

**Key Metrics:** Input voltage stability, load regulation, isolation resistance, protection response time.

---

### **2️⃣ HDR20 Tester** - Multi-Output 20W Supply Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/HDR20_1.webp?raw=true" alt="HDR20 Tester Unit" width="300" height="250">
        <p><strong>Tester Unit</strong></p>
      </td>
      <td align="center">
        <img src="Images/HDR20_dut_1.webp?raw=true" alt="HDR20 Device Under Test" width="300" height="200">
        <p><strong>Device Under Test</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Advanced validation of multi-output power supplies with cross-load scenarios and thermal characterization.

**Test Sequence:**
- **AC Input Connection:** 230V AC mains voltage connected at primary input
- **Output Load Selection:** Manual slide switch selects target measurement voltage for each test cycle
- **Dual-Pin Load Connection:** Two pins contact and apply full load to the selected output
- **Multi-Voltage Testing:** All output voltages tested sequentially under full-load conditions
- **Channel Independence:** Each output voltage measured independently with precision measurement
- **Status LED Monitoring:** Verifies status LED remains active throughout entire test execution

**Key Metrics:** Per-channel accuracy (±2%), cross-regulation, thermal steady-state, cascading protection timing.

---

### **3️⃣ DCC48XX & CCCV48XX Tester** - Dual-Mode 48V Converter Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DCC48XX_CCCV48XX_1.webp?raw=true" alt="DCC48XX & CCCV48XX Tester" width="300" height="300">
        <p><strong>Tester Frontend</strong></p>
      </td>
      <td align="center">
        <img src="Images/DCC48XX_CCCV48XX_dut_1.webp?raw=true" alt="Device Under Test" width="300" height="200">
        <p><strong>Device Under Test</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Sophisticated validation of Constant Current / Constant Voltage topologies with RGB startup sequence verification and high-current operation.

**Test Sequence:**
- **Device Selection:** Display menu selects which PSU variant to test (CCCV4805, CCCV4812, CCCV4824, DCC variants)
- **Pin Contact:** When DUT is inserted, two pins automatically contact and establish connection
- **DC Power Input:** 48V DC input applied to the selected device under test
- **Voltage Measurement:** Selected output voltage measured under full-load conditions
- **RGB Startup Detection:** Monitors color sensor for RGB LED sequence indicating proper initialization
- **Status LED Monitoring:** Verifies status LED remains active throughout entire test execution
- **Full-Load Testing:** All CC/CV variants tested under full-load conditions with continuous verification

**Key Metrics:** CC/CV accuracy (±1.8%), mode transition time, thermal stability, LED indication reliability.

---

### **4️⃣ DC-PD & USB-C-3A Tester** - Power Delivery Profile Validation
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DP-PD_USB-C-3A_1.webp?raw=true" alt="DC-PD & USB-C Tester" width="300" height="250">
        <p><strong>Tester Unit</strong></p>
      </td>
      <td align="center">
        <img src="Images/USB-C-3A_dut_testing_1.webp?raw=true" alt="USB-C Testing" width="300" height="200">
        <p><strong>Active Testing</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Comprehensive testing of Power Delivery profiles and high-current USB-C implementations.

**Test Sequence:**
- **Device Selection:** Display menu selects PD voltage profile (5V, 9V, 12V) and test mode (standard PD or 3A mode)
- **USB-C Connection:** USB-C connector inserted for physical and electrical connection
- **PD Profile Testing:** Multi-voltage testing with full-load current application
- **3A Mode Testing:** Special USB-C 3A mode tested at 5V only with 3A load applied
- **Connector Rotation:** Tests rotation of connector (up/down orientation) to verify bi-directional contact and data line integrity
- **Status LED Monitoring:** Verifies status LED remains active throughout entire test execution
- **Voltage Stability:** Monitors output voltage regulation under full-load conditions for each profile

**Key Metrics:** PD accuracy (±2%), connector reliability (10k cycles) 3A current compliance.

---

### **5️⃣ DCP48M Tester** - Multi-Mode 48V Converter Advanced Characterization
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="Images/DCP48M_tester_1.webp?raw=true" alt="DCP48M Tester Setup" width="300" height="200">
        <p><strong>Tester Configuration</strong></p>
      </td>
      <td align="center">
        <img src="Images/DCP48M_while_testing_11zon.jpg?raw=true" alt="DCP48M During Testing" width="300" height="200">
        <p><strong>Testing in Progress</strong></p>
      </td>
    </tr>
  </table>
</div>

**Purpose:** Modbus-controlled scenario-based testing for advanced 48V converter characterization across multiple topologies.

**Test Sequence:**
- **Modbus Configuration:** Controller sends scenario definition via Modbus (voltage selection, current profile, duration)
- **Multi-Voltage Testing:** Sequential testing at different voltages with full-load current applied to each
- **Scenario Execution:** Predefined test scenario loaded and executed with real-time parameter adjustment
- **Load Application:** Programmable electronic load applies specified current profile matching DUT characteristics
- **Status LED Monitoring:** Verifies status LED remains active throughout entire test execution
- **Measurement Logging:** All measurements streamed to database with per-second granularity

**Key Metrics:** Modbus response time, multi-voltage accuracy (±1.8%), thermal stability, efficiency measurement, extended reliability.

---

### **6️⃣ DIG-CCCV-15W Tester** - Standalone Offline 15W Converter Validation
<div align="center">
  <img src="Images/DIG-CCCV-15W_1.webp?raw=true" alt="DIG-CCCV-15W Standalone Tester" width="600" height="400">
</div>

**Purpose:** Portable field-deployable tester for 15W CCCV converters with standalone operation without database connectivity.

**Test Sequence:**
- **Current Application:** External pin provides constant current load based on selected voltage
- **UART Communication:** UART interface for configuration during test setup and verification during test execution
- **LED Status Monitoring:** Confirms output status indicator operation during test
- **Multi-Voltage Testing:** Tests 2-3 voltage points per DUT (e.g., 10V, 24V, 60V for full characterization)
- **Standalone Results:** Test pass/fail determination made locally without database connectivity

**Key Metrics:** Standalone reliability (no network dependency), voltage accuracy (±2%), UART communication robustness.

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

#### **Benefits for End Users**

<div align="center">
  <img src="Images/DCP48M_dut_qr-code_1.webp?raw=true" alt="QR-Code Traceability Label" width="400" height="300">
</div>

- **Per-Unit Data Access:** Every customer can scan the QR-code on their purchased PSU to access the complete test report and measurement history for their specific unit
- **Lifetime Traceability:** Manufacturing date, test conditions, voltage/current profiles tested, and pass/fail status permanently linked to the physical product
- **Quality Verification:** Customers verify the exact test parameters their unit underwent before leaving the factory
- **Batch Analysis:** Production teams identify quality trends across manufacturing batches and correlate failures to specific design revisions
- **Audit Trail:** Complete operational history supports product warranty claims and regulatory compliance documentation

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

### **2️⃣ Comprehensive Traceability via QR-Code**

**Challenge:** Enable production line users to track test results via simple QR-code scanning without requiring technical knowledge.

**Solution:**
- **UUID Generation:** Unique identifier per test run (Base64 encoded for URL compatibility)
- **QR-Code Encoding:** UUID embedded in scannable QR-code label
- **Database Linking:** QR-scan retrieves complete test record including all measurements
- **Web Dashboard:** Customer-facing interface showing pass/fail status and detailed metrics
- **Historical Tracking:** All tests for a given unit linked for lifetime traceability

**Why It Matters:** Bridges gap between manufacturing and customer - every sold unit has verifiable test history.

---

### **3️⃣ Production-Ready Architecture**

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
