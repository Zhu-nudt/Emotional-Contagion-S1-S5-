# Supplementary Code — SIA Model of Emotional Contagion on Real-World Networks

This package contains the simulation and analysis code accompanying the manuscript
**"Emotional Contagion Dynamics with Dual Recovery Channels on a Real-World Social Network:
An Agent-Based Complex Systems Model"** (submitted to *Systems*).

The code implements a **susceptible–influenced–aware (SIA)** compartment model of emotional
contagion with **dual recovery channels** — natural recovery (passive fading) and
awareness-mediated recovery (acquisition of emotion-regulation capacity) — and applies it to
real social networks and LFR benchmark networks.

## File overview

| File | Role | Description |
|------|------|-------------|
| `S1_sisa_model.py` | module | Core `SISaModel` class: three states (S / I / Sa) and five transition rules (S→I, I→S, I→Sa, Sa→I, Sa→S) with vectorized Monte-Carlo stepping and early-stop detection. |
| `S2_config.py` | module | All tunable parameters (β, μ, α, δ, awareness protection, dt, seeds) as dataclasses, plus preset configurations. |
| `S3_run_real_networks.py` | **script** | Runs the model on the Facebook and email-Eu-core networks and the LFR benchmark (30 trials each); produces time-series and bar charts plus a metrics JSON. |
| `S4_lfr_network.py` | module | Generates LFR (Lancichinetti–Fortunato–Radicchi) benchmark networks with power-law degree and community-size distributions. |
| `S5_compute_facebook_sna.py` | **script** | Social-network analysis of the Facebook network: degree distribution, communities (Louvain), centralities, and average path length. |

## Requirements

- Python 3.9+
- `networkx>=3.1`, `numpy>=1.24`, `scipy>=1.10`, `matplotlib>=3.7`, `seaborn>=0.12`

```bash
pip install -r requirements.txt
```

## Data

The real networks are public datasets from the **Stanford Large Network Dataset Collection
(SNAP)**, https://snap.stanford.edu/data. Download and place them in the same directory as the
scripts, keeping these names:

- `Facebook.txt.gz` — Facebook ego-network (N = 4039, E = 88,234)
- `email-Eu-core.txt.gz` — email communication network

## Usage

```bash
# Run simulations on real networks + LFR benchmark (S3)
python S3_run_real_networks.py

# Compute Facebook network SNA metrics (S5)
python S5_compute_facebook_sna.py
```

`S1`, `S2`, and `S4` are library modules imported by the scripts above.

## Outputs

| File | Description |
|------|-------------|
| `output_figures/fig7_real_networks.png` | Infection density time series (real networks vs. LFR) |
| `output_figures/fig8_real_networks_bars.png` | Peak vs. steady-state infection density |
| `output_figures/fig9_facebook_degree_distribution.png` | Facebook degree distribution |
| `output_figures/fig10_facebook_community_sizes.png` | Facebook community size distribution |
| `output/real_network_benchmark_metrics.json` | Benchmark metrics (mean ± 95% CI) |
| `output/facebook_sna_metrics.json` | Facebook SNA metrics |

## Default parameters

β = 0.35, μ = 0.10, α = 0.08, δ = 0.02, awareness protection = 0.5,
initial infected fraction = 2%, dt = 0.05 (see `S2_config.py`).
