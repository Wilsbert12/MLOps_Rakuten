# Rakuten Product Classification - MLOps Pipeline

This project demonstrates a complete MLOps pipeline for the [Rakuten product classification challenge](https://challengedata.ens.fr/participants/challenges/35/), focusing on deployment, versioning, and operational aspects rather than model accuracy.

## Project Overview

- **Task**: Classify products into categories using text and image data
- **Focus**: MLOps infrastructure (MLflow, FastAPI, Docker, model versioning)
- **Models**: Classical ML pipeline with XGBoost, Random Forest, Logistic Regression, and SVM (with plans to integrate deep learning models later)

## Project Structure

```
MLOps_Rakuten/
├── data/                    # Local data folder (not tracked in git)
│   ├── images/              # Product images
│   ├── text/                # Product text data (CSV files)
│   └── processed/           # Processed/cleaned data
│       ├── images/          # Processed image features
│       └── text/            # Processed text features
├── scripts/
│   ├── load_data_to_db.py  # One-time data loading to database
│   └── (additional scripts will be added)
├── src/
│   ├── api/
│   │   └── main.py             # FastAPI application entry point
│   ├── models/                 # Model training and evaluation
│   └── utils/                  # Utility functions
├── tests/                  # Unit tests
├── docker/                 # Docker configuration
├── mlflow/                 # MLflow tracking
├── .gitignore
├── requirements.txt
├── LICENSE                 # Project license
└── README.md               # This file
```

## Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/Wilsbert12/MLOps_Rakuten.git
cd MLOps_Rakuten
```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Download Dataset
1. Download the Rakuten product classification dataset
2. Extract and organize files in the existing data structure:
   ```
   data/
   ├── images/          # Place all product images here
   │   ├── image_001.jpg
   │   ├── image_002.jpg
   │   └── ...
   ├── text/            # Place CSV files here
   │   └── product_data.csv
   └── processed/       # Will be populated by preprocessing scripts
       ├── images/
       └── text/
   ```
3. The folder structure is already created in the repo with .gitkeep files

### 4. Setup Database
We use local MongoDB instances for this project for the following reasons:
- Faster queries (no internet latency)
- Works offline during development
- No storage limits or costs
- Each team member can experiment independently
- Simpler initial setup and coordination

**Install and setup local MongoDB:**
1. Install MongoDB locally on your system
2. Start MongoDB service
3. The database connection is configured in the loading script

*Note: We can migrate to a shared MongoDB Atlas instance later if team collaboration requires it.*

### 5. Load Data to Database
```bash
python scripts/load_data_to_db.py
```

### 6. Run the Application
```bash
# Start the API
python -m uvicorn src.api.main:app --reload

# Run MLflow UI
mlflow ui
```

## MLOps Metrics

*To be discussed and defined by the team.*

- **Inference Latency**: < 200ms per prediction
- **Throughput**: > 100 predictions/second
- **Model Versioning**: Track all model iterations in MLflow
- **Deployment Success Rate**: > 99% successful deployments
- **Resource Utilization**: Monitor CPU/memory usage

## Team Development

Each team member should:
1. Clone this repository
2. Download dataset to local `./data/` subfolders (images in `./data/images/`, text in `./data/text/`)
3. Set up local MongoDB database
4. Run the data loading script
5. Develop and test locally

## Technology Stack

- **Database**: MongoDB (NoSQL)
- **ML Tracking**: MLflow
- **API**: FastAPI
- **Containerization**: Docker
- **Models**: Scikit-learn (XGBoost, Random Forest, Logistic Regression, SVM)
- **Testing**: Pytest

## Contributing

1. Create feature branch from main
2. Make changes and test locally
3. Submit pull request
4. Ensure all tests pass