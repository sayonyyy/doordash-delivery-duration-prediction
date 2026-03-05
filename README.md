

---

# 🚚 DoorDash Delivery Duration Prediction

Accurately predicting food delivery time is critical for improving **customer experience**, **driver allocation**, and **marketplace efficiency** on platforms like **DoorDash**.

This project builds machine learning models to estimate the **total delivery duration** of an order using operational, marketplace, and order-level features.

---

# 📌 Problem Statement

When a customer places an order on DoorDash, the platform shows an **estimated delivery time (ETA)**.

Accurate ETAs are important because:

* Underestimation → customer dissatisfaction
* Overestimation → reduced order conversion
* Marketplace imbalance → inefficient driver allocation

The objective of this project is to **predict the delivery duration** between:

Start → `created_at` (order placed)
End → `actual_delivery_time` (order delivered)

---

# 🎯 Objective

Build a machine learning model that predicts the **total delivery duration** of a food delivery order using features related to:

* order characteristics
* restaurant information
* marketplace supply and demand
* operational duration estimates

---

# 📊 Dataset Overview

Each row in the dataset represents **one delivery order**.

## Time Features

| Feature                | Description                            |
| ---------------------- | -------------------------------------- |
| `market_id`            | Region where the order was placed      |
| `created_at`           | Timestamp when the order was created   |
| `actual_delivery_time` | Timestamp when the order was delivered |

---

## Store Features

| Feature                  | Description                          |
| ------------------------ | ------------------------------------ |
| `store_id`               | Unique identifier for the restaurant |
| `store_primary_category` | Cuisine category                     |
| `order_protocol`         | Ordering protocol used by the store  |

---

## Order Features

| Feature              | Description                  |
| -------------------- | ---------------------------- |
| `total_items`        | Number of items in the order |
| `subtotal`           | Total order value            |
| `num_distinct_items` | Number of unique items       |
| `min_item_price`     | Lowest item price            |
| `max_item_price`     | Highest item price           |

---

## Marketplace Features

These variables capture the **supply-demand dynamics** of the delivery marketplace.

| Feature                    | Description                                |
| -------------------------- | ------------------------------------------ |
| `total_onshift_dashers`    | Number of drivers available near the store |
| `total_busy_dashers`       | Drivers currently delivering orders        |
| `total_outstanding_orders` | Orders currently being processed nearby    |

---

## Operational Predictions

These values represent **internal system estimates** for parts of the delivery process.

| Feature                                        | Description                                        |
| ---------------------------------------------- | -------------------------------------------------- |
| `estimated_order_place_duration`               | Estimated time for restaurant to receive the order |
| `estimated_store_to_consumer_driving_duration` | Estimated driving time from store to customer      |

---

# ⚙️ Feature Engineering

Key transformations performed during preprocessing:

* Timestamp conversion to datetime format
* Delivery duration calculation from order creation to delivery
* Marketplace pressure indicator

  ```
  busy_dashers_ratio = total_busy_dashers / total_onshift_dashers
  ```
* Operational duration aggregation

  ```
  estimated_non_prep_duration =
  estimated_store_to_consumer_driving_duration +
  estimated_order_place_duration
  ```
* One-hot encoding of categorical variables
* Handling missing values and infinite ratios
* Multicollinearity analysis and feature selection

---

# 🧠 Modeling Approach

Multiple regression models were trained to predict delivery duration.

### Baseline Model

* Linear Regression

### Tree-Based Models

* Random Forest Regressor
* XGBoost Regressor
* LightGBM Regressor

Tree-based models capture **non-linear relationships** between marketplace dynamics and delivery time more effectively than linear models.

---

# 📏 Model Evaluation

Models were evaluated using standard regression metrics:

| Metric | Purpose                           |
| ------ | --------------------------------- |
| RMSE   | Penalizes large prediction errors |
| MAE    | Average absolute prediction error |
| R²     | Measures model explanatory power  |

Model predictions were also analyzed using **actual vs predicted delivery time visualizations**.

---

# 📈 Key Insights

The analysis highlights how delivery duration is influenced by:

* order complexity
* restaurant category
* driver availability
* marketplace congestion
* estimated preparation and driving time

These insights help understand how operational factors affect **delivery ETA accuracy**.

---

# 🛠 Tech Stack

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* XGBoost
* LightGBM

---

# 📂 Project Structure

```
doordash-delivery-duration-prediction
│
├── data
│   └── historical_data.csv
│
├── notebooks
│   └── doordash_analysis.ipynb
│
├── README.md
│
└── requirements.txt
```

---

# 👤 Author

**Sayony Chakraborty**

Data Science | Machine Learning | Data Analytics

GitHub
[https://github.com/sayonyyy](https://github.com/sayonyyy)

---

