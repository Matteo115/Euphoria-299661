# Euphoria Project: Classify Islands by Happiness

### Team Members:
- Matteo Bruni
- Federico Romano Gargarella
- Matteo Rapisarda

---

## [Section 1] Introduction

This project explores the unique environment of **Euphoria**, a virtual archipelago where each island offers diverse experiences to its inhabitants. The goal is to identify key characteristics that contribute to island happiness and create actionable groupings of islands based on these traits. These groupings aim to assist virtual travelers in selecting ideal destinations tailored to their preferences and needs.

Key aspects of this project include:
- **Understanding happiness drivers**: Investigating environmental, geographic, and amenity-related factors that impact happiness.
- **Data-driven insights**: Leveraging clustering techniques to reveal patterns and relationships.
- **Practical applications**: Helping stakeholders (travelers, island developers) make data-informed decisions for improving resident satisfaction.

By systematically analyzing and clustering islands, this project provides insights into what makes an island "happy," offering tools for better decision-making in virtual tourism.

---

## [Section 2] Methods

### Exploratory Data Analysis (EDA)
EDA was conducted to gain insights into the dataset and prepare it for clustering analysis. Key steps included:

- **Initial Inspection**: The dataset was examined for structure, completeness, and basic statistics. Duplicate rows were identified and removed to ensure data integrity.
- **Outlier Handling**: Outliers in numerical features were detected using Z-Scores. Extreme values were capped to reduce their impact on clustering.
- **Missing Values**: Missing data was analyzed using visualizations (`missingno`) and summary statistics. For missing values:
  - Columns with excessive missing values (>30%) were dropped.
  - For numerical features, missing values were imputed using mean or median, depending on skewness.
  - For categorical features, the most frequent value was used for imputation.

### Feature Selection
Features were selected based on their relevance to happiness and clustering objectives. The following steps guided this process:
- **Correlation Analysis**: Numerical features were analyzed for multicollinearity, and highly correlated features were excluded to prevent redundancy.
- **Domain Knowledge**: Geographic, environmental, and amenity-related features were prioritized due to their expected influence on happiness.
- **Dimensionality Reduction**: Principal Component Analysis (PCA) was used to reduce feature dimensionality, retaining 95% of the variance.

### Clustering Algorithms
To segment the islands, three clustering algorithms were tested:

- **KMeans Clustering**:
  - *Description*: Partitions data into `k` clusters by minimizing intra-cluster variance.
  - *Implementation*: Several `k` values were tested using the elbow method and silhouette score.
  - *Pros*: Fast and efficient for large datasets.
  - *Cons*: Requires specifying the number of clusters.

- **DBSCAN**:
  - *Description*: Groups points based on density, identifying noise for better robustness.
  - *Implementation*: Parameters `eps` and `min_samples` were tuned to optimize clustering performance.
  - *Pros*: No need to predefine the number of clusters; handles noise and outliers effectively.
  - *Cons*: Struggles with varying density in clusters.

- **Hierarchical Clustering**:
  - *Description*: Builds a dendrogram to visualize cluster relationships.
  - *Implementation*: Agglomerative clustering with linkage methods (ward, complete, average) was tested.
  - *Pros*: Provides a hierarchy of clusters.
  - *Cons*: Computationally intensive for large datasets.

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
- **Purpose**: Segment islands into groups based on happiness and related features.
- **Baseline(s)**: Random clustering and basic statistical groupings.
- **Evaluation Metrics**: Silhouette score, Davies-Bouldin index, and manual validation against known patterns.

### Experiment 2: Feature Importance
- **Purpose**: Determine which factors most strongly influence happiness levels.
- **Baseline(s)**: No clustering (raw data analysis).
- **Evaluation Metrics**: Feature correlations and importance weights in clustering models.

---

## [Section 4] Results

### Main Findings
- Islands can be grouped into 3-5 distinct clusters based on happiness levels and features.
- Environmental factors like greenery and access to water strongly correlate with happiness scores.

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
This project highlights the potential of clustering to segment islands in Euphoria by happiness levels. By leveraging geographic and environmental data, we identified actionable insights for improving traveler experiences.

### Open Questions and Future Work
While this work effectively segments islands, further exploration is needed to:
- Incorporate temporal data to assess seasonality effects.
- Evaluate traveler satisfaction metrics for validation.
- Explore more advanced clustering methods for dynamic updates.
