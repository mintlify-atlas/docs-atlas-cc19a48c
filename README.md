# NBA Playoff Prediction - Comprehensive Documentation

This project predicts NBA playoff teams using machine learning approaches on team statistics.

## 📁 Project Structure

```
workspace/
├── source/              # Raw data processing and feature engineering
├── data/
│   └── processed/       # Processed feature data and train/val/test splits
├── models/              # Trained model checkpoints
│   ├── logistic_regression/
│   ├── knn/
│   └── neural_network/
├── results/             # Model evaluation results and visualizations
│   ├── logistic_regression/
│   ├── knn/
│   ├── neural_network/
│   ├── eda/
│   └── model_comparison/
└── docs/                # Documentation
```

## 📚 Documentation Pages

### 1. [nba-predict.ipynb](reference/nba-predict.ipynb)
- **Purpose**: Data collection and feature engineering
- **Inputs**: Raw NBA team statistics from Kaggle dataset
- **Outputs**: Processed features, train/val/test splits
- **Key Functions**: Data loading, feature creation, data splitting

### 2. [log-predict.ipynb](reference/log-predict.ipynb)
- **Purpose**: Logistic Regression with L2 regularization
- **Inputs**: Processed feature data (baseline, poly2, poly3, PCA)
- **Outputs**: Trained models, performance metrics, visualizations
- **Best Model**: Lambda=0.01, Baseline features (AUC: 0.9754)

### 3. [knn-predict.ipynb](reference/knn-predict.ipynb)
- **Purpose**: K-Nearest Neighbors classification
- **Inputs**: Processed feature data (4 transformations)
- **Outputs**: 128 trained models, hyperparameter analysis
- **Best Model**: K=21, Polynomial degree 3, manhattan distance (AUC: 0.9660)

### 4. [neural-network-predict.ipynb](reference/neural-network-predict.ipynb)
- **Purpose**: Deep learning classification with Keras/TensorFlow
- **Inputs**: Processed feature data (4 transformations)
- **Outputs**: 96 trained models, architecture comparison
- **Best Model**: 2-Layer (128, 64), L2-0.01, Baseline features (AUC: 0.9824)

### 5. [model-comparison.ipynb](reference/model-comparison.ipynb)
- **Purpose**: Comprehensive comparison of all three approaches
- **Analysis**: Performance metrics, feature transformation impact, radar charts
- **Recommendation**: Neural Network (2-Layer, L2-0.01) for production use

### 6. [exploratory-data-analysis.ipynb](reference/exploratory-data-analysis.ipynb)
- **Purpose**: In-depth EDA and unsupervised learning
- **Analysis**: Feature distributions, correlation matrix, PCA, K-means clustering
- **Key Findings**: 11 components for 90% variance, natural clustering aligns with playoff status

## 🏆 Final Results Summary

| Model | Accuracy | Precision | Recall | F1 Score | AUC |
|-------|----------|-----------|--------|----------|-----|
| **Neural Network** | 0.8750 | **0.8936** | 0.9844 | 0.8936 | **0.9824** |
| Logistic Regression | **0.8917** | 0.8493 | 0.9688 | **0.9051** | 0.9754 |
| K-Nearest Neighbors | 0.8167 | 0.7500 | **0.9844** | 0.8514 | 0.9660 |

### Winner: **Neural Network (2-Layer, L2-0.01, Baseline Features)**
- Best overall performance (average score: 0.9258)
- Highest AUC (0.9824)
- Excellent balance between precision and recall
- Robust across different feature transformations

## 📊 Key Insights

### Feature Engineering Impact
- **Logistic Regression**: Benefits from polynomial features
- **KNN**: Best performance with Polynomial degree 3
- **Neural Networks**: Baseline scaled features work best

### Model Strengths
1. **Neural Network**: Best overall predictive performance, balanced metrics
2. **Logistic Regression**: Most interpretable, nearly matches NN performance
3. **K-Nearest Neighbors**: Best recall (0.9844), catches nearly all playoff teams

### Class Balance
- 53.8% playoff teams in dataset
- All models achieve >95% recall
- Neural network achieves best precision (89.36%)

## 🚀 Usage

### Training Models
```bash
# Train logistic regression
jupyter nbconvert --execute reference/log-predict.ipynb

# Train KNN
jupyter nbconvert --execute reference/knn-predict.ipynb

# Train neural network
jupyter nbconvert --execute reference/neural-network-predict.ipynb
```

### Running Analysis
```bash
# Generate model comparison
jupyter nbconvert --execute reference/model-comparison.ipynb

# Run exploratory data analysis
jupyter nbconvert --execute reference/exploratory-data-analysis.ipynb
```

## 📝 Dataset Information

- **Source**: Historical NBA team statistics
- **Features**: 27 engineered features (see [nba-predict.ipynb](reference/nba-predict.ipynb))
- **Samples**: 
  - Training: 446 teams
  - Validation: 120 teams
  - Test: 120 teams
- **Target**: Binary classification (made playoffs: 1, did not make playoffs: 0)

### Feature Categories
1. **Performance Metrics**: Win percentage, point differential, plus/minus
2. **Offensive Stats**: Points scored, field goals, three-pointers, free throws, EFG%
3. **Defensive Stats**: Points allowed, defensive strength
4. **Rebounding**: Total rebounds, offensive/defensive rebounds
5. **Ball Movement**: Assists, turnovers, steals, blocks
6. **Efficiency**: Field goal percentage, three-point percentage, free throw percentage

## 🔬 Methodology

### Data Processing
1. Feature engineering from raw team statistics
2. StandardScaler normalization
3. Four feature transformations:
   - Baseline (scaled)
   - Polynomial degree 2 (405 features)
   - Polynomial degree 3 (4059 features)
   - PCA (95% variance, 13 components)

### Model Training
- **Logistic Regression**: Tested 24 configurations (6 lambda values × 4 transformations)
- **K-Nearest Neighbors**: Tested 128 configurations (8 K values × 2 metrics × 2 weights × 4 transformations)
- **Neural Networks**: Tested 96 configurations (4 architectures × 6 regularizations × 4 transformations)

### Evaluation Metrics
- Accuracy: Overall prediction correctness
- Precision: Ability to avoid false positives
- Recall: Ability to identify all playoff teams
- F1 Score: Harmonic mean of precision and recall
- AUC: Area Under ROC Curve (discriminative ability)

## 🎯 Future Work

1. **Ensemble Modeling**: Combine predictions from all three models
2. **Temporal Validation**: Test on recent seasons for robustness
3. **Feature Importance**: Analyze which NBA statistics matter most
4. **Hyperparameter Tuning**: Fine-tune neural network architecture
5. **Cross-Validation**: Implement k-fold CV for robust estimates
6. **Real-time Predictions**: Deploy model for current season predictions

## 📦 Dependencies

- Python 3.x
- NumPy, Pandas, Matplotlib, Seaborn
- Scikit-learn (preprocessing, PCA, KNN, clustering)
- TensorFlow/Keras (neural networks)
- Jupyter Notebook

## 👥 Contact

For questions or feedback about this project, please refer to the individual notebook documentation.

---

**Last Updated**: March 4, 2026
**Version**: 1.0.0
