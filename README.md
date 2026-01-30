# Laptop Price Prediction using Machine Learning
## Introduction
This project builds a **machine learning–based laptop price prediction system** using real-world laptop specifications. The objective is to analyze how hardware, display, and software features influence laptop pricing and to compare multiple regression models to identify the most effective approach.

The notebook follows a **complete end-to-end pipeline**, including exploratory data analysis (EDA), detailed feature cleaning, feature engineering, model training, and evaluation using standard regression metrics.

## Why This Dataset?
The laptop dataset is well-suited for this problem because:
- It represents real market data with realistic pricing patterns.
- It contains a mix of categorical and numerical features, requiring extensive preprocessing.
- Pricing depends on multiple interacting components such as CPU, RAM, storage, GPU, display quality, and operating system.
- It provides an excellent opportunity to practice feature extraction from raw text data (e.g., CPU, memory, screen resolution).

## Project Workflow
### 1. Data Loading and Inspection
* Dataset loaded using Pandas
* Dataset shape, column names, and data types inspected
* Checked for missing values and duplicate rows
* Dropped unnecessary index column (`Unnamed: 0`)

### 2. Data Cleaning
#### RAM and Weight
* Removed units (`GB`, `kg`) from `Ram` and `Weight`
* Converted `Ram` to integer and `Weight` to float

#### Screen Resolution
* Extracted touchscreen information from `ScreenResolution`
* Created binary features:
  * `Touchscreen` (1 if touchscreen, else 0)
  * `Ips` (1 if IPS display, else 0)
* Split screen resolution into `X_res` and `Y_res`
* Converted resolutions to integers
* Computed **PPI (Pixels Per Inch)** using resolution and screen size
* Dropped redundant columns (`ScreenResolution`, `Inches`, `X_res`, `Y_res`)

#### CPU
* Extracted CPU names from raw text
* Grouped processors into categories:
  * Intel Core i3 / i5 / i7
  * Other Intel Processors
  * AMD Processors
* Dropped original CPU columns after encoding

#### Memory (Storage)
* Cleaned memory strings by removing units (`GB`, `TB`)
* Split storage into two parts (primary and secondary)
* Extracted storage types and sizes:
  * HDD
  * SSD
  * Hybrid
  * Flash Storage
* Retained HDD and SSD due to higher correlation with price
* Dropped low-impact storage features

#### GPU
* Extracted GPU brand from text
* Removed irrelevant GPU information

#### Operating System
* Grouped OS into categories:
  * Windows
  * Mac
  * Others / Linux / No OS
* Dropped original OS column

### 3. Exploratory Data Analysis (EDA)
* Distribution analysis of price and log-transformed price
* Bar plots for categorical features vs price
* Correlation analysis using Pearson correlation
* Heatmap visualization for numerical features

### 4. Feature Engineering
* Created `ppi` feature to capture display sharpness
* Log-transformed target variable (`Price`) to reduce skewness
* Selected high-impact numerical features:
  * RAM, Weight, Touchscreen, IPS, PPI, HDD, SSD
 
### 5. Model Preparation
* Features (`X`) separated from target (`y = log(Price)`)
* Train-test split (85% training, 15% testing)
* Categorical variables encoded using **OneHotEncoder**
* Preprocessing and modeling combined using **Scikit-learn Pipelines**

### 6. Models Trained
The following regression models were implemented and compared:
* Linear Regression
* Ridge Regression
* Lasso Regression
* K-Nearest Neighbors Regressor
* Decision Tree Regressor
* Random Forest Regressor

### 7. Evaluation Metrics













