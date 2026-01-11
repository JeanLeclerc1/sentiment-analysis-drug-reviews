# Sentiment Analysis of Patient Drug Reviews

This project explores sentiment patterns in patient-written drug reviews using an end-to-end natural language processing (NLP) workflow. It combines exploratory data analysis, lexicon-based sentiment scoring, and transformer-based embeddings to evaluate how well different approaches capture sentiment in medical narratives.

The focus is on comparing a lightweight baseline (VADER) against domain-specific transformer embeddings (Bio_ClinicalBERT) paired with a traditional classifier.

---

## Project Overview

The notebook demonstrates the following workflow:

- Construction of a unified review text field from multiple review components
- Exploratory analysis of ratings, medical conditions, and drugs
- Binary sentiment labeling derived from numeric ratings (as a proxy)
- Lexicon-based sentiment analysis using VADER
- Transformer-based embeddings using Bio_ClinicalBERT
- Logistic Regression classifier trained on top of frozen embeddings
- Comparative analysis of score distributions and model behavior

Because numeric ratings are used as sentiment labels, some label noise is expected. This mirrors real-world scenarios where explicit sentiment annotations are unavailable.

---

## Repository Structure

```text
sentiment-analysis-drug-reviews/
│
├── notebooks/
│   └── sentiment_analysis_drug_reviews.ipynb
│
├── data/
│   └── README.md
│
└── README.md
```

---

## Dataset

This project uses the **DrugLib patient drug review dataset**, which provides separate train and test splits and includes multiple free-text review fields per patient.

### Important
The dataset is **not redistributed** in this repository due to licensing and redistribution restrictions.

To run the notebook locally:
1. Obtain the DrugLib dataset from its original source
2. Place the files in a local directory (e.g. `drug+review+dataset+druglib+com/`)
3. Update the `data_path` variable in the notebook if needed

The original train/test split provided by the dataset is preserved and tracked via a `split` column.

---

## Methods

### Sentiment Labels
- Ratings > 5 → **positive**
- Ratings ≤ 5 → **negative**

These labels serve as a proxy for sentiment rather than gold-standard annotations.

### Models
- **VADER**  
  Lexicon-based sentiment analysis used as a lightweight baseline.

- **Bio_ClinicalBERT + Logistic Regression**  
  Reviews are encoded using Bio_ClinicalBERT as a frozen encoder.  
  A Logistic Regression classifier is trained on the resulting embeddings.

Batch encoding is used to improve inference efficiency and GPU utilization when available.

---

## Key Observations

- VADER compound scores show substantial overlap between positive and negative reviews, reflecting the difficulty of rule-based sentiment analysis in medical text.
- Bio_ClinicalBERT embeddings produce better separation between sentiment classes, particularly for positive reviews.
- Negative sentiment remains harder to classify, likely due to nuanced patient narratives and class imbalance.
- Using ratings as sentiment labels introduces unavoidable noise, but still allows meaningful comparative analysis.

---

## Requirements

Core dependencies include:

- Python 3.9+
- pandas, numpy
- scikit-learn
- matplotlib, seaborn
- nltk
- torch
- transformers

The notebook will automatically use a GPU for embedding inference if available.

---

## Notes

This repository is intended to demonstrate:
- NLP preprocessing and feature construction
- Practical sentiment modeling decisions
- Awareness of data leakage and evaluation boundaries
- Performance and efficiency considerations (batching, GPU usage)

It is designed as a portfolio-style project rather than a packaged library.

---

## Author

Jean Leclerc
