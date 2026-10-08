# Mental_Health_Score

## Mental Health Signal

An end-to-end machine learning project that predicts a student's **mental health score (0–10)** from their social media habits, lifestyle and stress level.

The project covers the full journey: exploring and cleaning the data, training and comparing models, saving the best one, serving it through an API, and building a web page where anyone can enter their details and see a predicted score.

> This is a learning project for informational purposes only. It is not a clinical assessment or a diagnosis.

## About the project

Students spend a large part of their day on social media, and that time interacts with sleep, study, exercise and stress. This project asks a simple question: **given a student's daily habits, can we estimate their mental health score?**

Since the answer is a number and not a category, this is a **regression** problem.

The user fills in a short form with 12 details, and the app returns a score on a gauge with one of three readings:

| Score | Reading |
|---|---|
| Below 4 | Strained |
| 4 to below 7 | Balanced |
| 7 and above | Strong |

## Dataset

**Student Social Media and Mental Health Impact**: 5,000 student records with 13 columns.

| Group | Columns |
|---|---|
| Profile | Age, Gender, Country, Academic Level |
| Social media use | Most Used Platform, Purpose of Use, Average Daily Usage Hours, Daily Unlocks |
| Lifestyle | Study Hours, Physical Activity Hours, Sleep Hours per Night |
| Stress | Stress Level (Low, Medium, High, Very High) |
| Target | Mental Health Score |

## What was done

**1. Data exploration**
Checked the shape, data types, missing values and duplicates, then plotted the target distribution, a correlation heatmap, and how stress, screen time and sleep relate to the score.

**2. Data cleaning**
Removed 2 duplicate rows and corrected impossible negative values in physical activity hours.

**3. Feature engineering**
The country column had 111 different values, so it was reduced to the 9 most common countries plus an "Other" group.

**4. Preprocessing**
Each kind of column gets the treatment it needs: a log transform for the skewed study hours, scaling for numeric columns, ordered encoding for stress level, and one-hot encoding for the remaining categories.

**5. Model training**
Three models were trained and compared on a 70/30 train/test split: Linear Regression as a baseline, a Random Forest, and a Random Forest with tuned hyperparameters.

**6. Saving the model**
Preprocessing and model were combined into one pipeline and saved as a single `.pkl` file.

**7. Backend**
A FastAPI app loads the saved pipeline and exposes a `/predict` endpoint. Pydantic checks every input before it reaches the model.

**8. Frontend**
A web page with a form that sends the details to the API and displays the predicted score on an animated gauge.

## Results

| Model | Test R² | MAE | RMSE |
|---|---|---|---|
| Linear Regression | 0.740 | 0.536 | 0.676 |
| **Random Forest** | **0.877** | **0.347** | **0.464** |
| Random Forest (tuned) | 0.865 | 0.369 | 0.487 |

The Random Forest performed best and is the model used in the app. It explains about 88% of the variation in scores, and its predictions are on average about 0.35 points away from the true value.

## Tech stack

| Part | Tools |
|---|---|
| Data analysis | pandas, NumPy, Matplotlib, Seaborn |
| Machine learning | scikit-learn |
| Model storage | joblib |
| Backend | FastAPI, Pydantic, Uvicorn |
| Frontend | HTML, CSS, JavaScript |

## Files

| File | Purpose |
|---|---|
| `ML.ipynb` | Data exploration, cleaning, training and evaluation |
| `Student_Social_Media_And_Mental_Health_Impact.csv` | Dataset |
| `Mental_Health_Model.pkl` | Saved model pipeline |
| `main.py` | FastAPI backend |
| `requirements.txt` | Backend dependencies |
| `index.html`, `style.css`, `script.js` | Web page |
