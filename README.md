# Empirical Study on Testing Model-Based Reinforcement Learning Systems

This repository contains the research artifact accompanying an empirical study on the applicability and effectiveness of existing Reinforcement Learning (RL) testing frameworks when applied to Model-Based Reinforcement Learning (MBRL) systems.

---

## Table of Contents
- [Artifact Overview](#artifact-overview)
- [Repository Structure](#repository-structure)
- [Running the Artifact](#running-the-artifact)
  - [Google Colab (Recommended)](#google-colab-recommended)
  - [Local Execution](#local-execution)
- [Large Model Files (DreamerV3)](#large-model-files-dreamerv3)
- [Expected Outputs](#expected-outputs)
- [Anonymity Statement](#anonymity-statement)

---

## Artifact Overview

The artifact consists of **seven executable Jupyter notebooks**, each corresponding to one environment–agent pair:

| Notebook | Agent | Environment |
|--------|------|------------|
| `N01_DynaQ_Taxi.ipynb` | Dyna-Q | Taxi |
| `N02_DynaQ_Frozenlake.ipynb` | Dyna-Q | FrozenLake |
| `N03_MuZero_Connect4.ipynb` | MuZero | Connect4 |
| `N04_MuZero_Cartpole.ipynb` | MuZero | CartPole |
| `N05_PETS_Pendulum.ipynb` | PETS | Pendulum |
| `N06_DreamerV3_Crafter.ipynb` | DreamerV3 | Crafter |
| `N07_MuZero_Lunalander.ipynb` | MuZero | LunarLander |

Each notebook:
- loads a fixed, pre-trained agent
- executes 18 RL testing frameworks
- computes metrics (FR, TTF, APFD, APFD-time)
- generates tables and plots

---
## Repository Structure
```text
mbrl-testing-frameworks-empirical-study/
├── notebooks/        # All experiment notebooks
├── agents/           # Pre-trained agent components
├── results/          # Generated results (tables, plots, raw logs)
├── data/             # Test pools (e.g., Connect4)
├── envs/             # Custom environments (e.g., Connect4)

The results/ directory is populated automatically when notebooks are executed.
```

## Running the Artifact

This artifact can be executed either on Google Colab (recommended) or locally.

---
### Google Colab (Recommended)
Each notebook includes a Google Colab–specific setup cell.
Steps:
1. Upload the repository to Google Drive
3. Open a notebook from the `notebooks/` directory
5. Run all cells sequentially (or use "run all")

All required output folders are created automatically during execution.

---
### Local Execution
Each notebook also includes a local path configuration cell, for example:
```python
AGENT_ROOT  = Path("mbrl-testing-frameworks-empirical-study/agents/muzero/cartpole")
RESULTS_DIR = Path("mbrl-testing-frameworks-empirical-study/results/cartpole")
```
Requirements: Python ≥ 3.9, Jupyter Notebook or JupyterLab

---

## Large Model Files (DreamerV3)

The DreamerV3 checkpoint is not included in this repository due to file size constraints.

It is publicly available via Zenodo: 🔗 [DreamerV3 agent checkpoint (Zenodo)](https://zenodo.org/records/18528220)

### Using the Real DreamerV3 Policy
To run the Crafter experiment with the real DreamerV3 agent:
1. Download the checkpoint from Zenodo
2. Place it under: agents/dreamerv3/crafter/
3. Uncomment (LOAD REAL DREAMERV3) code cell
4. In `N06_DreamerV3_Crafter.ipynb`, set:

    ```python
    USE_REAL_DREAMER = True
    ```
   
### Default Behavior
By default, the notebook runs with a competent fallback policy that preserves: action distribution characteristics, interaction frequency, oracle semantics
This ensures the notebook remains fully executable even without the large binary file.


---
## Expected Outputs
After executing a notebook, the following artifacts are generated under:

*tables/*

- Single-row metric summaries per testing framework
  
*figs/*

- Failure Rate bar plots
- Cumulative Failures vs Tests
- Cumulative Failures vs Time
  
*raw_single/*

- Per-episode failure logs
---
## Anonymity Statement
This repository is fully anonymized for double-blind review:
- no author names or affiliations are included
- no identifying metadata is present
- external resources (e.g., Zenodo) are referenced without attribution
