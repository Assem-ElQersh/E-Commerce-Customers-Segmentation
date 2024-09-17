# *E-Commerce Customers Segmentation*

### **Project Overview**
This project applies **clustering techniques** to segment customers of an E-commerce platform based on their transaction history and demographic data. The goal is to group customers with similar behaviors for marketing and personalization purposes. We compare three clustering algorithms: **K-Means**, **DBSCAN**, and **Hierarchical Clustering**, and evaluate their performance using silhouette scores.

### Dataset Information
The dataset contains customer transaction records along with demographic information, which includes:
- **customers**: Information on customer IDs, gender, and city.
- **transactions**: Records of purchases, including transaction status and coupon usage.
- **genders**: Mapping between gender ID and gender name.
- **cities**: Mapping between city ID and city name.

Key Features:
- `gender_name`: Gender of the customer.
- `city_name`: City where the customer resides.
- `coupon_usage_frequency`: Number of times the customer used coupons.
- `total_transactions`: Total number of transactions made by the customer.

### Project Structure
The project consists of the following key steps:

### 1. **Data Loading and Preprocessing**
- Load data from an Excel file containing multiple sheets.
- Drop irrelevant columns such as `burn_date` from the transaction data.
- Handle missing data using **SimpleImputer**:
  - Categorical columns: Imputed with the most frequent value.
  - Numerical columns: Imputed with the mean value.
- One-Hot Encoding was applied to categorical features like `gender_name` and `city_name`.

### 2. **Data Merging and Aggregation**
- Merged customer demographic information with transaction data.
- Aggregated transactions by calculating `coupon_usage_frequency` and `total_transactions` for each customer.
  
### 3. **Feature Selection and Preprocessing for Clustering**
- Selected features: `gender_name`, `city_name`, `coupon_usage_frequency`, and `total_transactions`.
- Preprocessed the data by scaling for **Hierarchical Clustering**, but no scaling was applied for **K-Means** and **DBSCAN** as scaling negatively impacted their results.

### 4. **Clustering Techniques**
We applied three clustering algorithms to the preprocessed data:

#### a. **K-Means Clustering**
- Tuned the number of clusters (`k`) using the **Elbow Method** and **Silhouette Scores**.
- The optimal number of clusters was **4**, with the highest silhouette score of **0.62**.

#### b. **DBSCAN Clustering**
- Applied grid search to optimize `eps` and `min_samples`.
- Best parameters: `eps=0.5`, `min_samples=5`.
- DBSCAN struggled with varying densities in the dataset, especially in high-dimensional spaces, making it less suitable for this particular problem.

#### c. **Hierarchical Clustering**
- Tested different linkage methods (Ward, Complete, Average).
- Best performance was achieved with **5 clusters** and **Average Linkage**.
- Hierarchical clustering produced clear groups but was more computationally expensive.

### 5. **Model Comparison**
| Model         | Best Params                                  | Silhouette Score           |
|---------------|----------------------------------------------|----------------------------|
| K-Means       | `n_clusters=4`                               | 0.62                       |
| DBSCAN        | `eps=0.5`, `min_samples=5`                   | 0.99(unstable due to noise)|
| Hierarchical  | `n_clusters=5`, `linkage='average'`          | 0.80                       |

**Key Findings**:
- **K-Means** performed the best with a silhouette score of **0.62**, identifying 4 distinct customer segments.
- **DBSCAN** had difficulties with noise and clusters of varying densities, making it less effective.
- **Hierarchical Clustering** was computationally expensive but produced reasonable clusters with an average silhouette score of **0.58**.

### 6. **Dimensionality Reduction for Visualization**
- Applied **PCA (Principal Component Analysis)** to reduce the dataset to 2 dimensions for visualizing the clusters.
  
### 7. **Visualization of Clusters**
Visualizations were generated to display the clustering results using **PCA** for dimensionality reduction:
- **K-Means Clustering**: 4 distinct clusters with good separation.
- **DBSCAN**: Struggled with noisy data and did not form clear clusters.
- **Hierarchical Clustering**: Produced 5 clusters with moderate separation.

### How to Run the Project

1. **Clone the Repository**:
```bash
git clone https://github.com/Assem-ElQersh//E-Commerce-Customers-Segmentation.git
cd E-commerce-Customer-Segmentation
```

2. **Install the Required Dependencies**:
```bash
pip install -r requirements.txt
```

3. **Run the Jupyter Notebook**:
Execute the notebook to preprocess the data, apply clustering algorithms, and generate visualizations.

#### Repository Structure
```
├── data/
│   ├── E-commerce_data.xlsx
├── src/
│   ├── Model.ipynb
├── README.md
└── requirements.txt
```

### Results and Conclusion
- **K-Means** was this dataset's most effective clustering method, producing 4 customer segments with the best silhouette score.
- **DBSCAN** struggled with noise and varying densities,

  resulting in lower performance.
- **Hierarchical Clustering** could identify clear segments but was less scalable and more computationally expensive compared to K-Means.

This project demonstrates a comprehensive approach to customer segmentation using various clustering techniques. The analysis offers valuable insights into customer behavior, which can be utilized by the E-commerce platform for targeted marketing strategies and personalized recommendations.


##
- Please note that this project is part of the **MLSC Data Science Graduation Project**.
