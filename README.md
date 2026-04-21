

# Cloud-MEC-Disaster-Recovery-System

## 📌 Overview
This project presents a **Resilient Disaster Recovery Framework** for **Cloud-Assisted Multi-Access Edge Computing (MEC)** networks. It focuses on ensuring service continuity and low latency in the presence of failures such as cloud outages, edge node crashes, and network disruptions.

The system introduces a **proactive recovery approach**, shifting from traditional reactive mechanisms to intelligent, prediction-driven recovery strategies.

---

## 🎯 Objectives
- Analyze limitations of existing cloud-MEC disaster recovery systems  
- Design a **proactive failure detection mechanism**  
- Develop a **low-complexity recovery algorithm**  
- Enable **dynamic edge node collaboration** during failures  
- Maintain **low latency (<100ms)** during service disruption  

---

## 🧠 Key Features

### 🔹 Predictive Failure Detection
- Uses machine learning concepts to anticipate failures before they occur  
- Enables **proactive recovery** instead of reactive failover  

### 🔹 Simplified Recovery Algorithm
- Reduces computational complexity from **O(N³) → O(N)**  
- Supports real-time decision making  

### 🔹 Dynamic Edge Re-Clustering
- Edge nodes reorganize automatically after failure  
- Eliminates dependency on central cloud during outages  

---

## 🏗️ System Architecture
The framework consists of three layers:

User Devices → Edge Nodes → Cloud Data Centers

- **Edge Layer**: Handles low-latency processing  
- **Fog/Control Layer**: Coordinates recovery decisions  
- **Cloud Layer**: Provides large-scale storage and backup  

---

## 🔍 Research Contributions
- Proactive disaster recovery using predictive models  
- Support for **zero-connectivity scenarios** (cloud unavailable)  
- Handling **cascading multi-node failures**  
- Formal modeling of **RTO (Recovery Time Objective)** and **RPO (Recovery Point Objective)**  

---

## 🛠️ Tech Stack (Planned)
- **Python** (Simulation & Modeling)  
- **MATLAB / SimPy / NS-3** (Network Simulation)  
- **Machine Learning Models** (LSTM / Random Forest - planned)  

---

## 📂 Project Structure

Cloud-MEC-Disaster-Recovery-System/ │ ├── docs/               # Research papers & documentation ├── models/             # ML models (planned) ├── simulation/         # Simulation scripts (planned) ├── results/            # Experimental outputs ├── README.md

---

## 🚀 Current Status
- ✅ Literature Review Completed  
- ✅ Problem Definition & Research Gaps Identified  
- ✅ Framework Design Proposed  
- ⏳ Simulation & Implementation (In Progress)  

---

## 📊 Expected Outcomes
- Reduced recovery latency  
- Improved system resilience  
- Proactive failure handling  
- Better SLA (Service Level Agreement) compliance  

---

## 🔮 Future Work
- Implement simulation environment  
- Train predictive ML models  
- Evaluate performance under real-world scenarios  
- Compare with state-of-the-art recovery techniques  

---

## 👨‍💻 Authors
- **Shehroz Majeed**  
- **Haider Iqbal**  

---

## 📄 License
This project is for academic and research purposes.

