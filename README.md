# H-FADF: Hybrid Fake Account Detection Framework

A machine learning and deep learning framework for detecting fake social media accounts by combining account-level metadata, behavioural features, and tweet-sequence patterns.

## Overview

Fake social media accounts can be used for spam, impersonation, automated manipulation, and other suspicious activities. H-FADF uses a hybrid classification approach to distinguish genuine accounts from fake accounts by combining the strengths of multiple models.

The framework integrates **Random Forest, Long Short-Term Memory (LSTM), and Logistic Regression** into a stacked ensemble architecture. It also provides detailed performance evaluation, threshold analysis, and error analysis to understand how effectively the models identify suspicious accounts.

## Key Features

- **Behavioural feature engineering:** Extracts account age, follower-to-friend ratio, posting frequency, URL usage, hashtags, mentions, retweets, replies, and posting-time patterns.
- **Random Forest classifier:** Analyses structured account metadata and aggregated behavioural features.
- **LSTM classifier:** Learns sequential patterns from the most recent 30 tweets associated with each account.
- **Stacked ensemble:** Combines the predictions of Random Forest and LSTM using Logistic Regression.
- **Leakage-aware training:** Uses out-of-fold predictions to train the stacking model.
- **Comprehensive evaluation:** Measures Precision, Recall, F1-score, ROC-AUC, and Average Precision.
- **Visual analytics:** Generates ROC curves, precision-recall curves, confusion matrices, feature importance plots, score distributions, and threshold comparisons.
- **Error analysis:** Examines false positives, missed fake accounts, and detection performance across fake-account categories.

## Model Architecture

The framework consists of three main components:

### 1. Random Forest

Uses structured account-level features, including account age, follower counts, friend counts, posting frequency, profile information, and aggregated tweet behaviour.

### 2. LSTM (Long Short-Term Memory)

Processes sequences of tweet-level features to learn temporal and behavioural patterns that may help distinguish fake accounts from genuine ones.

### 3. Logistic Regression Stacker

Combines the probability predictions from Random Forest and LSTM into a final classification score. The stacker is trained on out-of-fold predictions to reduce information leakage during training.

**Workflow:**

`Dataset → Feature Engineering → Random Forest + LSTM → Logistic Regression Stacker → Fake Account Probability → Evaluation`

## Dataset Requirements

The notebook expects a dataset archive named `fake_account_dataset.zip`, containing the following CSV files:

- `users.csv` — Account-level metadata and profile information.
- `tweets.csv` — Tweet-level data, including timestamps, user IDs, URLs, hashtags, mentions, retweets, and replies.

The dataset should also provide account labels and, where applicable, fake-account categories used for evaluation.

**Note:** The dataset is not included in this repository by default. You must provide the required archive separately before running the notebook.

## Technologies Used

- Python
- Jupyter Notebook / Google Colab
- Pandas and NumPy
- Scikit-learn
- TensorFlow / Keras
- Matplotlib

## How to Run

The notebook is designed to run in Google Colab.

1. Open `Fake_Account_Detection_Code.ipynb` from this repository.
2. Select **Open in Colab**, or upload the notebook to [Google Colab](https://colab.research.google.com/).
3. Upload `fake_account_dataset.zip` when prompted by the notebook.
4. Run the cells sequentially, from the dataset loading section through the evaluation sections.
5. Review the model comparison tables, plots, feature importance, threshold analysis, and error analysis.

### Dependencies

The notebook uses the following Python libraries:

```bash
pip install numpy pandas matplotlib scikit-learn tensorflow
```

Google Colab generally provides these libraries already, although versions may vary.

## Evaluation Metrics

The notebook evaluates the individual models and the hybrid framework using:

| Metric | Purpose |
|---|---|
| Precision | Measures how many accounts flagged as fake are actually fake. |
| Recall | Measures how many fake accounts are correctly detected. |
| F1-score | Balances precision and recall. |
| ROC-AUC | Measures how well the model separates the two classes across thresholds. |
| Average Precision | Summarises precision-recall performance. |
| Confusion Matrix | Shows correct predictions, false alarms, and missed fake accounts. |

The notebook also compares model performance by fake-account category, analyses feature importance, and explores alternative decision thresholds.

## Project Objectives

- Investigate whether combining structured account features with sequential tweet behaviour improves fake-account detection.
- Compare the performance of individual models against a stacked hybrid model.
- Analyse the trade-off between false positives and missed fake accounts.
- Identify behavioural features that contribute to model predictions.

## Limitations

- Detection quality depends on the dataset's coverage, label quality, and representativeness.
- Behavioural patterns can overlap between genuine and fake accounts.
- Performance on the supplied test split does not guarantee generalisation to new platforms or changing attack patterns.
- Model predictions indicate suspicious patterns and should not be treated as definitive proof that an account is fake.

## Repository Contents

- `Fake_Account_Detection_Code.ipynb` — Notebook containing data preparation, feature engineering, model training, evaluation, and visualisations.
- `README.md` — Project overview, setup instructions, model architecture, and evaluation details.

## Conclusion

H-FADF explores a stacked ensemble approach to fake social media account detection by combining structured behavioural analysis with sequential tweet modelling. Its evaluation and error-analysis components help assess model performance and understand the practical trade-offs involved in identifying suspicious accounts.
