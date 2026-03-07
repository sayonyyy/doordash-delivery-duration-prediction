
---

# 🚚 DoorDash Delivery Duration Prediction

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Machine Learning](https://img.shields.io/badge/Machine-Learning-green)
![Scikit Learn](https://img.shields.io/badge/Scikit--Learn-orange)
![Random Forest](https://img.shields.io/badge/Random-Forest-darkgreen)
![XGBoost](https://img.shields.io/badge/XGBoost-red)
![LightGBM](https://img.shields.io/badge/LightGBM-darkgreen)

Accurately predicting food delivery time is critical for improving customer experience, driver allocation, and marketplace efficiency in large-scale delivery platforms such as DoorDash.

This project develops **machine learning models to predict food delivery duration** using operational, marketplace, and order-level data from historical deliveries.

---

# 📌 Problem Statement

When a customer places an order on DoorDash, the platform shows an **Estimated Time of Arrival (ETA)**.

Accurate ETAs are essential because:

* **Underestimation →** Customer dissatisfaction
* **Overestimation →** Lower order conversion
* **Driver allocation imbalance →** Inefficient logistics

The goal of this project is to predict the delivery duration between:

**Start:** `created_at` (order placed)
**End:** `actual_delivery_time` (order delivered)

---

# 🎯 Objective

Build a **machine learning model** that predicts total delivery duration using:

* order characteristics
* restaurant attributes
* marketplace supply and demand
* operational delivery estimates

---

# 📊 Dataset Overview

Each row represents **one delivery order**.

---

## Time Features

| Feature              | Description                            |
| -------------------- | -------------------------------------- |
| market_id            | Region where the order was placed      |
| created_at           | Timestamp when the order was placed    |
| actual_delivery_time | Timestamp when the order was delivered |

---

## Store Features

| Feature                | Description                         |
| ---------------------- | ----------------------------------- |
| store_id               | Unique restaurant identifier        |
| store_primary_category | Restaurant cuisine category         |
| order_protocol         | Ordering protocol used by the store |

---

## Order Features

| Feature            | Description             |
| ------------------ | ----------------------- |
| total_items        | Number of items ordered |
| subtotal           | Total order value       |
| num_distinct_items | Number of unique items  |
| min_item_price     | Minimum item price      |
| max_item_price     | Maximum item price      |

---

## Marketplace Features

These variables represent the **supply-demand state of the delivery network**.

| Feature                  | Description                           |
| ------------------------ | ------------------------------------- |
| total_onshift_dashers    | Available drivers near the restaurant |
| total_busy_dashers       | Drivers currently delivering          |
| total_outstanding_orders | Orders currently being processed      |

---

## Operational Estimates

These variables represent **internal estimates of delivery stages**.

| Feature                                      | Description                                      |
| -------------------------------------------- | ------------------------------------------------ |
| estimated_order_place_duration               | Estimated time for restaurant to receive order   |
| estimated_store_to_consumer_driving_duration | Estimated travel time between store and customer |

---

# ⚙️ Feature Engineering

Several features were engineered to improve predictive performance.

---

## Delivery Duration

The **target variable** was calculated as:

```
actual_total_delivery_duration =
actual_delivery_time - created_at
```

Converted to **minutes** for modeling.

---

## Marketplace Pressure Indicator

```
busy_dashers_ratio =
total_busy_dashers / total_onshift_dashers
```

This captures **driver workload pressure in the marketplace**.

---

## Operational Duration Aggregation

```
estimated_non_prep_duration =
estimated_store_to_consumer_driving_duration
+ estimated_order_place_duration
```

This represents **non-preparation time components of the delivery pipeline**.

---

### Additional Preprocessing

* Datetime conversion
* Handling infinite ratios
* Missing value removal
* One-hot encoding of categorical features
* Multicollinearity detection using correlation analysis

---

# 🧠 Modeling Approach

Multiple machine learning models were trained and compared.

### Baseline Model

* Linear Regression

### Tree-Based Models

* Random Forest Regressor

### Gradient Boosting Models

* XGBoost
* LightGBM

Tree-based and boosting models capture **nonlinear relationships between delivery time drivers**.

---

# 🔧 Hyperparameter Optimization

Hyperparameters were optimized using:

**RandomizedSearchCV**

This method searches multiple parameter combinations using **cross-validation** to identify the best performing model configuration.

---

# 📏 Model Evaluation

Models were evaluated using standard regression metrics.

| Metric | Description                        |
| ------ | ---------------------------------- |
| RMSE   | Penalizes larger prediction errors |
| MAE    | Average absolute prediction error  |

Model predictions were also visualized using:

* **Actual vs Predicted delivery time plots**

---

# 📊 Model Performance

| Model             | RMSE   | MAE    |
| ----------------- | ------ | ------ |
| Linear Regression | ~18.03 | ~12.70 |
| Random Forest     | ~17.41 | ~12.06 |
| XGBoost           | ~17.17 | ~11.76 |
| LightGBM          | ~17.11 | ~11.80 |
| Tuned XGBoost     | ~17.20 | ~11.78 |
| Tuned LightGBM    | ~17.09 | ~11.86 |

The **LightGBM model achieved the best performance**.

---

# 🔍 Feature Importance

The model identified several **key drivers of delivery duration**.

Most influential factors include:

* driver availability (`total_onshift_dashers`)
* travel time (`estimated_store_to_consumer_driving_duration`)
* order value (`subtotal`)
* marketplace congestion (`busy_dashers_ratio`)
* item price range
* order complexity

These results align with **real-world delivery operations**.

---

# 🚚 Delivery ETA Simulation

Using model predictions, delivery duration can be converted into a **real ETA**.

Example workflow:

```
Predicted Delivery Duration = 45 minutes
Order Time = 7:30 PM
Estimated Delivery Time = 8:15 PM
```

This demonstrates how the model could be integrated into a **real-time delivery platform**.

---

# 💼 Business Impact

Accurate delivery time prediction can significantly improve platform efficiency:

- **Customer Experience** – more reliable ETAs
- **Marketplace Efficiency** – better driver allocation
- **Order Conversion** – reduced ETA overestimation
- **Logistics Optimization** – improved dispatch decisions

Such models can directly power **real-time ETA systems used by large-scale delivery platforms like DoorDash, Uber Eats, and Instacart.**

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

# 📦 Dataset Source

The dataset used in this project is derived from historical delivery data from **DoorDash** and is commonly used in data science case studies.

Source: StrataScratch Delivery Duration Prediction dataset.

*Note: The dataset is anonymized and used for educational and research purposes.*

---

# 📂 Project Structure

```
doordash-delivery-duration-prediction
│
├── datasets
│   └── historical_data.csv
│
├── deliver_duration_prediction.ipynb
│
└── README.md
```

---

# 👤 Author

**Sayony Chakraborty**

Data Science | Machine Learning | Data Analytics

GitHub
[https://github.com/sayonyyy](https://github.com/sayonyyy)

LinkedIn  
[https://linkedin.com/in/sayonychakraborty](https://linkedin.com/in/sayonychakraborty)

Email
sayonychakraborty@gmail.com

---

