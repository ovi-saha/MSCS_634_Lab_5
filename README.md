# Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering   
Avijit Saha  
Advanced Big Data and Data Mining (MSCS-634-M20)  
Dr. Satish Penmatsa  
March 12, 2026  
This Repo is Lab 5: Clustering Techniques Using DBSCAN and Hierarchical Clustering for Advanced Big Data and Data Mining (MSCS-634-M20)

## Project Overview
This lab provides a comparative analysis of two unsupervised machine learning algorithms—**Agglomerative Hierarchical Clustering** and **DBSCAN**—applied to the UCI Wine Dataset. The dataset consists of 178 samples with 13 chemical features representing three different wine cultivars.

The objective was to evaluate how well connectivity-based and density-based clustering could recover the original classes of the data.

## Technical Methodology
1. **Preprocessing:** Standardized the 13 chemical features using `StandardScaler` to ensure all features contributed equally to the distance calculations.
2. **Hierarchical Clustering:** - Utilized **Ward’s Linkage** to minimize within-cluster variance.
   - Generated a **Dendrogram** to determine the optimal number of clusters ($k=3$).
3. **DBSCAN Clustering:**
   - Performed parameter tuning using the **K-Distance Plot** method.
   - Tested multiple $(\epsilon)$ and `min_samples` configurations to address the "Mega-Cluster" vs. "Hyper-Fragmentation" issues.
4. **Evaluation:** Assessed models using **Silhouette**, **Homogeneity**, and **Completeness** scores.

## Key Insights & Results

### 1. Hierarchical Clustering (The Success)
- **Results:** Successfully partitioned the data into three balanced groups (**58, 56, and 64 points**).
- **Insight:** This distribution closely matches the actual cultivar sizes in the dataset. Hierarchical clustering proved highly effective because it relies on the data's topological structure (connectivity) rather than a fixed density threshold.

### 2. DBSCAN Clustering (The Challenge)
- **Results:** Produced a **Homogeneity Score of 0.052** and a **Silhouette Score of 0.161**.
- **Observation:** The model resulted in one "mega-cluster" of **158 points** and **20 noise points**.
- **Analysis:** This indicates that the Wine dataset lacks clear "density valleys" between the different cultivars in 13-dimensional space. Increasing the epsilon radius to capture the clusters caused the algorithm to "bridge" different wine types together into a single mass.

## Strengths and Weaknesses Comparison

| Feature | Hierarchical Clustering | DBSCAN Clustering |
| :--- | :--- | :--- |
| **Strengths** | **Highly Accurate for Wine:** Created balanced clusters that aligned with ground truth. | **Outlier Detection:** Successfully isolated 20 specific outliers (noise) from the core data. |
| **Weaknesses** | **Rigidity:** Forces every point into a cluster, potentially ignoring legitimate noise. | **High Dimensionality:** Extremely sensitive to `eps` (Curse of Dimensionality). |
| **Suitability** | **High:** The best choice for this dataset's connectivity-based structure. | **Low:** Unsuitable for class separation due to overlapping densities. |

## Final Conclusion
While DBSCAN is superior for outlier detection and non-spherical clusters, it is not the ideal choice for the Wine dataset. **Hierarchical Clustering** remains the superior method for this application, providing a clear, balanced, and accurate classification of the cultivars.
