# Catalog Feed Recommendation System Evaluation

## Overview
This project focuses on building a scalable PySpark pipeline to evaluate the performance of a catalog feed recommendation system. The system computes weekly metrics for user engagement, recommendation relevance, and value sensitivity, segmented by user cohorts such as power users and new users.

## Key Metrics
1. **User Engagement**:
   - Clicks
   - Views
   - Scroll depth

2. **Recommendation Relevance**:
   - **Recall@k**: Measures how many of the top-k recommendations were relevant.
   - **NDCG@k**: Normalized Discounted Cumulative Gain at k, quantifying the ranking quality of recommendations.

3. **Value Sensitivity**:
   - **View-weighted price**: Measures the price of viewed items weighted by engagement.

## Pipeline Design

The pipeline is modular and designed to run on Databricks, processing large-scale data using PySpark. The major steps include:

1. **Data Ingestion**:
   - Pulls data from multiple sources, including Mixpanel logs, order data, and catalog prices.

2. **Cohort Creation**:
   - The pipeline defines 3 user cohorts based on order history:
     - **22OD+**: Users with 22+ orders.
     - **<22OD**: Users with less than 22 orders.
     - **0-1 FY Feed**: Users with 0-1 feed interactions in the first year.

3. **Metric Calculation**:
   - Calculates interaction-based metrics (e.g., clicks_cdf, views_cdf, scroll depth).
   - Evaluates ranking quality using `pyspark.mllib.evaluation.RankingMetrics`.

4. **Output**:
   - All metrics are outputted into structured DataFrames for easy reporting and table storage.

## Results
- Enabled weekly automated reporting of the recommendation system's performance.
- Provided insights into areas of underperformance (e.g., low NDCG in the 0-1 FY Feed cohort).
- Reduced manual analysis time and improved decision-making for tuning the recommendation system.

