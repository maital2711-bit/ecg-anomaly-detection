# ECG Anomaly Detection

Finds abnormal heartbeats in ECG recordings using an autoencoder trained only on normal beats.

## Why it matters
A 24-hour heart monitor records about 100,000 beats, too many for a doctor to review one by one.
This model flags unusual beats for review.

## How it works
1. Train the autoencoder to rebuild normal beats
2. Normal beat: small rebuild error
3. Abnormal beat: large rebuild error, so it gets flagged

## Data
[MIT-BIH Arrhythmia Database](https://physionet.org/content/mitdb/)

## Model
- Linear autoencoder in PyTorch: 250 → 128 → 32 → 128 → 250
- Trained on normal beats only
- Flagging threshold: 95th percentile of validation errors on normal beats

## Results
| Test split | AUC | Recall | Precision | F1 |
|---|---|---|---|---|
| Split A | 0.873 | 0.80 | 0.56 | 0.66 |
| Split B | 0.946 | 0.92 | 0.78 | 0.84 |

Results change depending on which patients are in the test set.

## Findings
- PVC beats are detected very well because their shape is clearly different
- PAC and junctional beats are harder because their shape looks normal and mainly their timing differs

## Next steps
- Conv1d denoising autoencoder
- KNN distance in latent space
- RR timing score to help detect PAC beats
- Ensemble of the detectors
- 5-fold cross-validation by patient

## How to run
Open `ECG_Anomaly_Detection_v2.ipynb` in Google Colab

## Limitations
Educational project, not for clinical use.

## Author
Mai Siton
