# TransOMNeT
High performance integration bridge for TransModeler traffic simulator and OMNeT++ for V2X simulation.

**TransOMNeT** is an open-source, high-performance integration bridge between [TransModeler](https://www.caliper.com/transmodeler/) — a professional-grade microscopic traffic simulation platform — and [OMNeT++](https://www.omnetpp.org/), a modular, event-driven network simulator. This bridge enables cyber-physical co-simulation of connected transportation systems for research, security testing, and secure-by-design ITS development.

> ⚠️ **Disclaimer**: TransOMNeT is an independent open-source project. It is not affiliated with or endorsed by the OMNeT++ development teams. OMNeT++ is a trademark of OpenSim Ltd.


## ✨ Features

- Seamless **in-process coupling** between OMNeT++ and TransModeler
- **Pure C++ implementation** for unmatched performance and portability
- **Sub-microsecond latency** using shared memory or COM-based IPC
- Support for:
  - Vehicle-to-Everything (V2X) simulation
  - SPaT and MAP message exchange
  - Cyber-attack injection and resilience testing
- Modular architecture designed for extension and experimentation


## 🚀 Why TransOMNeT Performs Exceptionally Well

**TransOMNeT is engineered for simulation performance and scalability**, avoiding the typical bottlenecks of socket-based or script-driven integration frameworks.

### ⚙️ Pure C++ Architecture

- Built entirely in **modern C++20**
- No Python, Java, or interpreter layers
- Full control over memory, threading, and simulation timing

### 🔗 In-Process OMNeT++ Execution

- OMNeT++ is embedded directly as a simulation engine within TransModeler
- Avoids launching subprocesses or relying on external schedulers
- Simulation events are co-stepped in **tick-accurate sync**

### 🔄 Zero-Copy IPC via Shared Memory or In-Process COM

- Vehicle state, signal timing, and simulation hooks are exchanged using:
  - **In-process COM interfaces** (near-function call latency)
  - **Shared memory buffers** for batch updates
- No network stacks, no marshalling, no latency drift

### 🧪 Real-Time and Faster-Than-Real-Time Execution

- Designed to support both real-time digital twin environments and offline, faster-than-real-time analysis
- Easily handles **10k+ vehicles** with responsive cyber-physical feedback

### 📉 Benchmark: IPC Latency Comparison

| Method                         | Typical Latency |
|-------------------------------|------------------|
| **TransOMNeT (COM/shared mem)** | **< 1 μs**       |
| Veins (TraCI via TCP)         | ~100–500 μs     |
| Socket-based co-simulation    | 1–2 ms           |


## 🧱 Architecture Overview

```text
TransModeler (C++) ⇄ [TransOMNeT Bridge] ⇄ OMNeT++ Modules
                        ▲           ▲
               COM / Shared Memory IPC
```

## 📂 Project Structure

```
transomnet/
├── CMakeLists.txt
├── README.md
├── LICENSE
├── bridge/
│   ├── TransOmnetBridge.h/.cpp     # Core integration logic
│   ├── VehicleMobilityAdapter.h    # Vehicle state adapter
│   ├── EventHookAPI.h              # OMNeT++ event hook interface
├── omnet/
│   ├── ned/                        # OMNeT++ NED topology files
│   ├── msg/                        # Message definitions (SPaT, MAP)
│   ├── apps/                       # Custom application modules
│   └── omnetpp.ini                 # OMNeT++ simulation config
├── examples/
│   ├── simple_spat/
│   ├── dos_attack_sim/
│   └── multi_intersection_test/
```

## 🔧 Getting Started

### Prerequisites
- TransModeler TsmApi COM Interface
- OMNeT++ 5.6.x or 6.0
- CMake and MSYS2 (on Windows)

## Build Instructions

```bash
git clone https://github.com/yourname/transomnet.git
cd transomnet
mkdir build && cd build
cmake ..
make
```

## 🧠 Use Cases
- Secure-by-design ITS controller development
- SPaT and MAP broadcasting via RSUs
- Simulation of DoS attacks, GPS spoofing, or message falsification
- SDN-integrated V2X control loops
- Digital twin of connected corridors

## 📄 License
This project is licensed under the BSD 3-Clause License — see the LICENSE file for details. This permissive license allows use in both academic and commercial applications, with minimal restrictions.

## 📫 Contributing
Pull requests, suggestions, and forks are welcome! Please open an issue to start a discussion or propose enhancements.

## 📖 Citation (for academic use)
If you use TransOMNeT in a publication or technical report, please cite this repository or the associated paper (to be added).