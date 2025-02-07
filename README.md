Here is your formatted README for the Kaggle Predicting Future Sales project:

---

# Kaggle-Predicting-Future-Sales
![Kaggle-Predicting-Future-Sales](https://img.shields.io/badge/ForTheBadge-uses--git-brightgreen)  

**The goal of this project is to predict the future sales using a challenging time-series dataset consisting of daily sales data.**  
This project was built with the aim to apply and enhance data science skills for predicting the total sales for every product and store in the next month. The dataset was kindly provided by 1C Company, one of the largest Russian software firms.

---

## Motivation
In this competition, I worked with a challenging time-series dataset containing daily sales data, aiming to predict the total sales for every product and store in the next month. By solving this problem, I could apply and improve my data science skills.

---

## Project Overview
### Competition: [Predict Future Sales](https://www.kaggle.com/competitions/predict-future-sales)
- **Data**: Historical daily sales data
- **Task**: Forecast the total sales of products for each shop in the test set for the following month.
- **Key challenges**: Shops and products change every month, creating a dynamic data environment.

### Tools and Libraries Used:
- **Python Libraries**: NumPy, Pandas, Scikit-Learn, XGBoost, LightGBM
- **Hardware**: Training on a Linux server with Intel i5 processor, 16GB RAM, NVIDIA 1080 GPU.

---

## Data Description
You are provided with daily historical sales data, and the task is to forecast the total sales amount for each shop and product for the test set. The list of shops and products changes slightly every month.

### File Descriptions:
- `sales_train.csv`: The training set from January 2013 to October 2015.
- `test.csv`: The test set to forecast sales for November 2015.
- `sample_submission.csv`: Sample submission file in the correct format.
- `items.csv`: Information about the items/products.
- `item_categories.csv`: Information about the item categories.
- `shops.csv`: Information about the shops.

### Data Fields:
- `ID`: A unique ID for each shop-item pair in the test set.
- `shop_id`: Unique identifier for each shop.
- `item_id`: Unique identifier for each product.
- `item_category_id`: Unique identifier for each item category.
- `item_cnt_day`: Number of products sold (daily data).
- `item_price`: Price of the item.
- `date`: Date in `dd/mm/yyyy` format.
- `date_block_num`: A consecutive month number (0 for January 2013, 33 for October 2015).
- `item_name`: Name of the item.
- `shop_name`: Name of the shop.
- `item_category_name`: Name of the item category.

---

## Approach

### **Exploratory Data Analysis (EDA)**
Basic data analysis was done, which included plotting item counts (`item_cnt_day`) per month to uncover patterns, inspecting missing values, and analyzing the test set. Some key insights include:
- A decline in sold items over the year.
- Peaks in November and consistent zigzag patterns in June-July-August.

### **Feature Engineering**
1. **Generate Shop-Item Pairs & Mean Encoding**:  
   Aggregating data to a monthly level, generating features such as `target`, `shop_block_target_sum`, and `item_block_target_mean`.
   
2. **Lag Features**:  
   Generated lag features based on `item_cnt` grouped by `shop_id` and `item_id` over various time steps (1, 2, 3, 5, and 12 months).

3. **Holiday Features**:  
   Created Boolean features for Russian national holidays such as New Year's, Valentine's Day, Women's Day, and Easter.

### **Cross-Validation**
Since this is a time series problem, cross-validation was done using a custom `get_cv_idxs()` function, dividing data into 6 folds based on `date_block_num`.

---

## Models Used
### 1. **LightGBM**
LightGBM was tuned using **hyperopt** and **GridSearchCV**. The best model produced a mean RMSE of 0.8088 across the 6 folds of cross-validation.

### 2. **XGBoost**
I ran XGBoost using GPU, but it didn't perform as consistently as LightGBM. Despite tuning, the best models had RMSE scores slightly worse than LightGBM.

### 3. **Ensembling**
Ensembling models using:
- **Simple Average** and **Weighted Average**
- **Linear Regression** and **ElasticNet**
- **Shallow Random Forest**  
The ensembling methods didn't outperform the LightGBM model but added slight improvements.

---

## Improvements and Future Work
1. Implement neural networks without categorical embeddings.
2. Generate more holiday-related features, such as differences between current month and holiday month.
3. Translate item names to English and perform sentiment analysis on item names.

---

## Installation
To run this project, you need to install the required dependencies:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn xgboost lightgbm
```

---

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/iamsivab/Kaggle-Predicting-Future-Sales.git
   ```
   
2. Run the project using Jupyter Notebooks or Python scripts.
