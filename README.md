# XAI-Project: Sentiment Analysis with Explainability

This project implements a sentiment analysis pipeline using the fine-tuned `vinai/bertweet-base` model on the Sentiment140 dataset, following the CRISP-DM methodology. The core objective is to systematically compare two XAI (Explainable AI) frameworks—SHAP and Captum—across four dimensions: token agreement, faithfulness (deletion AUC), robustness under perturbations, and computational efficiency. Results demonstrate that SHAP provides superior faithfulness (73% above threshold) and robustness (ρ ≈ 0.75), while Captum offers 2.3× faster inference, suggesting a hybrid deployment strategy for production use cases.

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
   - Navigate to `notebooks/` and execute `1_Business_Understanding.ipynb` through `6_Deployment.ipynb` sequentially
   - The pipeline trains the model, generates predictions, and produces XAI evaluation metrics

## Project Structure

```
├── notebooks/
│   ├── 1_Business_Understanding.ipynb
│   ├── 2_Data_Understanding.ipynb
│   ├── 3_Data_Preparation.ipynb
│   ├── 4_Modeling.ipynb
│   ├── 5_Evaluation.ipynb
│   └── 6_Deployment.ipynb
├── data/                     # Dataset files (not tracked)
├── models/                   # Trained models (not tracked)
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.10+
- PyTorch 2.0+
- Transformers 4.57+
- SHAP, Captum, Pandas, Matplotlib, Seaborn
- See `requirements.txt` for full dependencies

## Key Results

- **Model Performance:** Fine-tuned BERTweet achieves strong sentiment classification
- **XAI Comparison:** SHAP excels in faithfulness/robustness; Captum wins on speed
- **Deployment Insight:** Hybrid approach recommended (Captum for real-time, SHAP for audits)
