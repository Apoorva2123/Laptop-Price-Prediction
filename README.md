# Laptop Price Prediction using Machine Learning
## Introduction
Ever wondered what really drives the price of a laptop — the processor, RAM, GPU, or brand name? This project explores how different technical specifications influence laptop pricing by building and comparing multiple machine learning regression models. From raw data to final predictions, the workflow demonstrates how real-world datasets can be transformed into actionable insights through data science.

This project builds a **machine learning–based laptop price prediction system** using real-world laptop specifications. The objective is to analyze how hardware, display, and software features influence laptop pricing and to compare multiple regression models to identify the most effective approach.

The notebook follows a **complete end-to-end pipeline**, including exploratory data analysis (EDA), detailed feature cleaning, feature engineering, model training, and evaluation using standard regression metrics.

## Why This Dataset?
The laptop dataset is well-suited for this problem because:
- It represents real market data with realistic pricing patterns.
- It contains a mix of categorical and numerical features, requiring extensive preprocessing.
- Pricing depends on multiple interacting components such as CPU, RAM, storage, GPU, display quality, and operating system.
- It provides an excellent opportunity to practice feature extraction from raw text data (e.g., CPU, memory, screen resolution).
- Pricing is influenced by complex interactions between features, mimicking real-world decision-making scenarios.

The dataset includes outliers and high variability in prices, requiring careful model tuning.

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
Each model’s performance was assessed using:
* **R² Score** to evaluate how much variance in the data was explained.
* **Mean Absolute Error (MAE)** – to measure average prediction error
Predictions were compared against actual prices in log scale to ensure stability and fairness across models.

### Technologies Used
* Python
* NumPy
* Pandas
* Matplotlib & Seaborn
* Scikit-learn
* Jupyter Notebook

### Challenges Faced
- **Messy text data:** Key features like CPU, storage, and screen resolution were embedded in raw text and required careful parsing and validation.
- **Feature selection trade-offs:** Some extracted features had low impact on price and were intentionally dropped to reduce noise and improve model performance.
- **Skewed target variable:** Laptop prices were highly skewed, requiring log transformation to stabilize training and improve predictions.

### Repository Structure
* `Laptop_Prediction.ipynb` – Complete notebook with analysis, preprocessing, modeling, and evaluation
* `README.md` – Project documentation

### Conclusion
This project demonstrates **how careful data cleaning, feature engineering, and model selection significantly impact predictive performance**. By transforming raw laptop specifications into meaningful, model-ready features and systematically comparing multiple regression models, the project highlights the importance of preprocessing in real-world machine learning. It illustrates that attention to detail in handling textual and numerical data, along with proper feature encoding and target transformation, directly improves prediction accuracy. This end-to-end project reinforces essential skills in data analysis, machine learning modeling, and performance evaluation, providing a practical example that can be applied to similar structured data problems in industry.

### Acknowledgements
Thank you for exploring this project. Feedback, suggestions, and improvements are always welcome—feel free to fork the repository.












