🎬 What Makes a Movie “Timeless”?
A Data + Machine Learning Analysis using TMDB Metadata (200 Movies)

This project explores a surprisingly difficult question:

What makes a movie timeless — a film that stays culturally relevant long after its release?

Using 200 of the most-popular movies on TMDB, I scraped detailed metadata, engineered features, and trained a supervised logistic regression model to analyze which factors most strongly predict whether a movie endures or fades.

This repo contains:

✔ The Python notebook used to scrape TMDB, clean data, build features, and train the model

✔ All figures, charts, and insights referenced in the Medium article

✔ A direct link to the final write-up

✔ A reproducible ML pipeline for analyzing cultural longevity 

🔗 Medium Article (Final Submission)

“What Makes a Movie Timeless? Using Data and Supervised Learning to Find Out”
👉 https://medium.com/@kwanjosh25/what-makes-a-movie-timeless-a-data-driven-look-using-tmdb-and-supervised-learning-9eff432fac6e 

This README is designed to accompany and reinforce that article.

📂 Project Structure

📁 timeless-movies/
│── tmdb_timeless_movies.csv        # 200-row cleaned dataset
│── movie_timeless_analysis.ipynb   # Full scraping + ML notebook
│── visuals/                        # Saved plots used in article
│── README.md                       # (this file)

🎯 Goal

Identify non-obvious patterns in popular films that help explain why some movies become timeless while others are forgotten — and explore how ML can support decisions such as:

- film studio investment

- streaming platform catalog curation

- franchise strategy

- marketing prioritization

- long-term content licensing

📊 Dataset Overview

The dataset was built programmatically using the TMDB API, collecting metadata for 200 high-engagement films, each tagged with:

- vote_average

- vote_count

- popularity

- budget / revenue

- runtime

- release year, movie_age

- genre IDs → one-hot vectors

- cast size

- production companies

- manually assigned “timeless” label (0 or 1)

Counts:

- Total films: 200

- Timeless = 26

- Not timeless = 174

This imbalance influences modeling — and is handled explicitly in the Medium article.

🧹 Data Collection & Cleaning
✔ Scraping (Python + TMDB API)

Functions written using:
import requests
import pandas as pd

Steps included:

Fetching movie IDs page-by-page

Pulling metadata, credits, and details

Normalizing JSON structures

Expanding genre_ids into one-hot columns

Calculating movie_age and cast_size

Merging to a single DataFrame

✔ Cleaning

Filled missing numeric fields with 0

Removed malformed genre strings

Resolved SettingWithCopyWarning

Normalized revenue/budget scales

Verified no duplicates

Confirmed final row count: 200

🧠 Modeling Approach
🎯 Supervised Learning

This project uses:

✔ Logistic Regression

Why?

Our target is binary (timeless vs not timeless)

Interpretability is essential

Handles class imbalance with weighting

Works well with mixed numeric + one-hot data

Feature Set Used

Audience Metrics

vote_average

vote_count

popularity

Economic Metrics

budget

revenue

Content Structure

genre one-hots

runtime

cast_size

Temporal

movie_age

Model Evaluation

Includes:

Confusion matrix

Accuracy

False positive/negative inspection

Hand-review of 5 misclassified films

🔍 Key Findings

(Full details in Medium article)

🎬 1. Popular + Highly Rated Movies Age Best

Vote average and vote count have the strongest positive impact.

🎭 2. Drama, Mystery, Fantasy, and Sci-Fi genres have higher timeless probability

Genre mattered more than expected.

⏳ 3. Older movies are more often timeless

Aging exposes whether a film sustains engagement.

🔥 4. Big budgets don’t guarantee longevity

Economic scale ≠ cultural endurance.

🎯 5. Timeless movies cluster around certain “story archetypes”

Partially captured by genre and vote metrics.

🧪 Validation

To ensure correctness:

Verified records manually against TMDB

Checked outliers (budget errors, malformed release dates)

Reviewed 5 misclassified samples to interpret model behavior

Compared ChatGPT suggestions with actual notebook output

Re-ran the notebook end-to-end to confirm reproducibility

📉 Limitations

Small dataset (200 rows) limits generalization

Class imbalance affects precision

Timelessness is subjective, based on a consistent definition but still opinion-based

TMDB popularity can skew toward recency

No textual data (scripts, reviews, keywords)

Future improvements listed in the article also apply here.

🧩 Technologies Used

Python

Pandas

NumPy

Matplotlib / Seaborn

Scikit-learn

Requests (for API calls)

Jupyter Notebook

TMDB API

This project demonstrates:

Practical data scraping

Feature engineering

Supervised learning

Model interpretation

API integration

Visual storytelling

Research-grade write-up

It pairs a real Medium-ready article with a reproducible ML pipeline.

🙌 Credits

Dataset collected & curated by Joshua Kwan
Analysis, visualizations, and writing by Joshua Kwan
TMDB API used under fair-use academic guidelines

