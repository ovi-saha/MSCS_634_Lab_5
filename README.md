# Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering   
Avijit Saha  
Advanced Big Data and Data Mining (MSCS-634-M20)  
Dr. Satish Penmatsa  
March 12, 2026
This Repo is Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering for Advanced Big Data and Data Mining (MSCS-634-M20)

## Project Overview
This lab explores unsupervised machine learning techniques by applying **Hierarchical (Agglomerative)** and **DBSCAN** clustering algorithms to the UCI Wine Dataset. The dataset contains chemical analyses of wines grown in the same region of Italy but derived from three different cultivars. 

The goal was to determine how effectively these algorithms could group the 178 samples based on 13 chemical attributes such as Alcohol, Magnesium, and Color Intensity.

## Lab Structure
The analysis was conducted in four distinct steps:
1. **Data Preparation:** Loading the dataset from `sklearn` and standardizing features using `StandardScaler` to ensure distance-based metrics were not biased by feature scales.
2. **Hierarchical Clustering:** Generating a Dendrogram using Ward's linkage and applying Agglomerative Clustering to identify the three natural wine cultivars.
3. **DBSCAN Clustering:** Experimenting with density-based clustering by tuning `eps` and `min_samples` parameters.
4. **Analysis & Metrics:** Evaluating cluster quality using Silhouette, Homogeneity, and Completeness scores.

## Key Insights & Results

### Hierarchical Clustering
- **Success:** The Dendrogram successfully revealed three distinct branches, matching the known wine cultivars.
- **Visualization:** Scatter plots showed clear separation between the clusters when plotted against Alcohol and Color Intensity.
- **Strength:** This algorithm was the most effective for this dataset as it utilizes the connectivity and topology of the data points.

### DBSCAN Clustering
- **Challenges:** DBSCAN proved highly sensitive to the high dimensionality (13 features) of the dataset.
- **The "Mega-Cluster" Issue:** With parameters set to `eps=2.6` and `min_samples=4`, the algorithm identified **one dominant cluster (158 points)** and 20 noise points. 
- **Metric Breakdown:**
    - **Homogeneity (0.052):** Near-zero homogeneity indicates that the algorithm failed to separate the three different cultivars, lumping them into one mass.
    - **Silhouette Score (0.161):** Indicated significant overlap between the clusters.
- **Conclusion:** The Wine dataset lacks the distinct "density gaps" required for DBSCAN to work effectively. The chemical profiles are too similar in the 13D space, leading the algorithm to "bridge" the different wine types.

## Challenges Faced
- **Curse of Dimensionality:** In 13D space, Euclidean distance becomes less meaningful, making it difficult for DBSCAN to find "valleys" of low density between classes.
- **Parameter Sensitivity:** Tuning `eps` was a delicate balance; lowering it led to 80% of the data being labeled as noise, while raising it slightly merged all clusters into one.
