# Euphoria Project: Classify Islands by Happiness

### Team Members:
- Matteo Bruni
- Federico Romano Gargarella
- Matteo Rapisarda

---

## [Section 1] Introduction

This project discusses the unique environment of **Euphoria**, a virtual archipelagos where each island offers its inhabitants unique experiences. The main goal is to highlight the main characteristics that allow islands to be happy and to put together useful classes of islands using these characteristics. These classes will help virtual travelers choose the best places based on their tastes and needs.

Key aspects of this project include:
- **Understanding happiness drivers**: Investigating environmental, geographic, and amenity-related factors that impact happiness.
- **Data-driven insights**: Leveraging clustering techniques to reveal patterns and relationships.
- **Practical applications**: Helping travelers and island developers make correct and useful decisions for improving resident satisfaction.

By systematically analyzing and clustering islands, we can get insights of what makes an island "happy", offering tools for better decision-making in virtual tourism and urban planning.

---

## [Section 2] Methods

### Exploratory Data Analysis (EDA)
EDA was conducted to understand the dataset and prepare it for clustering analysis. Key steps included:

- **Initial Inspection**: We analyzed the structure, the completedness and basic statistics of the dataset. We identiifed and removed duplicate rows in order to ensure data integrity.
- **Outlier Handling**: Outliers in numerical features were detected using z-scores. Extreme values were either removed or capped to reduce their impact on clustering.
- **Missing Values**: Missing data was analyzed using visualizations (`missingno`) and summary statistics. For missing values:
  - Columns with more than 30% missing values were dropped.
  - For numerical features, missing values were imputed using mean or median, depending on skewness.
  - For categorical features, the most frequent value was used for imputation.

### Feature Selection
Features were selected based on their relevance to happiness and clustering objectives. Those are the main steps for this process:
- **Correlation Analysis**: Numerical features were analyzed for multicollinearity using pairwise correlation matrices. Features that were very similar (correlation coefficient > 0.8) were removed to prevent redundancy and to make the model easier to understand.
- **Domain Knowledge**: Features that are related to geographic attributes (e.g., proximity to water, terrain), environmental factors (e.g., vegetation, climate), and amenities (e.g., access to services, infrastructure) were prioritized because they are expected to affect happiness.
- **Feature Engineering**: Additional derived features, such as population density and average income per capita, were created to enhance the dataset.
- **Dimensionality Reduction**: Principal Component Analysis (PCA) was applied to reduce the feature dimensionality (number of features) while retaining 95% of the variance. PCA made the task of clustering easier by transforming the features into uncorrelated principal components.

### Clustering Algorithms
In order to segment the islands, we tested 3 different clustering algorithms:

- **KMeans Clustering**:
  - *Description*: KMeans clustering partitions the dataset into a predefined number of clusters (`k`) by minimizing the variance within each cluster. The algorithm assigns each data point to the nearest cluster centroid and iteratively updates centroids to improve the clustering.
  - *Parameters*: The main parameter is `k`, the number of clusters. Several values of `k` were tested using the elbow method (identifies the optimal number of clusters by finding the "elbow point") and silhouette score to determine the optimal number of clusters.
  - *Advantages*:
    - Computationally efficient and can handle large datasets.
    - It Works well when clusters are spherical and of similar size.
  - *Challenges*:
    - Requires specifying the number of clusters beforehand.
    - Sensitive to outliers and non-spherical cluster shapes.
  - *How it was used*: KMeans was used as a baseline clustering method. Its output was used as a starting point to understand the data structure; further improvement in the structure was achieved by the density based (DBSCAN) and hierarchical techniques (Hierarchical clustering).

- **DBSCAN**:
  - *Description*: Density-Based Spatial Clustering of Applications with Noise (DBSCAN) is a clustering algorithm that identifies core samples of high density and expands clusters from them. It groups points that are closely packed together (based on a distance metric) and marks points that are alone in low-density regions as noise.
  - *Parameters*: The two key parameters are:
    - `eps`: The maximum distance between two samples for them to be considered as part of the same neighborhood.
    - `min_samples`: The number of samples (or total weight) in a neighborhood for a point to be considered a core point. This includes the point itself.
  - *Implementation*: These parameters were tuned iteratively. A small `eps` resulted in many small clusters or noise, while a large `eps` merged distinct clusters. Similarly, adjusting `min_samples` affected the granularity (meaning the level of detail) of clustering.
  - *Advantages*:
    - Doesn't require specifying the number of clusters.
    - Handles noise effectively by labeling it as outliers.
    - Finds arbitrarily shaped clusters, making it versatile for non-linear data structures.
  - *Challenges*:
    - Sensitive to the choice of `eps` and `min_samples`.
    - Struggles with datasets containing clusters of different density or very high dimensionality.
  - *Usage in this Project*: DBSCAN was particularly useful for identifying isolated islands and differentiating between densely populated and sparsely populated clusters while treating outliers as noise.

