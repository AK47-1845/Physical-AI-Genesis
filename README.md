# The Physical AI Atlas [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![Track](https://img.shields.io/badge/Status-Living%20Standard-brightgreen.svg)](https://github.com/AK47-1845/physical-ai-atlas) [![Python](https://img.shields.io/badge/Python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13-blue.svg)](https://www.python.org/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/AK47-1845/physical-ai-atlas/pulls) [![Safety: ISO 13849](https://img.shields.io/badge/Safety-ISO%2013849%20%7C%20IEC%2061508-red.svg)](./ARCHITECTURE.md)

> **The Open Standard, System Architecture, and Engineering Roadmap for Physical AI, Vision-Language-Action (VLA) Foundation Models, World Models, and Industrial Embodied Intelligence.**

---

<div align="center">
  <a href="./docs/index.html"><strong>🌐 Launch Interactive Web Portal</strong></a> •
  <a href="./ROADMAP.md"><strong>🗺️ Practitioner Roadmap</strong></a> •
  <a href="./HARDWARE_GUIDE.md"><strong>🔩 Hardware Lab Guide ($250 to $100k)</strong></a> •
  <a href="./ARCHITECTURE.md"><strong>🏛️ Theoretical Architecture</strong></a> •
  <a href="./examples"><strong>⚡ Runnable Starter Code</strong></a> •
  <a href="./briefings"><strong>📑 Executive Briefing Decks</strong></a>
</div>

---

## 🌟 Executive Overview: The Physical Paradigm Shift

**Physical Artificial Intelligence (Physical AI)** marks the fundamental transition from autoregressive next-token prediction in static semantic spaces to **closed-loop causal interaction with continuous physical dynamics**.

While Large Language Models (LLMs) operate on statistical association ($P(Y \mid X)$), robots and embodied agents must operate on **causal interventions** ($P(Y \mid \text{do}(u))$) and **counterfactual planning** ($P(Y_u \mid X', Y')$) governed by continuous differential equations of motion:

$$\tau = M(q)\ddot{q} + C(q, \dot{q})\dot{q} + g(q) - J^T(q)F_{\text{contact}}$$

```
                      ▲
     RUNG III         │   Counterfactuals: P(Y_u | X', Y')
   (Imagining)        │   "What would have happened had the robot gripped with 5N less force?"
                      │
     RUNG II          │   Interventions: P(Y | do(u))
     (Doing)          │   "What is the system trajectory if actuator 3 applies torque tau?"
                      │
     RUNG I           │   Associations: P(Y | X)
    (Seeing)          │   "What text tokens/pixels statistically co-occur in historical data?"
                      └────────────────────────────────────────────────────────►
```

In language, hallucinating a wrong token can be regenerated or ignored. In physical systems, hallucinating an unsafe torque breaches contact boundaries, breaks expensive tooling, or injures human operators. **Physical AI requires mathematical guarantees, derivative continuity, and real-time safety envelopes.**

---

## ⚡ Quick Start: 5 Verified Starter Kits

This repository provides tested, production-grade Python reference scripts that run out of the box:

```bash
# 1. Clone the repository
git clone https://github.com/AK47-1845/physical-ai-atlas.git
cd physical-ai

# 2. Run the 5 standalone starter demos (Zero external GPU dependencies required):
python examples/01_diffusion_policy_minimal.py   # Continuous Action Chunking via DDPM
python examples/02_flow_matching_action.py        # Action Flow Matching (pi-0 / ManiFlow style)
python examples/03_cbf_safety_filter.py           # Real-Time Control Barrier Function QP Filter
python examples/04_vla_inference_pipeline.py      # VLA Multimodal Inference (OpenVLA/SmolVLA)
python examples/05_brownfield_plc_bridge.py       # Industrial PLC Fieldbus Bridge & Watchdog
```

---

