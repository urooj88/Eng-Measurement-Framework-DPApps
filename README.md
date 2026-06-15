# Energy Measurement Framework for Data-Parallel Matrix Multiplication (MXM)

**Designed and developed by Urooj Asgher**
Technological University Dublin, Ireland
ORCID: 0000-0001-9218-3307

[![Python 3](https://img.shields.io/badge/python-3+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Author](https://img.shields.io/badge/Author-Urooj%20Asgher-blue)](https://orcid.org/0000-0001-9218-3307)
[![Institution](https://img.shields.io/badge/TU%20Dublin-Ireland-green)](https://www.tudublin.ie)
[![Power Meter](https://img.shields.io/badge/Power-Omegawatt-orange)]()
[![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20macOS-lightgrey)]()

---

This repository contains the code and scripts used to measure the energy consumption of a serial matrix-multiplication (MXM) workload using the Omegawatt power-measurement tool.

This energy measurement framework was designed and developed by **Urooj Asgher** on an HPC server, using a **physical power meter** to capture real hardware-level energy readings during workload execution. The framework provides an accurate, hardware-grounded approach to energy profiling — going beyond software estimates to measure actual power draw directly from the machine.

The framework is designed so that users can run the full experiment without manually compiling or editing any files. All compilation steps are handled automatically inside the scripts.

---

##  **Repository Structure**

```
├── smxm.c                                      # Serial matrix multiplication source code
├── esmxm                                        # Compiled executable (auto-generated)
├── run_smxm.sh                                  # Script to compile and run MXM
├── run_basepower_omegawatt_var_std.py           # Script to measure baseline power
├── run_appenergy_smxm_omegawatt_stdvar.py       # Script to measure application energy
├── power_serial_mxm.txt                         # Raw power log (auto-generated)
├── Omegawatt-output.csv                         # Baseline power results
├── mxm_power.csv                                # Application power data
├── all_powerresults_omegawatt_varstd.txt        # Summary of energy results
└── README.md                                    # Documentation
```

---

##  **Requirements**

Before running the scripts, ensure your system has:

| Requirement | Details |
|---|---|
| Python | Version 3+ |
| Power Meter | Omegawatt or access to its serial device |
| Shell | Bash (Linux / macOS) |
| Compiler | GCC (used automatically inside the scripts) |

> No manual compilation is required — the shell scripts take care of it.

---

##  **How to Run the Framework**

The project provides two main measurement modes.

### **1.  Measure Baseline System Power (Idle)**
To record the idle/baseline power of the system before running any workload:
```bash
python3 run_basepower_omegawatt_var_std.py
```
This script:
*  Starts Omegawatt
*  Collects baseline power readings
*  Computes variance and standard deviation
*  Saves results into:
```
Omegawatt-output.csv
```

### **2.  Measure Energy Consumption of the MXM Application**
To measure the energy consumption of the serial matrix multiplication program:
```bash
python3 run_appenergy_smxm_omegawatt_stdvar.py
```
This script automatically:
*  Calls `run_smxm.sh`
*  Compiles and runs `smxm.c`
*  Monitors energy using Omegawatt
*  Saves results into:
```
mxm_power.csv
all_powerresults_omegawatt_varstd.txt
power_serial_mxm.txt
```
No file compilation or editing is required.

---

##  **Makefile Support**

The repository also includes a simple Makefile so users can run the main steps with short commands:

```bash
make baseline      # Measure idle/baseline power
make appenergy     # Measure MXM application energy
make run-mxm       # Only run the serial MXM program
```

---

##  **How a User Runs Everything**

After cloning the repository:
```bash
git clone https://github.com/yourusername/hpc-energy-measurement-framework.git
cd hpc-energy-measurement-framework
```
Then simply choose:

| Goal | Command |
|---|---|
| Baseline Only | `make baseline` |
| Application Energy | `make appenergy` |
| Run Program Only | `make run-mxm` |

> No manual setup, compilation, or configuration is needed.

---

##  **License**

MIT License — see [LICENSE](LICENSE) for details.
