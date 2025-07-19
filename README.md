# Spotify Streaming Analysis 2024

This project explores the most streamed Spotify songs of 2024 using data from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/most-streamed-spotify-songs-2024). It combines data cleaning, exploratory data analysis (EDA), and classification modeling to uncover trends in music popularity, cross-platform engagement, and the characteristics of explicit content.

---

## Objectives

- Understand the popularity and distribution of artists and songs  
- Analyze music release trends by year and month  
- Explore cross-platform relationships between streaming metrics (Spotify, YouTube, TikTok, Shazam)  
- Predict whether a track is explicit based on streaming and release patterns  
- Reflect on statistical concepts (e.g. ROC, coefficient analysis) via interpretable models

---

## Dataset

- Source: [Kaggle – Most Streamed Spotify Songs 2024](https://www.kaggle.com/datasets/nelgiriyewithana/most-streamed-spotify-songs-2024)  
- Includes streams/views/likes across Spotify, YouTube, TikTok, Shazam, Pandora, and more  
- Contains metadata like track name, artist, release date, and explicit flag

---

## Key Analysis Highlights

### Exploratory Data Analysis
- Top artists and most streamed songs on Spotify and YouTube  
- Month-wise release trends and artist streaming averages  
- Cross-platform scatterplots (e.g. TikTok Views vs Spotify Streams)  
- Distribution of explicit vs. non-explicit songs (via boxplots)

---

## Classification Modeling: Predicting Explicit Content

The target variable is **explicit content** (binary: 1 = explicit, 0 = not explicit). However, the dataset shows a **class imbalance**, with more non-explicit tracks. To address this and avoid biased predictions, both models were trained using **`class_weight='balanced'`**, which adjusts for this skew by weighting minority class samples more heavily.

### Models Used

- **Balanced Random Forest**
  - Robust and interpretable with strong overall performance  
  - Automatically balances class weights during training  
  - Captures key predictors like Shazam Counts, YouTube Likes, and TikTok activity

- **Balanced Logistic Regression**
  - Interpretable model with strong recall for explicit tracks  
  - Useful for coefficient-based insights and statistical diagnostics  
  - Prioritizes identifying explicit content even at the cost of precision

_Balanced model selection helps ensure fairer evaluation and better generalization for minority-class (explicit) detection._

---

## Results Summary (Balanced Models)

| Model                      | Accuracy | Recall (Explicit) | AUC  | Notes                          |
|----------------------------|----------|-------------------|------|--------------------------------|
| Balanced Random Forest     | 67%      | 0.39              | 0.70 | Most balanced overall          |
| Balanced Logistic Regression | 51%    | 0.72              | 0.59 | High recall, low precision     |

Both models outperform a baseline majority-class predictor and uncover meaningful patterns behind explicit labeling.

---

## ROC Curve Evaluation

To compare the models across thresholds, ROC curves were plotted:

- **Random Forest**: AUC ≈ 0.70 — good separation between classes  
- **Logistic Regression**: AUC ≈ 0.59 — less separation but better recall  
- ROC helps visualize trade-offs between **true positive rate (recall)** and **false positive rate**, independent of a 0.5 threshold

---

## Tools & Libraries
- Python, Pandas, NumPy  
- Seaborn, Matplotlib  
- Scikit-learn (classification models, metrics, preprocessing)

---

## Key Insights

- **Virality matters**: Tracks with more TikTok and YouTube activity tend to have more Spotify streams  
- **Explicit content thrives**: Explicit songs are common among top-streamed tracks, defying the idea that they perform worse  
- **Shazam Counts** were one of the strongest predictors of explicit labeling — likely reflecting discoverability of edgy content  
- **Balanced models** helped uncover these insights without being biased toward the majority class
