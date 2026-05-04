# 🧠📉 Critical Transitions: EEG vs Financial Markets

> **Do a brain about to seize and a stock market about to crash follow the same mathematical warning patterns?**

This project applies **Critical Transition Theory** — a framework from physics and ecology — to two completely different complex systems: epileptic brain signals (EEG) and the S&P 500 index before the 2008 Lehman Brothers collapse.

---

## 🔬 The Core Hypothesis

> Brain activity before a seizure and stock market prices before a crash both exhibit the same universal mathematical warning signals as they approach a tipping point.

This idea comes from a field called **Complex Systems Science**. The theory is called **Critical Slowing Down (CSD)** — and it predicts that *any* complex system near a collapse will show measurable warning signs, regardless of whether it's biological, financial, or ecological.

---

## 📐 What is Critical Slowing Down?

When a complex system (brain, market, ecosystem) nears a **critical transition** (seizure, crash, extinction), it loses its ability to bounce back from small disturbances. This shows up mathematically as:

| Warning Signal | What it means | Why it rises |
|---|---|---|
| **Variance ↑** | Fluctuations grow bigger | System is less stable, wobbles more |
| **Lag-1 Autocorrelation ↑** | The system's memory gets longer | Recovery from shocks becomes slower |
| **\|Skewness\| ↑** | The distribution becomes lopsided | System is being pushed asymmetrically toward the tipping point |

These are called **Early Warning Signals (EWS)**.

---

## 📦 Datasets Used

| Dataset | Source | What it is |
|---|---|---|
| **CHB-MIT EEG** | [PhysioNet](https://physionet.org/content/chbmit/) | Real pediatric epilepsy EEG recordings with annotated seizure timestamps |
| **S&P 500** | Yahoo Finance (`yfinance`) | Daily OHLCV price data from 2006–2009 covering the Lehman Brothers collapse |

If PhysioNet or Yahoo Finance is unreachable, the code automatically generates **physiologically grounded synthetic data** that mimics the real signals.

---

## 🗂️ Directory Structure

```
critical-transitions-eeg-vs-market/
│
├── README.md                          ← You are here
│
├── notebook/
│   └── critical_transitions_eeg_vs_market.ipynb   ← Main analysis notebook
│
├── outputs/
│   └── critical_transitions_results.png           ← Auto-generated result figure
│
├── requirements.txt                   ← Python dependencies
└── .gitignore                         ← Ignore cache, outputs, etc.
```

---

## ⚙️ Setup & Usage

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/critical-transitions-eeg-vs-market.git
cd critical-transitions-eeg-vs-market
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebook
```bash
jupyter notebook notebook/critical_transitions_eeg_vs_market.ipynb
```

Run all cells from top to bottom. The final figure is saved as `outputs/critical_transitions_results.png`.

---

## 📊 What the Code Does — Step by Step

### Step 0 — Install dependencies
Installs `yfinance`, `wfdb`, `scipy`, `matplotlib`, `seaborn`, `pandas`, `numpy` if not already present.

### Step 1 — Imports & Styling
Loads all libraries and sets a dark terminal-style plot theme using `matplotlib.rcParams`.

### Step 2 — Load EEG Data
Streams the CHB-MIT pediatric EEG recording `chb01/chb01_03` from PhysioNet using the `wfdb` library. This is a real recording from a child with epilepsy, sampled at 256 Hz. Seizure onset is at ~2996 seconds.  
If PhysioNet is unavailable, a synthetic 4-phase signal is generated: *interictal (normal) → pre-ictal (building) → ictal (seizure) → post-ictal (recovery)*.

### Step 3 — Load S&P 500 Data
Downloads daily closing prices from 2006–2009 via `yfinance`. Computes **log returns** (the standard way to measure daily price changes in finance). The crash event is Lehman Brothers' collapse on **September 15, 2008**.

### Step 4 — EWS Helper Functions
Three functions:
- `compute_ews(series, window, step)` — slides a rolling window over the signal and computes **variance**, **autocorrelation**, and **skewness** at each position
- `kendall_tau(series)` — computes the **Kendall's Tau** statistic, which measures whether a signal is trending upward (positive τ means rising trend)
- `norm01(array)` — normalizes values to [0, 1] so EEG and market metrics can be visually compared on the same scale

Then applies these to:
- **EEG**: 10-minute pre-seizure window, downsampled 10×, rolling window of 500 points (~20 seconds)
- **Market**: 250 trading days before the crash, rolling window of 30 days

### Step 5 — Visualization
Generates a 5-row, 3-column figure:
- **Row 0**: Raw EEG signal and S&P 500 price chart
- **Rows 1–3**: Variance, Autocorrelation, |Skewness| for EEG (left), Market (center), Overlay (right) — each with a trend line and Kendall tau value
- **Row 4**: Verdict table — color-coded summary of all 6 EWS metrics and whether the hypothesis holds

### Conclusion Cell
Prints a structured text summary of: hypothesis, assumptions, caveats, next steps, and references.

---

## 📈 Results Interpretation

The **Verdict row** shows Kendall's τ for each of the 6 metric × system combinations:

| τ value | Meaning |
|---|---|
| > 0.3 | **Strong rising trend** — strong support for CSD |
| 0.1 – 0.3 | **Moderate rising trend** |
| 0 – 0.1 | **Weak rising trend** |
| < 0 | **No support** |

p-value < 0.05 (green) means the trend is statistically significant.

---

## ⚠️ Assumptions & Caveats

- This is a **single-event study** (1 seizure, 1 crash) — not enough to make general claims
- **Hindsight bias** — we already knew when the events happened, so windows were chosen accordingly
- EEG uses only one frontal channel — full network dynamics are not captured
- Market crashes have external causes (policy, geopolitics) that CSD models don't account for
- Rising EWS does **not** guarantee an upcoming collapse — false positives exist

---

## 🔭 Future Work

- Test across 20+ seizures and 5+ market crashes
- Add spectral EWS: Hurst exponent, 1/f power-law slope
- Apply graph-based EWS on full 23-channel EEG network
- Extend to climate or ecological tipping points

---

## 📚 References

- Scheffer et al. (2009) *Nature* 461:53–59 — CSD theory
- Dakos et al. (2008) *PNAS* — Kendall tau EWS methodology
- Meisel & Kuehn (2012) *PLOS ONE* — CSD before epileptic seizures
- Goldberger et al. (2000) *Circulation* — PhysioNet / CHB-MIT database

---

## 🛠️ Requirements

```
numpy
pandas
matplotlib
scipy
seaborn
yfinance
wfdb
jupyter
```

See `requirements.txt` for pinned versions.

---

*Built as an exploratory data science project applying complexity theory across neuroscience and finance.*
