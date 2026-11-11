# House Price Predictor

A machine learning project that estimates residential sale prices using selected property features. The project includes exploratory data analysis, model evaluation, feature-importance analysis, and an interactive Streamlit application.

**[Live Demo](https://house-price-predictor-22.streamlit.app/) · [GitHub Repository](https://github.com/thamil-sivagnanam/house-price-predictor)**

## About the Project

This project uses the Ames Housing dataset to explore how property characteristics relate to sale prices and to build models that estimate a home's sale price from its features.

The work covers data exploration, preprocessing, model comparison, evaluation, and a Streamlit interface for predictions.

## Dataset

- **Dataset:** Ames Housing
- **Records:** 2,930
- **Columns:** 82, including the target
- **Target variable:** `SalePrice`

## Notebook Workflow

The notebook uses an 80/20 train-test split with `random_state=42`. Numerical missing values are imputed using the median. Categorical missing values are imputed using the most frequent value, and categorical features are one-hot encoded.

The workflow includes:

1. Data exploration and inspection
2. Missing-value analysis and preprocessing
3. Exploratory data analysis
4. Training and comparing regression models
5. Model evaluation
6. Feature-importance analysis
7. Saving the final notebook model

## Model Comparison

Three regression models were compared on the notebook's full feature set:

| Model | R² Score |
|---|---:|
| Linear Regression | 0.7365 |
| Random Forest Regressor | 0.9110 |
| Gradient Boosting Regressor | 0.9169 |

Gradient Boosting achieved the highest R² score in this notebook experiment.

### Gradient Boosting Results

- **R² Score:** 0.9169
- **Mean Absolute Error (MAE):** 15,243.60
- **Root Mean Squared Error (RMSE):** 25,808.56

These are test-set results from the notebook experiment. They should not be interpreted as verified performance metrics for the separate model currently loaded by the Streamlit application.

### Feature Importance

The notebook's Random Forest feature-importance analysis ranked Overall Quality as the most influential feature, followed by Living Area, Garage Cars, and Total Basement Area.

## Streamlit Application

The application provides an interactive form based on six selected property features:

- Lot Area
- Year Built
- Overall Quality
- Living Area
- Basement Area
- Garage Cars

The app loads `models/model.pkl` and `models/features.pkl` to generate a predicted sale price. The uploaded saved model was inspected and identified as a scikit-learn pipeline containing a median `SimpleImputer` followed by a `RandomForestRegressor` with 400 estimators. Its six input features match the feature list used by the app: Lot Area, Year Built, Overall Qual, Gr Liv Area, Total Bsmt SF, and Garage Cars.

The repository also contains `models/final_model.pkl`, which the notebook saved after fitting the Gradient Boosting model. **The Streamlit app loads `models/model.pkl`, not `models/final_model.pkl`.** The notebook's Gradient Boosting metrics above therefore describe the notebook experiment, not the app's Random Forest model. The repository's current training script for the six-feature app model does not record a separate evaluation report, so no notebook score is attributed to the deployed app.

![Application screenshot](assets/app.png)

**[Try the Live Application](https://house-price-predictor-22.streamlit.app/)**

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Streamlit
- Joblib
- Matplotlib

## Run Locally

Clone the repository:

```bash
git clone https://github.com/thamil-sivagnanam/house-price-predictor.git
cd house-price-predictor
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the Streamlit application from the repository root:

```bash
streamlit run app/app.py
```

The application expects these files to be present:

- `models/model.pkl`
- `models/features.pkl`

## Repository Structure

```text
house-price-predictor/
├── app/
│   └── app.py
├── assets/
│   └── app.png
├── models/
│   ├── features.pkl
│   ├── final_model.pkl
│   └── model.pkl
├── notebooks/
│   └── eda.ipynb
├── src/
│   ├── evaluate.py
│   ├── main.py
│   ├── preprocess.py
│   ├── train.py
│   ├── train_save.py
│   └── utils.py
└── requirements.txt
```

## Author

**Thamil Sivagnanam**  
MSc Artificial Intelligence student at Brandenburg University of Technology (BTU Cottbus).

[GitHub Profile](https://github.com/thamil-sivagnanam)

---

This project was developed for learning purposes. Predictions are estimates based on the dataset and model, not professional property valuations.
