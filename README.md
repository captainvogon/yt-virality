# Predicting YouTube Virality: A Statistical Analysis of YouTube Trends

## Introduction

With the rapid growth of online video platforms such as YouTube, millions of videos are uploaded every day. However, only a small percentage of these videos become viral - receiving a very large number of views, likes, and comments within a short period. Understanding why certain videos go viral while others do not is an important problem in statistics and data analysis. Viral videos often depend on multiple factors such as viewer engagement, upload timing, video duration, and channel popularity.

The goal of this project is to analyse YouTube trending video metrics using a full statistical pipeline to identify patterns associated with video virality and determine which factors most strongly influence a video's popularity.

This project was completed as part of the course **PHY5132/6132/AOE5132 - Statistics and Data Analysis**.
 
## Dataset

**YouTube Trending Videos Dataset - Daily Update**
Source: [Kaggle](https://www.kaggle.com/datasets/asaniczka/trending-youtube-videos-113-countries)

The dataset contains daily trending video records across 110 countries, covering the period from late 2024 to early 2026. After cleaning (removing the Movies category which had no view data, and capping video duration at 60 minutes to exclude livestreams and movie uploads), the working dataset contains approximately **7 million rows** across **15 video categories**.

Key columns used:
- Engagement - `video_view_count`, `video_like_count`, `video_comment_count`
- Channel - `channel_subscriber_count`, `video_duration`
- Content - `video_category_id`, `video_trending_country`
- Temporal - `video_published_at`, `video_trending__date`

## Defining Virality

A key challenge in this project was defining virality in a way that is both meaningful and statistically robust. A naive definition based purely on high view counts is insufficient, as it heavily biases toward massive, established channels.

Instead, we defined virality using a View Multiplier, which measures how a video performs relative to the channel's existing baseline audience:

```Virality Score = View Count / Subscriber Count```

This creates a level playing field, highlighting "breakout" content. For classification purposes, videos in the top 10% of this distribution are labeled as Viral (1), while the remaining 90% are labeled as Normal (0).

## Research Questions

1. What statistical distributions govern YouTube video engagement and "time-to-trend"?
2. Do certain days of the week or specific months yield a higher share of trending videos?
3. Which metadata factors (duration, channel size, title length, tags) most strongly predict a viral hit?
4. Can we build a highly precise logistic regression model to predict if a video will go viral or not?

## Methods Used

- Exploratory Data Analysis: Spearman correlation and non-parametric comparisons.
- Statistical Distribution Fitting: Log-Normal fitting for virality scores and Gamma fitting for incubation time (hours to trend).
- Time Series Analysis: Day-of-week trends and category-specific monthly share tracking.
- Predictive Modeling: Logistic Regression with balanced class weights.
- Threshold Optimization: Fine-tuning decision boundaries using ROC curves, Precision-Recall curves, and custom Confusion Matrices to minimize Type I errors (False Positives).

## Key Findings

- The Shape of Virality: Viral hits are exceptionally rare and follow a steep Log-Normal distribution. The algorithm batches these trends, typically surfacing them within the first 72 hours of publication (following a Gamma distribution).
- The "Short & Niche" Formula: Our Logistic Regression model revealed that Duration and Subscriber Count are the strongest negative predictors of virality. The algorithm highly favors short-form content from smaller, breakout creators over long-form content from established giants.
- By optimizing our predictive model to a high-confidence 0.75 probability threshold, we successfully built a recommendation engine that catches roughly 46% of all viral hits while keeping the False Positive rate safely under 9%.

> Add More...

## Repository Structure

```
- data.parquet                        # Dataset from Kaggle (formatted as .parquet)
- yt-virality.ipynb                   # Main statistical, time-series, and predictive analysis
- thumbnail.ipynb                     # Visual analysis of video thumbnails
- README.md                           # Project documentation
```