- **Hierarchical Clustering**:
  - *Description*: Hierarchical clustering builds a hierarchy of clusters by either merging smaller clusters (agglomerative) or splitting larger clusters (divisive). The result is a dendrogram that represents the cluster relationships at various levels.
  - *Parameters*: The main parameters include:
    - Linkage method (ward, complete, average): Determines how distances between clusters are calculated.
    - Distance metric: Defines the measure used to calculate distances between points (e.g., Euclidean, Manhattan).
  - *Advantages*:
    - Does not require specifying the number of clusters beforehand.
    - Provides a clear view of cluster relationships through the dendrogram.
  - *Challenges*:
    - Computationally expensive for large datasets.
    - May be sensitive to the choice of distance metric and linkage method.
  - *Usage in this Project*: Hierarchical clustering was used to visualize the relationships between clusters and to get a better understanding of the dataset's structure. The dendrogram provided insights into the natural grouping of islands, guiding us in the selection of an appropriate number of clusters for other methods.

Each algorithm's performance was evaluated using metrics such as silhouette score, Davies-Bouldin index, and manual validation of clusters against known patterns.

### Environment Setup
To recreate the environment, follow these steps:
1. Clone the repository: `git clone [repository-url]`
2. Set up the conda environment:
   ```bash
   conda env create -f environment.yml
   conda activate euphoria-env
   ```
3. Install additional dependencies if needed: `pip install -r requirements.txt`

**Environment Details:**
- Python version: 3.8
- Dependencies: pandas, matplotlib, seaborn, missingno, etc. (attach full `conda list` or `conda env export` as needed).

### Methodology Illustration
Below is a high-level description of the methodology:

- **EDA**: Cleaning and preprocessing the data for clustering.
- **Feature Selection**: Choosing relevant attributes and reducing dimensionality.
- **Clustering**: Testing and evaluating different algorithms.

![Flowchart Placeholder](#)

---

## [Section 3] Experimental Design

### Experiment 1: Clustering Analysis
- **Purpose**: Segmenting the islands into groups based on happiness and related features.
- **Baseline(s)**: Random clustering and basic statistical groupings.
- **Evaluation Metrics**: Silhouette score, Davies-Bouldin index, and manual validation against known patterns.

### Experiment 2: Feature Importance
- **Purpose**: Determine which are the main factors that influence happiness level.
- **Baseline(s)**: No clustering (raw data analysis).
- **Evaluation Metrics**: Feature correlations and importance weights in clustering models.

---

## [Section 4] Results

### Main Findings
- Islands can be grouped into 3-5 distinct clusters based on happiness levels and features.
- Environmental factors like greenery and access to water are strongly correlated with happiness scores.

### Figures and Tables
Below is a placeholder for the main results:

| Metric         | KMeans  | DBSCAN  | Hierarchical |
|----------------|---------|---------|--------------|
| Silhouette Score | 0.65  | 0.58    | 0.62         |
| Clusters Found  | 4      | 3       | 5            |

![Results Placeholder](#)

---

## [Section 5] Conclusions

### Summary
This project highlights the potential of machine learning techniques, like clustering, to segment and classify islands in Euphoria by happiness levels.
Our approach, combining KMeans, DBSCAN, and Hierarchical clustering, revealed strong patterns in island happiness levels that remained consistent across different methodologies. Key findings showed that island happiness is strongly influenced by a combination of:
- Natural environmental factors (vegetation density, access to water, climate patterns)
- Infrastructure development (transportation networks, public facilities)
- Social dynamics (population density, community engagement levels)
- Economic indicators (average income, business diversity)

Those results can be used to help virtual travelers choose the best places based on their tastes and needs as well as to help island developers make correct and useful decisions in order to improve the resident satisfaction.

### Open Questions and Future Work
While this work effectively segments islands, further exploration is needed to:
- Incorporate temporal data to assess seasonality effects.
- Evaluate traveler satisfaction metrics for validation.
- Explore more advanced clustering methods for dynamic updates.
