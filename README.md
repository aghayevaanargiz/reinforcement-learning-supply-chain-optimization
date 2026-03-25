# Reinforcement Learning for Dynamic Supply Chain Optimization

Deep reinforcement learning for inventory allocation under stochastic demand using real-world transactional data.

---

**Authors:** Laman Panakhova, Nargiz Aghayeva, Leyla Eynullazada, Aysu Azammadova, Samir Mammadov  
**Institution:** ADA University, School of Information Technologies and Engineering  
**Status:** Active Research - Paper Under Review, Implementation in Development

---

## Abstract

Inventory allocation in multi-client warehouse systems requires sequential decision-making under demand uncertainty. This project investigates the application of Deep Q-Networks (DQN) to learn adaptive allocation policies from real-world transactional data. The problem is formulated as a Markov Decision Process (MDP) with a reward function balancing fulfillment, backlog clearance, and service level. Preliminary results indicate that learned policies reduce backlog by approximately 18% compared to fixed-multiplier heuristics.

---

## Data

| Attribute | Description |
|-----------|-------------|
| Source | Warehouse-client transaction system |
| Records | 5,847,820 |
| Time Period | July 2024 – June 2025 |
| Active Days | 178 |
| Clients | 9,682 (anonymized) |
| Items | 4,152 |
| Analyzed Pairs | 3,000 (top by transaction volume) |

Raw data is confidential and not included in this repository.

---

## Methodology

### Demand Modeling

Stochastic demand for each item-client pair follows a Gamma process with intermittent zeros. Parameters are estimated from historical data via method-of-moments.

### Markov Decision Process

| Component | Specification |
|-----------|---------------|
| **State Space** | 5-dimensional normalized vector: inventory, backlog, backlog change, average demand, transaction density |
| **Action Space** | Discrete multipliers {0.0, 0.5, 1.0, 2.0, 3.0, 5.0} applied to historical average demand |
| **Reward Function** | Weighted combination: fulfillment (λ=1.0), backlog clearance (λ=8.0), service level (λ=10.0) |
| **Discount Factor** | γ = 0.99 |

### Algorithm

Deep Q-Network (DQN) with:
- Two hidden layers (128 units each, ReLU)
- Experience replay buffer (capacity 200,000)
- Target network with soft updates (τ = 0.005)
- Adam optimizer (learning rate 5×10⁻⁴)
- Gradient clipping at norm 10

---

## Preliminary Results

| Policy | Average Reward | Fulfillment | Service Level | Average Backlog |
|--------|---------------|-------------|---------------|-----------------|
| DQN | 9.978 | 99.8% | 99.0% | 3.54 |
| Greedy (1.0×) | 9.926 | 99.8% | 98.4% | 4.32 |
| Random | 9.856 | 99.6% | 97.0% | 8.55 |
| Conservative (0.5×) | 9.788 | 99.6% | 95.7% | 8.32 |

*Results reported over 50 evaluation episodes. Final results subject to change as research progresses.*

---

## Project Status

| Component | Status |
|-----------|--------|
| Data preprocessing | Complete |
| MDP formulation | Complete |
| DQN implementation | Complete |
| Initial experiments | Complete |
| Code refactoring | In progress |
| Extended experiments | Planned |
| Paper | Under review |

---

## Repository Status

This project is **ongoing**. The repository currently contains the paper draft and preliminary results. Upon finalization of the project, the following will be added:

- Full implementation code
- Training scripts
- Experiment notebooks
- Preprocessing pipelines
- Evaluation metrics
- Configuration files

---

## Technologies

| Category | Stack |
|----------|-------|
| Programming | Python 3.8+ |
| Deep Learning | PyTorch |
| Data Processing | pandas, NumPy |
| Experiment Tracking | MLflow (planned) |

---

## Citation

```bibtex
@techreport{panakhova2025reinforcement,
  author      = {Panakhova, Laman and Aghayeva, Nargiz and Eynullazada, Leyla and Azammadova, Aysu and Mammadov, Samir},
  title       = {Reinforcement Learning for Dynamic Supply Chain Optimization: Managing Inventory Under Stochastic Demand},
  institution = {ADA University, School of Information Technologies and Engineering},
  year        = {2025},
  note        = {Under review}
}
