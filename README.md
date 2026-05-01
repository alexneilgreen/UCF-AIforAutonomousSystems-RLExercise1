<!-- SHOWCASE: false -->

# Reinforcement Learning Exercise: Deep RL Hyperparameter Study

> Trains and evaluates RL agents to follow a synthetic speed profile, comparing algorithms and hyperparameters using stable-baselines3 and custom Gymnasium environments.

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Language](https://img.shields.io/badge/language-Python-blue)
![Semester](https://img.shields.io/badge/semester-Spring%202025-orange)

---

## Course Information

| Field                  | Details                                                                                                                                                                                                                                       |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Course Title           | Special Topics: Artificial Intelligence for Autonomous Systems                                                                                                                                                                                |
| Course Number          | EEL 6938                                                                                                                                                                                                                                      |
| Semester               | Spring 2025                                                                                                                                                                                                                                   |
| Assignment Title       | Reinforcement Learning Exercise 1                                                                                                                                                                                                             |
| Assignment Description | Modify a provided RL training script to support multiple algorithms, reward functions, and hyperparameters, then systematically experiment across configurations to identify the optimal setup for a continuous speed-following control task. |

---

## Project Description

This project implements a reinforcement learning pipeline for a speed-profile-following control task using custom Gymnasium environments and the stable-baselines3 library. A 1200-step synthetic speed dataset is generated and split into episodic training chunks, with agents trained to minimize speed error via continuous acceleration commands. Eight hyperparameter categories are investigated through automated experimentation, including algorithm type (SAC, PPO, TD3, DDPG), batch size, chunk size, learning rate, gamma, entropy coefficient, network architecture, and reward function. Results are evaluated using MAE, MSE, RMSE, and 95th-percentile error, with PPO + squared error reward emerging as the optimal configuration.

---

## Screenshots / Demo

> _No screenshot available. Add one with: `![Demo](docs/your-image.png)`_

---

## Results

When run correctly, the program produces per-experiment output directories containing trained model files, test result CSVs, performance metric CSVs, and six visualization plots. A final summary report is generated when running all experiments. Sample terminal output during a training run looks like:

```
Training SAC model with chunk_size=100, lr=3e-4, batch=256 ...
Saving model to ./logs_algorithm/SAC/model.zip
Testing model over 1200 steps ...
MAE: 2.1546 | MSE: 7.5267 | RMSE: 2.7435 | 95th Pct: 5.4924
Results saved to ./logs_algorithm/SAC/test_results.csv
```

The six plots generated per experiment are: speed tracking (reference vs. predicted), absolute error over time, squared error over time, control action (acceleration), error histogram, and a combined summary plot. Lower MAE, MSE, and RMSE values indicate better tracking. The best overall configuration identified was PPO with batch size 64, chunk size 50, learning rate 1e-5, gamma 0.9, entropy coefficient 0.1, small network architecture (64, 64), and squared error reward. If results appear poor, check the `--timesteps` value (default 100,000) and consider increasing it, or verify GPU availability for faster training.

---

## Key Concepts

`reinforcement-learning` `proximal-policy-optimization` `soft-actor-critic` `gymnasium` `stable-baselines3` `hyperparameter-tuning` `reward-shaping` `continuous-control` `speed-profile-tracking` `MAE` `MSE` `RMSE`

---

## Languages & Tools

- **Language:** Python 3
- **Framework/SDK:** stable-baselines3, Gymnasium, PyTorch
- **Hardware:** GPU-accelerated training supported (CUDA); falls back to CPU automatically
- **Build System:** pip / requirements.txt

---

## File Structure

```
Reinforcement-Learning-Exercise/
├── Main.py                  # Experiment runner: automates hyperparameter sweeps and compiles final results
├── RL_assignment.py         # Core RL environment, training logic, evaluation, and visualizations
├── speed_profile.csv        # Auto-generated 1200-step synthetic speed dataset
├── requirements.txt         # Python dependencies
├── logs_*/                  # Per-experiment output directories (models, CSVs, plots)
├── comparative_results_*/   # Cross-configuration comparison plots and metrics
└── final_report/            # Summary visualizations produced when running all experiments
```

---

## Installation & Usage

### Prerequisites

- Python 3.8 or later
- pip

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/alexneilgreen/UCF-AIAutonomousSystems-RLExercise1.git
cd UCF-AIAutonomousSystems-RLExercise1

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run all experiments (default 100,000 timesteps)
python Main.py

# Or run a specific experiment type
python Main.py --experiment algorithm --timesteps 100000
```

### Controls

| Argument                     | Action                                                    |
| ---------------------------- | --------------------------------------------------------- |
| `--experiment all`           | Run all hyperparameter experiment categories sequentially |
| `--experiment learning_rate` | Run only learning rate experiments                        |
| `--experiment batch_size`    | Run only batch size experiments                           |
| `--experiment chunk_size`    | Run only chunk size experiments                           |
| `--experiment reward`        | Run only reward function experiments                      |
| `--experiment algorithm`     | Run only algorithm comparison experiments                 |
| `--experiment network_arch`  | Run only network architecture experiments                 |
| `--experiment gamma`         | Run only discount factor experiments                      |
| `--experiment ent_coef`      | Run only entropy coefficient experiments                  |
| `--timesteps N`              | Set total training timesteps per run (default: 100000)    |

---

## Academic Integrity

This repository is publicly available for **portfolio and reference purposes only**.
Please do not submit any part of this work as your own for academic coursework.