## 🏛️ System Architecture: The Full Physical AI Stack

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              THE PHYSICAL AI ARCHITECTURE                              │
├────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                        │
│   MULTIMODAL SENSORY INGESTION (30 Hz - 60 Hz)                                         │
│   • Wrist & Overhead RGB-D Cameras (RealSense D405/D435i)                              │
│   • Elastomeric Tactile Sensing (GelSight Mini / DIGIT) for contact shear stress       │
│   • High-precision Joint Proprioception & Encoders [q, dot(q)]                         │
│                                                                                        │
│                                      │                                                 │
│                                      ▼                                                 │
│                                                                                        │
│   SLOW REASONING LAYER (System 2: 1 Hz - 5 Hz)                                         │
│   • Large Vision-Language-Action Models (OpenVLA, PaLM-E, Gemini Robotics)             │
│   • Semantic scene grounding and hierarchical sub-goal task decomposition              │
│                                                                                        │
│                                      │                                                 │
│                                      ▼                                                 │
│                                                                                        │
│   FAST VISUOMOTOR EXECUTION (System 1: 50 Hz - 100 Hz)                                 │
│   • Optimal Transport Flow Matching Policy (pi-0, ManiFlow)                            │
│   • 3-5 Euler ODE integration steps generating smooth continuous action chunks         │
│                                                                                        │
│                                      │                                                 │
│                                      ▼                                                 │
│                                                                                        │
│   DETERMINISTIC SAFETY ENVELOPE (1,000 Hz Hard Real-Time)                              │
│   • Control Barrier Function (CBF) Quadratic Program (QP) Minimal-Intervention Filter  │
│   • Kinematic Singularity Mitigation via Damped Least-Squares (DLS):                   │
│     J* = J^T (J J^T + lambda^2 I)^(-1)                                                 │
│   • alpha,beta-CROWN Forward Reachable Set Verification (ISO 13849 PL-d Compliance)    │
│                                                                                        │
│                                      │                                                 │
│                                      ▼                                                 │
│                                                                                        │
│   BROWNFIELD INDUSTRIAL ACTUATION LAYER (Fieldbus)                                     │
│   • Deterministic 50ms Watchdog Heartbeat Interlock                                    │
│   • Modbus TCP / EtherCAT / OPC-UA Fixed-Point Register Serialization                  │
│   • Motor Servo Drives (CAN FD / EtherCAT / RS-485)                                    │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🌐 The Three Schools of World Modeling

