# ECG-Arrhythmia-Detection
ECG arrhythmia classification using signal processing, feature engineering, and machine learning. Includes ECG preprocessing, R-peak detection, heartbeat segmentation, and model evaluation.
# ECG Arrhythmia Classification

This project uses ECG signals from the MIT-BIH Arrhythmia Database to classify heartbeats as normal or abnormal using machine learning.

## What I did

* Loaded ECG recordings and annotations using WFDB.
* Detected R-peaks to identify individual heartbeats.
* Compared a simple threshold-based peak detector with methods available in NeuroKit2.
* Extracted features such as RR intervals, peak amplitude, and beat width.
* Trained a Random Forest classifier using the extracted features.
* Evaluated the model using accuracy, precision, recall, F1-score, and a confusion matrix.

## Dataset

**MIT-BIH Arrhythmia Database**

The dataset contains annotated ECG recordings used for studying cardiac arrhythmias.

Dataset: https://physionet.org/content/mitdb/1.0.0/

The recordings are accessed using the WFDB Python library.

## Features Used

* **Pre-beat RR interval:** Time between the previous R-peak and the current R-peak.
* **Post-beat RR interval:** Time between the current R-peak and the next R-peak.
* **Peak amplitude:** ECG signal amplitude at the detected R-peak.
* **Beat width:** Approximate width of the heartbeat based on the signal amplitude.

## Model

I used a Random Forest classifier to classify heartbeats into two categories:

* Normal
* Abnormal

The model uses features extracted from the ECG signal, with reference labels obtained from the database annotations.

## Results

The current notebook reports:

* Accuracy: 97%
* Normal beat precision: 99%
* Abnormal beat precision: 93%
* Abnormal beat recall: 97%

The notebook also includes a confusion matrix and classification report.

These results are preliminary. The current evaluation uses a random beat-level split from the same ECG recording, so performance on unseen patients has not yet been established.

## Peak Detection

Initially, I used `scipy.signal.find_peaks()` with a fixed threshold. It worked reasonably well on one recording but missed several peaks in another recording containing arrhythmias.

I then tested R-peak detection methods available through NeuroKit2, including the Pan-Tompkins method.

This improved detection sensitivity on the challenging recording and showed why peak detection is an important part of the overall pipeline.

## Libraries

* Python
* NumPy
* SciPy
* WFDB
* NeuroKit2
* scikit-learn
* Matplotlib

## How to Run

Install the required libraries:

```bash
pip install wfdb neurokit2 numpy scipy scikit-learn matplotlib
```

Open `ecg_arrhythmia_classifier.ipynb` in Jupyter Notebook and run the cells in order.

An internet connection is required to access the ECG recordings from PhysioNet.

## Limitations and Future Work

* Test the model on additional ECG recordings.
* Use record-wise or patient-wise evaluation.
* Extract more features describing QRS morphology.
* Compare Random Forest with Logistic Regression and SVM.
* Investigate the effect of noise on classification performance.

## Disclaimer

This is an educational project and is not intended for clinical diagnosis.
