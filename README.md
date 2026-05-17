IPDR-Cloud — Intelligent Predictive Disaster Recovery
A Deep Q-Network (DQN) Reinforcement Learning system for cloud disaster recovery that dynamically learns optimal backup scheduling policies from non-stationary workloads. Replaces static Random Forest classification with a true RL agent that adapts to changing cloud conditions in real time.
Architecture
```
┌─────────────────────────────────────────────────────────┐
│                    Flask Backend (app.py)                │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────┐ │
│  │  RL Env       │  │  DQN Agent   │  │  JSON API     │ │
│  │  (rl\_env.py)  │──│ (dqn\_agent)  │──│  /api/state   │ │
│  │  8 features   │  │  PyTorch NN  │  │  /api/control │ │
│  └──────────────┘  └──────────────┘  └───────┬───────┘ │
└──────────────────────────────────────────────┼─────────┘
                                               │ poll 1s
                                    ┌──────────▼──────────┐
                                    │  Dashboard (HTML/JS) │
                                    │  Chart.js + GSAP     │
                                    └─────────────────────┘
```
State Space (8 Features)
Feature	Unit	Description
`cpu\_util`	%	CPU utilization
`mem\_util`	%	Memory utilization
`disk\_io`	MB/s	Disk I/O throughput
`net\_latency`	ms	Network latency
`error\_rate`	%	Error rate
`backup\_age`	min	Time since last backup
`sla\_breach\_risk`	0–1	Composite breach risk score
`workload\_trend`	-1 to 1	Workload slope
Action Space
Action	Label	Backup Interval
0	NORMAL	Every 30 steps
1	WARNING	Every 10 steps
2	CRITICAL	Every 2 steps
Reward Function
```
R(t) = -10    if SLA breached at failure event
        +1    if failure occurs and SLA is met
       -0.1   per backup triggered
       +0.01  per idle step (no failure, no backup)
```
SLA compliance: RTO ≤ 5.0 min and RPO ≤ 15.0 min
DQN Agent
Network: 8 → 64 → 64 → 32 → 3 (ReLU activations)
Replay Buffer: 10,000 transitions
Epsilon Decay: 0.995 per episode (not per step)
Target Network: hard update every 10 episodes
Optimizer: Adam (lr=1e-3)
Framework: PyTorch
File Structure
```
ipdr\_cloud/
├── rl\_env.py              # Custom Gymnasium environment
├── dqn\_agent.py           # DQN network, replay buffer, agent
├── train\_dqn.py           # Train agent, print RTO/RPO/SLA results
├── run\_experiments.py     # Full experiment pipeline → graph\_data.json
├── generate\_graphs.py     # Read graph\_data.json → 8 PNG graphs
├── app.py                 # Flask backend + real-time simulation
├── templates/
│   └── index.html         # Dashboard UI (Chart.js, GSAP)
├── model/
│   └── dqn\_cloud\_dr.pth   # Trained model weights
├── results/
│   ├── graph\_data.json    # All experiment data for 8 graphs
│   ├── dqn\_rewards.png    # Training reward curve
│   └── dqn\_loss.png       # Training loss curve
├── data/
│   └── borg\_traces\_data.csv  # Google Cluster Trace dataset
├── requirements.txt
└── README.md
```
Setup
```bash
pip install -r requirements.txt
```
Usage
1. Train the DQN agent
```bash
python train\_dqn.py
```
Trains for 500 episodes, saves model to `model/dqn\_cloud\_dr.pth`, prints RTO/RPO/SLA compliance results.
2. Run full experiments (all 8 graphs)
```bash
python run\_experiments.py
```
Runs:
DQN training (150 episodes)
Protocol comparison: Reactive vs Rule-Based vs DQN
Non-stationary adaptation (DQN vs Paper 10 baseline)
Reward weight ablation (3 configs)
Feature correlation analysis
Outputs `results/graph\_data.json` with data for all 8 research graphs.
3. Generate graphs
```bash
python generate\_graphs.py
```
Reads `graph\_data.json` and produces 8 publication-quality PNG graphs in `results/`.
4. Launch live dashboard
```bash
python app.py
```
Opens at `http://localhost:5000`. Features:
Live telemetry bars (8 features, color-coded thresholds)
Non-stationary vs stationary trace comparison charts
DQN decision panel with Q-values
Backup event log
Simulation controls (Force Failure, Traffic Spike, Pause/Play)
Experiment Graphs
#	Graph	Source
1	SLA Compliance Comparison	Reactive / Rule-Based / DQN
2	RTO/RPO Reduction	Mean RTO and RPO per protocol
3	DQN Learning Curve	Cumulative reward per episode
4	Non-Stationary Adaptation	Sliding-window SLA with workload shift
5	Backup Action Distribution	Action timeline with failure markers
6	Reward Convergence	Average reward per episode
7	Reward Weight Optimization	Ablation across 3 reward configs
8	Feature Correlation	Pearson correlation with SLA breach
Requirements
Python 3.10+
PyTorch
Gymnasium
Flask
NumPy, Pandas, Matplotlib
