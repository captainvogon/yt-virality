# Predicting YouTube Virality: A Statistical Analysis of YouTube Metrics

## Introduction

With the rapid growth of online video platforms such as YouTube, millions of videos are uploaded every day. However, only a small percentage of these videos become viral - receiving a very large number of views, likes, and comments within a short period. Understanding why certain videos go viral while others do not is an important problem in statistics and data analysis. Viral videos often depend on multiple factors such as viewer engagement, upload timing, video duration, and channel popularity.

The goal of this project is to analyse YouTube trending video metrics using a full statistical pipeline - spanning descriptive statistics, probability distributions, Monte Carlo simulation, statistical inference, dimensionality reduction, clustering, and time series analysis - to identify patterns associated with video virality and determine which factors most strongly influence a video's popularity.

This project was completed as part of the course **PHY5132/6132/AOE5132 - Statistics and Data Analysis**.

---

## Dataset

**YouTube Trending Videos Dataset - Daily Update**
Source: [Kaggle](https://www.kaggle.com/datasets/asaniczka/trending-youtube-videos-113-countries)

The dataset contains daily trending video records across 110 countries, covering the period from late 2024 to early 2026. After cleaning (removing the Movies category which had no view data, and capping video duration at 60 minutes to exclude livestreams and movie uploads), the working dataset contains approximately **4.8 million rows** across **15 video categories**.

Key columns used:
- `video_view_count`, `video_like_count`, `video_comment_count`
- `channel_subscriber_count`, `video_duration`
- `video_category_id`, `video_trending_country`
- `video_published_at`, `video_trending__date`

A video is defined as **viral** if its view count falls in the top 10% of the dataset (≥ ~25 million views).

---

## Research Questions

1. What statistical patterns exist in YouTube video engagement metrics?
2. Which factors most strongly influence video virality?
3. Can we model and simulate the distribution of video views?
4. How does virality probability differ across categories, and how uncertain are those estimates?
5. What do unsupervised methods reveal about natural groupings of trending videos?
6. How does trending video volume and viewership evolve over time?

---

## Methods Used

- Descriptive statistics and correlation analysis
- Distribution fitting: log-normal (view counts), Beta (like rate), Gamma (time to trend)
- Bootstrap resampling and Monte Carlo simulation
- One-way ANOVA and logistic regression
- Bayesian inference with Beta prior vs frequentist proportion estimation
- Principal component analysis (PCA)
- K-means clustering
- Time series smoothing and trend analysis

---

## Key Findings

- **Category matters enormously**: Howto & Style and Pets & Animals have viral rates of ~30%, while Gaming sits at ~1% despite being the largest category by video count
- **Short videos dominate**: videos under 1 minute have a median view count 10× higher than videos over 5 minutes
- **Subscriber count alone is not enough**: large channels appear across the full range of view counts - audience size does not guarantee virality
- **Likes are the strongest predictor**: logistic regression shows like count (corr = 0.89 with views) and subscriber count are the top positive drivers; duration is a negative predictor
- **Three natural video tiers exist**: clustering identifies a low-engagement tier (median 314k views, ~0% viral), a mid-tier, and a high-viral tier (median 7.3M views, ~22% viral rate)
- **Sports content trends fastest**: Sports videos accumulate ~55k views per hour before trending - roughly 3× the rate of Gaming

---

## Repository Structure

```
- data.parquet                        # Dataset from Kaggle, formatted as .parquet file
- yt-virality.ipynb                   # main jupyter notebook
- README.md
```