A **World Model** allows an agent to simulate, plan, and evaluate actions before executing them in the irreversible physical world.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              THE 3 WORLD MODEL SCHOOLS                                 │
├─────────────────────────┬──────────────────────────┬───────────────────────────────────┤
│ SCHOOL I: GENERATIVE    │ SCHOOL II: LATENT        │ SCHOOL III: SPATIAL & OCCUPANCY   │
│ (Pixel / Video Models)  │ (Energy-Based JEPA)      │ (3D PointFlows & PINNs)           │
├─────────────────────────┼──────────────────────────┼───────────────────────────────────┤
│ • Sora, Genie 2, Cosmos │ • LeCun JEPA, V-JEPA 2   │ • PointWorld, 3DGS-Dynamics       │
│ • Predicts raw pixels   │ • Predicts latent states │ • Predicts 3D point flows & volume│
│ • Photorealistic        │ • Fast inference (<5ms)  │ • Formally verifiable geometry    │
│ • High latency (>200ms) │ • Discards pixel noise   │ • Guaranteed collision bounds     │
└─────────────────────────┴──────────────────────────┴───────────────────────────────────┘
```

*See [ARCHITECTURE.md](./ARCHITECTURE.md) for full mathematical comparisons and loss formulations.*

---

## ⚠️ The 5 Canonical Failure Modes & Industrial Solutions

| # | Canonical Failure Mode | Underlying Physical Mechanism | Industrial & Theoretical Mitigation |
| :-: | :--- | :--- | :--- |
| **1** | **Visual Distractor Fragility** | Background shifts cause spurious cross-attention activations | Invariant feature pretraining (DINOv2 / SigLIP) + visual domain randomization |
| **2** | **Multi-Contact Discontinuity** | Non-smooth Coulomb friction boundaries ($F_f \le \mu F_N$) | Hybrid continuous dynamics + elastomeric tactile feedback (GelSight) |
| **3** | **Kinematic Singularity Explosion** | Yoshikawa manipulability $\mu(q) \to 0$ demands infinite joint rates | **Damped Least-Squares (DLS)** inverse filtering: $J^* = J^T(J J^T + \lambda^2 I)^{-1}$ |
| **4** | **Compounding Covariate Shift** | $O(\epsilon T^2)$ drift off expert demonstration manifold | **Action Chunking (ACT)** + **Flow Matching ($\pi_0$)** with temporal ensembling |
| **5** | **Edge Latency Jitter** | Dropped frames violate control loop stability deadlines | **Deterministic RTOS Watchdog** + Control Barrier Function (CBF) QP override |

---

## 🗺️ Complete Practitioner Roadmap

Looking for a structured, step-by-step path to master Physical AI? Follow our complete **[ROADMAP.md](./ROADMAP.md)**:

1. **Classical Mechanics, Kinematics & Spatial Algebra** ($SE(3)$, Jacobians, Operational Space Control)
2. **Physics Simulators & Synthetic Data Foundries** (Isaac Lab, Genesis, MuJoCo, Domain Randomization)
3. **Visuomotor Imitation Learning & Policy Representations** (ACT, Diffusion Policies, Flow Matching)
4. **Vision-Language-Action (VLA) Foundation Models** (OpenVLA, SmolVLA, Fast-in-Slow Systems)
5. **World Models & Predictive Latent Dynamics** (JEPA, V-JEPA 2, PointWorld)
6. **Sim-to-Real, Safety & Formal Verification** (Control Barrier Functions, $\alpha,\beta$-CROWN reachability)
7. **Real-Time Edge Quantization & Industrial PLC Bridges** (AutoQVLA, Modbus/EtherCAT, 50ms Watchdogs)
8. **Physical Hardware, Bimanual Teleop & Humanoids** (LeRobot SO-ARM100 to Unitree G1)

---

## 🔩 Hardware Lab Blueprint

| Tier | Budget | Embodiment | Actuation / Compute | Primary Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Tier 1: Bedroom Hacker** | **~$291 USD** | 3D Printed SO-ARM100 | 6x Feetech STS3215 Servos + Waveshare Bus + Jetson Nano | Hobbyist, student lab, LeRobot imitation learning |
| **Tier 2: Research R&D** | **$4,500 - $15,000** | AgileX Piper / Franka Panda | Dynamic joint torque sensing + RealSense D405 + RTX 4090 | Academic lab, dexterous assembly, benchmark evaluation |
| **Tier 3: Enterprise Humanoid** | **$16,000 - $100k+** | Unitree G1 / Figure 02 | 23-43 DoF bipedal humanoid with whole-body control | Automotive kitting, warehouse logistics, frontier research |

*Read the complete [HARDWARE_GUIDE.md](./HARDWARE_GUIDE.md) for full Bill of Materials (BOM), sensor guides, and STL files.*

---

## 📑 Curated Research Paper Index

### Vision-Language-Action (VLA) Foundation Models
- **π0 (pi-zero)** (Physical Intelligence 2024) - "A Vision-Language-Action Flow Model for General Robot Control" [[Paper](https://arxiv.org/abs/2410.24164)]
- **OpenVLA** (CoRL 2024) - "An Open-Source Vision-Language-Action Model" [[Paper](https://arxiv.org/abs/2406.09246)]
- **SmolVLA** (Hugging Face 2025) - "A Small Vision-Language-Action Model for Efficient Robot Learning" [[Blog](https://huggingface.co/blog/smolvla)]
- **RT-2** (CoRL 2023) - "Vision-Language-Action Models Transfer Web Knowledge to Robotic Control" [[Paper](https://arxiv.org/abs/2307.15818)]
- **Fast-in-Slow** (arXiv 2025) - "A Dual-System Foundation Model Unifying Fast Manipulation within Slow Reasoning" [[Paper](https://arxiv.org/abs/2506.01953)]
- **BitVLA** (arXiv 2025) - "1-bit Vision-Language-Action Models for Robotics Manipulation" [[Paper](https://arxiv.org/abs/2506.07530)]
- **AutoQVLA** (ICLR 2026) - "Not All Channels Are Equal in Vision-Language-Action Model Quantization"

### Continuous Flow & Diffusion Policies
- **Diffusion Policy** (RSS 2023) - "Visuomotor Policy Learning via Action Diffusion" [[Paper](https://arxiv.org/abs/2303.04137)]
- **ManiFlow** (CoRL 2025) - "A General Robot Manipulation Policy via Consistency Flow Training" [[Paper](https://arxiv.org/abs/2509.01819)]
- **Streaming Flow Policy** (CoRL 2025 Oral) - "Simplifying Diffusion / Flow-Matching Policies" [[Paper](https://arxiv.org/abs/2505.21851)]
- **GPC** (arXiv 2025) - "Compose Your Policies! Test-Time Distribution-Level Policy Composition" [[Paper](https://arxiv.org/abs/2510.01068)]

### World Models & Latent Dynamics
- **LeCun Architectural Blueprint** (Meta AI 2022) - "A Path Towards Autonomous Machine Intelligence" [[Paper](https://openreview.net/pdf?id=BZ5a1r-kVsf)]
- **V-JEPA 2** (Meta AI 2025) - "Self-Supervised Video Models Enable Understanding, Prediction and Planning" [[Paper](https://arxiv.org/abs/2506.09985)]
- **Genie 2** (DeepMind 2024) - "A Large-Scale Foundation World Model" [[Blog](https://deepmind.google/discover/blog/genie-2-a-large-scale-foundation-world-model/)]
- **Cosmos-Predict2.5** (NVIDIA 2025) - "World Simulation with Video Foundation Models for Physical AI" [[Paper](https://arxiv.org/abs/2511.00062)]
- **PointWorld** (NVIDIA 2026) - "Scaling 3D World Models for In-The-Wild Robotic Manipulation" [[Paper](https://arxiv.org/abs/2601.03782)]

### Cross-Embodiment & Humanoids
- **Open X-Embodiment (RT-X)** (ICRA 2024) - "Robotic Learning Datasets and RT-X Models" [[Paper](https://arxiv.org/abs/2310.08864)]
- **Crossformer** (CoRL 2024 Oral) - "One Policy for Manipulation, Navigation, Locomotion" [[Paper](https://arxiv.org/abs/2408.11812)]
- **EgoScale** (NVIDIA GEAR 2026) - "Scaling Dexterous Manipulation with Diverse Egocentric Human Data" [[Paper](https://arxiv.org/abs/2602.16710)]
- **Being-H0.5** (2026) - "Scaling Human-Centric Robot Learning for Cross-Embodiment Generalization" [[Paper](https://arxiv.org/abs/2601.12993)]

---

## 📑 Executive Briefings & Presentation Deck

For enterprise practice leaders, C-suite executives, and industrial systems integrators:
- **Master 25-Slide Executive Deck (PPTX):** [`The_Practice_of_Physical_AI_Executive_25_Master.pptx`](./briefings/The_Practice_of_Physical_AI_Executive_25_Master.pptx) — Fully styled 16:9 widescreen presentation engineered for high-stakes executive briefings.
- **Reference PDF Deck:** [`The_Practice_of_Physical_AI_Executive_Deck_Master.pdf`](./briefings/The_Practice_of_Physical_AI_Executive_Deck_Master.pdf) — Complete 23-slide executive briefing.
- **Enterprise Whitepaper:** [`Executive_Strategic_Briefing.md`](./briefings/Executive_Strategic_Briefing.md) — Strategic analysis on commercial reality, macro AI economics, and the multi-hundred-million-dollar systems integration opportunity.
- **Master Deck Generator & Self-QA Validator:**
  - [`generate_deck_master_25.py`](./briefings/generate_deck_master_25.py) — 25-slide generator with strict type scale ($\ge 18\text{pt}$ body text), layout constants, and matplotlib 300 DPI equation/diagram rendering.
  - [`validate_deck.py`](./briefings/validate_deck.py) — Programmatic self-QA validator verifying text overflow, font/color explicitness (0 theme leaks), table bounds ($\le 5\times 4$), footer zones, and claim traceability across all 25 slides (**100% PASS**).

---

## 🤝 Contributing

We actively welcome community contributions! Please review [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a Pull Request.

### Standards:
1. **Mathematical Rigor:** Ensure equations use standard notation ($SE(3)$, Lie derivatives, Pearl causality).
2. **Reproducibility:** Code examples must be standalone, verifiable, and adhere to clean PyTorch/NumPy conventions.
3. **No Fluff:** Focus on actionable blueprints, empirical failure modes, and verified benchmarks.

---

## 📜 Citation

If this repository supports your research or industrial engineering workflows, please cite:

```bibtex
@misc{physical-ai-atlas-2026,
  author = {Adari Karthikeya},
  title = {The Physical AI Atlas: The Open Standard, System Architecture & Engineering Roadmap for Embodied Intelligence},
  year = {2026},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/AK47-1845/physical-ai-atlas}}
}
```

---

<div align="center">
  <sub>Maintained with rigorous engineering standards by the open-source Physical AI community.</sub>
</div>
