# XAI-Project: Sentiment Analysis with Explainability

**Note:** While this README is in English, the Jupyter Notebooks and detailed analysis within this repository are written in **German**.

This project implements a sentiment analysis pipeline using the fine-tuned `vinai/bertweet-base` model on the Sentiment140 dataset, following the CRISP-DM methodology. The core objective is to systematically compare two XAI (Explainable AI) frameworks—SHAP and Captum—across four dimensions: token agreement, faithfulness (deletion AUC), robustness under perturbations, and computational efficiency.

**Key Findings:**
The evaluation reveals that **SHAP** significantly outperforms Captum in terms of explanation quality (faithfulness and robustness), while **Captum** offers a moderate speed advantage. Specifically:
- **Faithfulness:** SHAP explanations are highly faithful (Mean Deletion-AUC Ratio ~6.9x), whereas Captum performs close to random baseline.
- **Robustness:** SHAP is moderately robust to text perturbations (ρ ≈ 0.60), while Captum rankings are unstable (ρ ≈ 0.04).
- **Efficiency:** Captum is approximately 1.4x faster than SHAP, which is less than the hypothesized 2x speedup.

## Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sean-mas/XAI-Project.git
   cd XAI-Project
   ```

2. **Create virtual environment and install dependencies:**
   ```bash
   python3 -m venv venv_Machine_Learning
   source venv_Machine_Learning/bin/activate  # On Windows: venv_Machine_Learning\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Download data:**
   - Download [Sentiment140 dataset](http://help.sentiment140.com/for-students) and place CSV files in `data/` directory

4. **Run notebooks in order:**
   - Navigate to `notebooks/` and execute `1_Business_Understanding.ipynb` through `6_Deployment.ipynb` sequentially.
   - The pipeline trains the model, generates predictions, and produces XAI evaluation metrics.

## Project Structure

```
├── notebooks/
│   ├── 1_Business_Understanding.ipynb  # (German) Project goals & XAI definition
│   ├── 2_Data_Understanding.ipynb      # (German) EDA of Sentiment140
│   ├── 3_Data_Preparation.ipynb        # (German) Cleaning & Tokenization
│   ├── 4_Modeling.ipynb                # (German) Fine-tuning BERTweet
│   ├── 5_Evaluation.ipynb              # (German) SHAP vs. Captum analysis
│   └── 6_Deployment.ipynb              # (German) Production architecture
├── data/                               # Dataset files (not tracked)
├── models/                             # Trained models (not tracked)
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.10+
- PyTorch 2.0+
- Transformers 4.57+
- SHAP, Captum, Pandas, Matplotlib, Seaborn
- See `requirements.txt` for full dependencies

## Key Results & Deployment

- **Model Performance:** Fine-tuned BERTweet achieves strong sentiment classification.
- **XAI Comparison:**
    - **Agreement:** Low overlap (~50%) between SHAP and Captum.
    - **Faithfulness:** SHAP excels (64% of samples > 1.5x AUC ratio).
    - **Robustness:** SHAP is significantly more robust than Captum.
    - **Efficiency:** Captum provides a 1.37x speedup over SHAP.
- **Deployment Strategy:** A **hybrid microservices architecture** is recommended:
    - **Synchronous Path:** Uses Captum for real-time, low-latency feedback in user interfaces.
    - **Asynchronous Path:** Uses SHAP for high-precision, audit-grade explanations in background workers.
