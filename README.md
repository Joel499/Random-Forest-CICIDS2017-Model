# Random Forest Intrusion Detection System (CICIDS2017)

## Overview
A machine learning-based Network Intrusion Detection System (IDS) trained on the 
CICIDS2017 dataset. This project uses Random Forest classification with SHAP 
explainability to detect FTP-Patator and SSH-Patator brute force attacks.

## Results
| Model | Accuracy | False Negatives |
|-------|----------|-----------------|
| Random Forest | 99.99% | 1 |

## Dataset
- **Source:** Canadian Institute for Cybersecurity (CICIDS2017)
- **Link:** https://www.unb.ca/cic/datasets/ids-2017.html
- **Day used:** Tuesday (FTP-Patator & SSH-Patator attacks)
- **Total samples:** 445,909
- **Features:** 78 network traffic features

## Project Structure
```
ids-phd-project/
├── notebooks/
│   └── 01_eda.ipynb        # Main analysis notebook
├── models/
│   └── random_forest_model.pkl  # Saved trained model
├── outputs/
│   ├── class_distribution.png   # Class distribution chart
│   ├── confusion_matrix.png     # Model performance matrix
│   ├── shap_summary.png         # SHAP feature importance
│   └── experiment_results.json  # Experiment metrics
└── README.md
```

## Key Findings
- Random Forest achieved **99.99% accuracy** on Tuesday's dataset
- **Destination Port** was the most influential feature for FTP attack detection
- Low destination port values (port 21) strongly indicated FTP-Patator attacks
- Model correctly identified all FTP-Patator attacks with zero false positives
- 1 SSH-Patator attack was misclassified as BENIGN (false negative)

## Explainability (SHAP)
SHAP (SHapley Additive exPlanations) was used to explain model predictions:
- Top features for FTP detection: Destination Port, Max Packet Length, Bwd Header Length
- Low destination port values (port 21) strongly pushed toward FTP attack prediction
- Most features cluster near zero SHAP value, suggesting the model relies on a 
  small subset of highly discriminative features

## Setup & Installation
1. Clone this repository:
```
git clone https://github.com/Joel499/Random-Forest-CICIDS2017-Model.git
```

2. Create a virtual environment:
```
python -m venv venv
.\venv\Scripts\activate
```

3. Install dependencies:
```
pip install -r requirements.txt
```

4. Download the CICIDS2017 dataset from:
https://www.unb.ca/cic/datasets/ids-2017.html
Extract into the `data/` folder.

5. Open and run `notebooks/01_eda.ipynb`

## Dependencies
- Python 3.11
- PyTorch 2.11.0
- scikit-learn
- pandas
- numpy
- shap
- matplotlib
- seaborn
- xgboost

## Future Work
- Test on all 5 days of CICIDS2017 dataset
- Compare with XGBoost and Deep Learning models
- Address class imbalance using SMOTE
- Deploy as a real-time network monitoring tool

