# ⚡ Critical Transition Analysis: EEG Seizures vs Market Crashes

> *Do complex systems fail the same way?*

What if a brain approaching seizure and a market approaching crash are — mathematically — the same event?

This project explores whether **EEG neural activity** and **financial market dynamics** share common warning signatures before catastrophic state transitions. The hypothesis: radically different systems may obey the same underlying mathematics when they approach instability.

---

## 🧠 The Core Idea

Across physics, ecology, and neuroscience, a phenomenon called **critical slowing down** appears before systems tip from one state into another. As a system approaches a tipping point, it loses its ability to recover from small perturbations — and this leaves measurable fingerprints in the data before the collapse ever happens.

| Warning Signal | Seizure (EEG) | Market Crash |
|---|---|---|
| Rising autocorrelation | Neural activity becomes "stickier" | Price returns show memory |
| Increasing variance | Amplitude swells pre-ictal | Volatility expands |
| Slowing recovery rate | Brain struggles to dampen oscillations | Market takes longer to absorb shocks |
| Cross-correlation changes | Regions synchronize abnormally | Assets that shouldn't move together, do |

The bet this project is making: **these fingerprints are domain-agnostic.**

---

## 📐 Framework

```
Raw Data (EEG / OHLCV)
        │
        ▼
 Preprocessing & Windowing
        │
        ├──► Sliding window variance
        ├──► Lag-1 autocorrelation (AR1)
        ├──► Detrended Fluctuation Analysis (DFA)
        ├──► Power Spectral Density shift
        └──► Early Warning Score (composite)
                │
                ▼
        Tipping Point Proximity Map
```

---

## 🗂️ Repository Structure

```
critical-transition-analysis/
│
├── data/
│   ├── eeg/                  # Raw EEG recordings (.edf, .csv)
│   ├── market/               # OHLCV price data
│   └── processed/            # Windowed, normalized datasets
│
├── notebooks/
│   ├── 01_eeg_exploration.ipynb        # EEG signal basics & nomenclature
│   ├── 02_market_exploration.ipynb     # Market regime analysis
│   ├── 03_early_warning_signals.ipynb  # CSD metrics: variance, AR1, DFA
│   ├── 04_cross_domain_comparison.ipynb # Side-by-side signature analysis
│   └── 05_composite_score.ipynb        # Building an EWS composite index
│
├── src/
│   ├── signals/
│   │   ├── autocorrelation.py    # Lag-1 AR estimation
│   │   ├── variance.py           # Rolling variance + detrending
│   │   ├── dfa.py                # Detrended Fluctuation Analysis
│   │   └── psd.py                # Power spectral density tools
│   │
│   ├── eeg/
│   │   ├── loader.py             # EDF/CSV parsing
│   │   ├── bandpass.py           # Delta, theta, alpha, beta, gamma filters
│   │   └── epoch.py              # Segmentation around seizure events
│   │
│   ├── market/
│   │   ├── loader.py             # Price data ingestion
│   │   ├── regimes.py            # Bull/bear/crash labeling
│   │   └── volatility.py         # GARCH, realized vol, VIX proxy
│   │
│   └── utils/
│       ├── windowing.py          # Sliding window utilities
│       └── visualization.py     # Shared plotting helpers
│
├── results/
│   ├── figures/                  # Generated plots
│   └── reports/                  # Analysis summaries
│
├── tests/
│   └── ...
│
├── requirements.txt
├── environment.yml
└── README.md
```

---

## 🔬 EEG Primer (Work in Progress)

*This section grows as I learn the domain.*

**Electrode Nomenclature (10-20 System)**
- Letters indicate brain region: `F` (frontal), `T` (temporal), `P` (parietal), `O` (occipital), `C` (central)
- Numbers: odd = left hemisphere, even = right, `z` = midline
- Common channels: `Fp1`, `Fp2`, `F3`, `F4`, `C3`, `C4`, `P3`, `P4`, `O1`, `O2`

**Frequency Bands**
| Band | Range | Association |
|---|---|---|
| Delta (δ) | 0.5–4 Hz | Deep sleep, pathological slow waves |
| Theta (θ) | 4–8 Hz | Drowsiness, memory |
| Alpha (α) | 8–13 Hz | Relaxed wakefulness |
| Beta (β) | 13–30 Hz | Active thinking, alertness |
| Gamma (γ) | 30–100 Hz | High-level cognition, binding |

**Seizure Phases**
1. **Interictal** — baseline, no seizure activity
2. **Pre-ictal** — warning window (where early signals live)
3. **Ictal** — the seizure itself
4. **Post-ictal** — recovery

---

## 📊 Datasets

**EEG Sources**
- [CHB-MIT Scalp EEG Database](https://physionet.org/content/chbmit/1.0.0/) (PhysioNet)
- [Bonn EEG Dataset](https://www.ukbonn.de/epileptologie/arbeitsgruppen/ag-lehnertz-neurophysik/downloads/)
- Temple University Hospital EEG Corpus

**Market Sources**
- S&P 500 daily / intraday (Yahoo Finance, Quandl)
- VIX index for implied volatility baseline
- Historical crash events: 1987, 2000, 2008, 2020

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/critical-transition-analysis.git
cd critical-transition-analysis

# Using conda (recommended)
conda env create -f environment.yml
conda activate cta

# Or pip
pip install -r requirements.txt

# Run the first exploration notebook
jupyter notebook notebooks/01_eeg_exploration.ipynb
```

**Core dependencies:** `numpy`, `scipy`, `pandas`, `mne` (EEG), `yfinance`, `matplotlib`, `seaborn`, `statsmodels`

---

## 📈 Current Status

- [x] Project scaffolding
- [x] EEG nomenclature primer
- [ ] CHB-MIT dataset ingestion pipeline
- [ ] Rolling variance & AR1 implementation
- [ ] First side-by-side seizure vs crash comparison
- [ ] DFA (Detrended Fluctuation Analysis) module
- [ ] Composite early warning score
- [ ] Statistical validation across multiple events

---

## 📚 Key References

- Scheffer et al. (2009). *Early-warning signals for critical transitions.* Nature.
- Dakos et al. (2012). *Methods for detecting early warnings of critical transitions in time series.* PLOS ONE.
- Kramer et al. (2012). *Human seizures self-terminate across spatial scales via a critical transition.* PNAS.
- Haldane & May (2011). *Systemic risk in banking ecosystems.* Nature.
- Sornette (2003). *Why Stock Markets Crash: Critical Events in Complex Financial Systems.*

---

## 🤝 Contributing

This is an exploratory research project — ideas, domain knowledge, and dataset suggestions are very welcome. If you work in epileptology, computational neuroscience, or quantitative finance and find this interesting, open an issue or reach out.

---

## 📝 License

MIT License — see `LICENSE` for details.

---

*Built out of curiosity. The mathematics of collapse might be universal.*
