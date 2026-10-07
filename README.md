# STRIDE-Z

A sliding-window persistent-homology descriptor of bilateral stride-interval geometry.

**Status:** research code, version 0.3.1. Synthetic benchmark and open-cohort feasibility study. Not a clinical tool and not a validated biomarker.

## What this repository contains

- `stridez/`: the Python package. Paired left/right stride intervals are mapped to a two-dimensional point cloud, and a Vietoris–Rips H1 persistent-homology computation (own NumPy implementation, no external persistent-homology library) yields the Coordination Loop Persistence Ratio (CLPR).
- `experiments/`: scripts for the synthetic benchmark, the PhysioNet GaitNDD analysis and the sensitivity sweep.
- `config/frozen_config.yaml`: the frozen analysis configuration.
- `results/`: archived result tables.
- `tests/`: unit tests (`pytest tests/ -v`).

## Main findings, with their limits

- In a 1,200-series synthetic benchmark, CLPR was more steadily associated with disruption severity than stride-time CV under phase drift and intermittent breaks, and showed no advantage under independent noise.
- In all 64 GaitNDD records, CLPR was computable for every subject but did not separate the four diagnostic groups (Kruskal–Wallis H = 3.262, p = 0.353), whereas the five baseline measures did.
- CLPR values and subject rank order depend on window length and normalization.

See the manuscript for the full analysis and limitations.

## Installation

```
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pytest tests/ -v
```

## Reproducing the analyses

```
python3 experiments/run_synthetic.py --config config/frozen_config.yaml
python3 experiments/analyze_synthetic.py
bash experiments/download_gaitndd.sh
python3 experiments/run_physionet.py --config config/frozen_config.yaml
python3 experiments/analyze_physionet.py --input results/gaitndd_subject_level_v03.csv
python3 experiments/robustness_physionet.py
python3 experiments/make_figures.py
```

## Data

The real-data analysis uses the PhysioNet Gait in Neurodegenerative Disease Database (Hausdorff, 2000; DOI 10.13026/C27G6C; Open Data Commons Attribution License v1.0). The raw data are not redistributed here; `download_gaitndd.sh` fetches them from PhysioNet.

## Citation

Cite the archived release through its Zenodo DOI (see `CITATION.cff`).

## License

Code: MIT (see `LICENSE`).
