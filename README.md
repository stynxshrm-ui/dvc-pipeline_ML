Here's a comprehensive description and README for your GitHub repository:

# IMDB Sentiment Analysis Pipeline with DVC

A complete, reproducible machine learning pipeline for sentiment analysis on the IMDB movie review dataset using DVC (Data Version Control) for pipeline orchestration and versioning.

## Overview

This project implements a sentiment analysis classifier that predicts whether an IMDB movie review is positive or negative. The pipeline is structured into four main stages using DVC:

1. **Data Preparation** - Splits raw data into train/test sets
2. **Feature Engineering** - Transforms text data into numerical features
3. **Model Training** - Trains a sentiment classification model
4. **Model Evaluation** - Evaluates performance and saves metrics

## Project Structure

```
dvc-pipeline_ML/
├── archive/                    # Data and artifacts directory
│   ├── imdb-dataset.csv       # Raw IMDB dataset (not tracked by git)
│   ├── train.csv              # Training data (DVC-tracked)
│   ├── test.csv               # Testing data (DVC-tracked)
│   ├── train.joblib           # Training features (DVC-tracked)
│   ├── test.joblib            # Testing features (DVC-tracked)
│   ├── model.joblib           # Trained model (DVC-tracked)
│   └── results.yaml           # Evaluation metrics (DVC-tracked)
├── prepare_data.py            # Stage 1: Data preparation script
├── make_features.py           # Stage 2: Feature extraction script
├── train.py                   # Stage 3: Model training script
├── evaluate.py                # Stage 4: Model evaluation script
├── params.yaml                # Pipeline parameters
└── dvc.yaml                   # DVC pipeline definition
```


### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/imdb-sentiment-pipeline.git
   cd imdb-sentiment-pipeline
   ```

2. **Install dependencies**
   ```bash
   pip install pandas numpy scikit-learn nltk dvc joblib pyyaml
   ```

3. **Download the IMDB dataset**
   - Download the dataset from [Kaggle IMDB Dataset](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)
   - Place `IMDB Dataset.csv` in `archive/imdb-dataset.csv`

4. **Run the pipeline**
   ```bash
   dvc repro
   ```
## DVC Commands

| Command | Description |
|---------|-------------|
| `dvc init` | Initialize DVC in project |
| `dvc repro` | Reproduce pipeline |
| `dvc status` | Show changed stages |
| `dvc metrics show` | Display evaluation metrics |
| `dvc dag` | Visualize pipeline DAG |
| `dvc push` | Push DVC-tracked files to remote |
| `dvc pull` | Pull DVC-tracked files from remote |


## Pipeline Stages

### Stage 1: Data Preparation (`prepare_data.py`)
- Loads raw IMDB dataset
- Performs train-test split (configurable ratio)
- Saves `train.csv` and `test.csv`

### Stage 2: Feature Extraction (`make_features.py`)
- Converts text reviews to numerical features
- Applies text preprocessing (lowercase, punctuation removal, etc.)
- Extracts features using TF-IDF vectorization
- Saves features as `train.joblib` and `test.joblib`

### Stage 3: Model Training (`train.py`)
- Trains a Logistic Regression classifier
- Uses features from training set
- Saves trained model as `model.joblib`

### Stage 4: Model Evaluation (`evaluate.py`)
- Evaluates model on test set
- Calculates accuracy, precision, recall, F1-score
- Saves metrics to `results.yaml`


## Running the Pipeline

### Execute full pipeline
```bash
dvc repro
```

### Run specific stage
```bash
dvc repro prepare_data
dvc repro make_features
dvc repro train
dvc repro evaluate
```

### Visualize pipeline
```bash
dvc dag
```

### Check pipeline status
```bash
dvc status
```

## Results

After running the pipeline, evaluation metrics are saved in `archive/results.yaml`:

```yaml
accuracy: 0.885
precision: 0.882
recall: 0.889
f1: 0.885
```

## Customization

### Modify parameters
Edit `params.yaml` to adjust:
- Train/test split ratio
- Feature extraction settings
- Model hyperparameters

### Add new features
Enhance `make_features.py` to include:
- Word embeddings
- Sentiment scores
- Part-of-speech tags
- Custom text preprocessing

### Try different models
Modify `train.py` to experiment with:
- Support Vector Machines (SVM)
- Random Forest
- Naive Bayes
- Neural networks

