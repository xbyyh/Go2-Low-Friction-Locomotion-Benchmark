# Go2 Low-Friction Locomotion Benchmark
### Robust Quadruped Control under Slippery Real-World Conditions

---

## 🌧️ Introduction

Teaching a robot to walk is a classic problem in robotics and reinforcement learning.  
With modern RL methods like PPO, quadruped robots can achieve stable locomotion in simulation.

However, a key challenge remains:

👉 **Policies trained in ideal conditions often fail when the environment changes.**

---

## ⚠️ Real-World Motivation

Consider deploying a quadruped robot outside controlled lab conditions:

- 🌧️ Wet pavement after rain  
- ❄️ Icy roads in winter  
- 🏢 Polished marble or tile floors indoors  

In these scenarios, ground friction can drop to:

> **μ ≈ 0.1 – 0.15**

A policy trained on normal terrain may:

- lose velocity tracking  
- become unstable  
- or even fail completely  

---

## 🎥 Demo (Flat vs Slippery)

👉 **（这里放演示 GIF，对比最重要）**

<!-- 🔥 在这里放 GIF -->
<p align="center">
  <img src="assets/gifs/flat_vs_slippery.gif" width="600">
</p>

> Left: normal flat ground  
> Right: low-friction slippery surface  

---

## 📊 Key Result (Quick Insight)

Using the same trained policy under identical command inputs:

| Scenario | Mean vx tracking error |
|----------|----------------------|
| Flat ground | 0.108 |
| Slippery ground (μ ≈ 0.1–0.2) | 0.163 |

📌 **Observation:**

Low-friction surfaces significantly degrade velocity tracking performance.

👉 This highlights a **critical deployment risk** for real-world quadruped systems.

---

## 📈 Tracking Performance Comparison

👉 **（这里放最关键的对比图）**

<!-- 🔥 在这里放 tracking 曲线 -->
<p align="center">
  <img src="assets/tracking_plots/vx_tracking_comparison.png" width="700">
</p>

> Velocity tracking under identical command (step_vx_06)

---

## 🎯 What This Project Does

This project builds a **reproducible benchmark and evaluation pipeline** to:

- 🧪 Measure performance degradation under low-friction conditions  
- 📊 Compare flat vs slippery environments  
- 🤖 Train a more robust locomotion policy  

All experiments are conducted on:

- Unitree Go2 quadruped  
- MuJoCo simulation  
- PPO-based velocity tracking policy  

---

## 🧠 Key Idea

Instead of focusing on algorithm novelty, this project emphasizes:

> **evaluation, failure analysis, and robustness under realistic conditions**

---

## 📦 Benchmark Design

To ensure fair comparison, all models are evaluated using a **fixed-command benchmark**:

- hold_zero  
- step_vx_03 / step_vx_06  
- step_wz_05 / step_wz_08  
- switch_vx_wz  

Each episode uses identical command sequences across all environments.

---

## ⚙️ Methodology

- Training: PPO-based locomotion policy  
- Environment:
  - Flat ground (baseline)  
  - Low-friction ground (μ ≈ 0.1–0.4)  
- Evaluation:
  - step-wise command injection  
  - identical episode replay  
- Metrics:
  - mean absolute tracking error  
  - steady-state error  

---

## 📊 (Optional) Robust Policy Result

👉 **（如果你后面做了 robust training，再放）**

<!-- 🔥 可选对比图 -->
<p align="center">
  <img src="assets/tracking_plots/robust_vs_baseline.png" width="700">
</p>

---

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
