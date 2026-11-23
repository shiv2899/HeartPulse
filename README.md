# HeartPulse - Heart Arrhythmia Detection from ECG Signals

ECG heartbeat classification using 1D-CNN. No leakage - Train and Test patients are completely different.

> Built a 1D-CNN for ECG arrhythmia detection on MIT-BIH data, using patient-level splits to prevent data leakage.

## Why Patient-wise Split?
Most projects split by heartbeat - same patient in Train and Test = Fake 99% accuracy.
This project splits by PATIENT - DS1 (22 patients) for Train, DS2 (22 patients) for Test.
Test patients are never seen during training.

## Dataset
- MIT-BIH Arrhythmia Database - PhysioNet
- 48 patients, 100,699 beats (187 points per beat)
- Train: 51,008 beats (22 patients), Test: 49,691 beats (22 patients)
- Classes: N=Normal, S=Supraventricular, V=Ventricular, F=Fusion (Q removed - only 8 samples in Train)

## Results - BEST MODEL
- Overall Accuracy (Unseen Patients): 93.34% (Epoch 2)
- Macro F1: 0.47 - This is the honest number, Accuracy is inflated by N class (89% of data)
- N: Precision 0.94, Recall 0.99 - Excellent
- V: 2689 / 3220 correctly detected
- S and F: Weak due to severe imbalance (S=1837, F=388 vs N=44246) - Model predicts them as N

## What I Learned
- Accuracy alone is misleading on imbalanced medical data
- Confusion Matrix matters more than Accuracy
- Class imbalance cannot be fixed by Class Weights alone when samples are <400

## How to Run
1. Open `01_ecg_arrhythmia_setup_and_training.ipynb` in Google Colab
2. Enable T4 GPU
3. Run all cells in order
