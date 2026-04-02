# Go2 Low-Friction Locomotion Benchmark
### A reinforcement learning project that improves quadruped stability under low-friction conditions (e.g., wet floors, ice, tiles).

---

## 🌧️ Introduction

Teaching a robot to walk is a classic problem in robotics and reinforcement learning.  
With modern RL methods like PPO, quadruped robots can achieve stable locomotion in simulation.

However, a key challenge remains:

👉 **Policies trained in ideal conditions often fail when the environment changes.**

---

## 🌍 Motivation

Imagine a quadruped robot walking on:

- Wet marble floors (μ ≈ 0.1–0.2)
- Icy roads in winter
- Polished indoor tiles

In these conditions, robots easily slip and lose balance.

👉 This project focuses on improving locomotion robustness under low-friction environments.

---

## 🎥 Demo: Robustness under Different Terrains

### 🟦 Flat Terrain (Normal Ground)

| Baseline Policy | Robust Policy (Slippery-Trained) |
|----------------|----------------------------------|
| ![](base4800flat.gif) | ![](slippery1.0flat.gif) |

👉 Both policies perform well on flat terrain.

---

### 🧊 Slippery Terrain (Low Friction μ ≈ 0.1–0.2)

| Baseline Policy | Robust Policy (Slippery-Trained) |
|----------------|----------------------------------|
| ![](baseline4800slippery.gif) | ![](slippery1.0slippery.gif) |

👉 Baseline becomes unstable, while the robust policy maintains balance and tracking performance.


### Result

| Scenario | Outcome |
|----------|--------|
| Flat + baseline | Stable |
| Slippery + baseline | Falls |
| Slippery + robust | Stable |

👉 The robust policy significantly improves stability under external disturbance.

📌 **Observation:**

Low-friction surfaces significantly degrade velocity tracking performance.

👉 This highlights a **critical deployment risk** for real-world quadruped systems.

---

⚖️ Robustness Without Conservativeness

A common concern in robustness-oriented training is that policies become overly conservative, sacrificing speed or responsiveness.

However, this is not observed in our case:

At low velocities, the robust policy achieves better tracking and faster convergence
At higher velocities, performance remains comparable to baseline
Under low-friction conditions, stability is improved without degrading motion quality

👉 This is directly evidenced by the velocity tracking results shown below, including tracking accuracy and steady-state behavior.

---

## 📊 Overall Comparison

<p align="center">
  <img src="comprehensive_error_comparison.png" width="1000">
</p>

👉The robust (slippery-trained) policy achieves lower mean and steady-state errors in most cases, particularly at low-to-medium linear and angular velocities as well as during standstill, while maintaining comparable performance to the baseline at higher speeds.

---

## ⚠️ Extreme Case: Rapid Yaw Reversal (lwz → rwz)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_lwz_rwz_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_lwz_rwz_wz_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_lwz_rwz_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_lwz_rwz_wz_tracking.png) |

👉 Stress test under abrupt direction switching (high angular acceleration).

---
## 📈 Velocity Tracking (vx = 0.3)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_vx_03_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_vx_03_vx_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_vx_03_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_vx_03_vx_tracking.png) |

---

## 📈 Velocity Tracking (vx = 0.6)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_vx_06_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_vx_06_vx_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_vx_06_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_vx_06_vx_tracking.png) |

---

## 📈 Velocity Tracking (vx = 0.9)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_vx_09_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_vx_09_vx_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_vx_09_vx_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_vx_09_vx_tracking.png) |

---

## 🔄 Angular Velocity Tracking (wz = 0.3)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_wz_03_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_wz_03_wz_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_wz_03_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_wz_03_wz_tracking.png) |

---

## 🔄 Angular Velocity Tracking (wz = 0.6)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_wz_06_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_wz_06_wz_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_wz_06_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_wz_06_wz_tracking.png) |

---

## 🔄 Angular Velocity Tracking (wz = 0.9)

| Terrain | Baseline | Robust |
|--------|----------|--------|
| Flat | ![](baseline/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_baseline_model_4800_step_wz_09_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Flat/eval_log_Unitree_Go2_Flat_slippery1.0_model_4800_step_wz_09_wz_tracking.png) |
| Slippery | ![](baseline/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_baseline_model_4800_step_wz_09_wz_tracking.png) | ![](slippery1.0plot/Unitree_Go2_Slippery/eval_log_Unitree_Go2_Slippery_slippery1.0_model_4800_step_wz_09_wz_tracking.png) |

👉 Both policies degrade on slippery terrain, but the slippery-trained policy achieves faster convergence and lower steady-state error at low-to-medium speeds, while remaining comparable at higher velocities.

---

## 📊 Qualitative Comparison (Robust vs Baseline)

| Setting | Mean Error | Convergence | Steady Error | Stability |
|--------|-----------|------------|-------------|----------|
| **Linear (low) - Flat** | ↑ | ↑ | ↑ | ✓ |
| **Linear (low) - Slippery** | ↑ | ↑ | ↑ | ✓ |
| **Linear (medium) - Flat** | ↑ | ↑ | ↑ | ✓ |
| **Linear (medium) - Slippery** | ↑ | ↑ | ↑ | ✓ |
| **Linear (high) - Flat** | ↑ | ↑ | ≈ | ✓ |
| **Linear (high) - Slippery** | ↑ | ↑ | ↓ | ✓ |
| **Angular (low) - Flat** | ↑ | ≈ | ↑ | ✓ |
| **Angular (low) - Slippery** | ↑ | ≈ | ↓ | ✓ |
| **Angular (medium) - Flat** | ↓ | ≈ | ↓ | ✓ |
| **Angular (medium) - Slippery** | ↑ | ≈ | ↑ | ✓ |
| **Angular (high) - Flat** | ↓ | ≈ | ↓ | ✓ |
| **Angular (high) - Slippery** | ≈ | ≈ | ≈ | ✓ |
| **Standstill - Flat** | ↑ | ≈ | ≈ | ✓ |
| **Standstill - Slippery** | ↑ | ≈ | ≈ | ✓ |
| **Rapid Yaw Reversal - Flat** | ↓ | ≈ | ↑ | ✓ |
| **Rapid Yaw Reversal - Slippery** | ↑ | ≈ | ↑ | ↑↑ |


**Legend:**  
↑ better than baseline  ↓ worse than baseline  ≈ comparable  ✓ no failure  ↑↑ significantly more stable

---

## ⚙️ Methodology

- Policy: PPO-based locomotion controller (MuJoCo, Unitree Go2)  
- Training environments:
  - Flat ground (baseline)  
  - Low-friction ground with randomized μ ∈ [0.1, 1.2]  

- Evaluation:
  - fixed-command benchmark  
  - identical command sequences across environments  

- Metrics:
  - mean absolute tracking error  
  - steady-state error  
  - convergence behavior  
---
## 📉 Training Performance

<p align="center">
  <img src="baseline/baseline_reward.png" width="48%">
  <img src="slippery1.0plot/slippery1.0_reward.png" width="48%">
</p>

<p align="center">
Baseline &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Robust (Slippery-Trained)
</p>

👉 Both models reach peak performance around 4800 iterations, after which a noticeable drop in reward is observed.

👉 We select checkpoints near this peak for evaluation.

## 🚀 Quick Start

```bash
# train baseline
python scripts/train.py --task flat

# train robust policy
python scripts/train.py --task slippery_train

# evaluate
python scripts/eval_fixed_cmd.py --model models/baseline.pt

# analyze results
python scripts/analyze_and_plot.py
