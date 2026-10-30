# Verification Theater: Confidence-Calibration Simulation

> **All data in this repository are simulated.** This notebook is a design probe, not a human-subject study, and it makes no empirical claims about AI systems or users.

## Purpose

This notebook explores a system-side question related to my research project [Verification Theater](https://github.com/its25sensei/verification-theater): how far an AI system's **stated confidence** can diverge from its **actual accuracy**, and how that gap can be measured.

It compares two simulated conditions:

| Condition | How the data are generated |
| --- | --- |
| **A · Overconfident** | Stated confidence is drawn from 0.70–0.99; the probability of a correct outcome is set 0.25 below the stated confidence. |
| **B · Confidence-matched** | Stated confidence is drawn from 0.50–0.95; the probability of a correct outcome equals the stated confidence. |

## What It Measures

- **Expected calibration error (ECE):** the weighted average gap between stated confidence and observed accuracy across five equal-width confidence bins. Lower values indicate closer agreement.
- **Calibration curve:** observed accuracy plotted against stated confidence for each condition, compared with the diagonal of perfect calibration.

## Results from One Simulated Run

Random seed 42, 200 simulated observations per condition:

| Condition | Observed accuracy | ECE |
| --- | --- | --- |
| A · Overconfident | 0.565 | 0.275 |
| B · Confidence-matched | 0.760 | 0.026 |

The gap between conditions exists because it was built into the simulated data. These values are estimates from a single finite sample, not fixed properties of either condition.

## Scope and Limitations

- The notebook measures **model-side calibration only**. It does not measure users' trust, verification behavior, or decision quality.
- With 200 observations and five fixed-width bins, observations are unevenly distributed across bins, and estimates can shift between runs. Repeated simulations or bootstrap intervals would be needed before making stronger comparisons.

## Connection to Verification Theater

Verification Theater asks whether citation-like cues increase users' trust in AI recommendations even when the cited evidence cannot be traced. Stated confidence is a related cue: like a citation, it can signal reliability without guaranteeing it.

This probe isolates the system side of that problem. The open question it leads to is the one that connects the two projects: **does a better-calibrated system actually help users calibrate their trust, and how should a model-side metric such as ECE be linked to user-side outcomes?**

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook ECE_Project.ipynb
```

## Repository Structure

```text
.
├── ECE_Project.ipynb   # Simulation, ECE calculation, and calibration curve
├── requirements.txt
└── README.md
```
