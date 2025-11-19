# 🎬 What Makes a Movie *Timeless*?
### A Data + Machine Learning Analysis Using TMDB Metadata (200 Movies)

This project explores a surprisingly difficult question:

## **What makes a movie timeless — a film that stays culturally relevant long after its release?**

Using a dataset of 200 high-engagement films scraped directly from the TMDB API, I collected metadata, engineered features, and trained a supervised logistic regression model to analyze which factors most strongly predict whether a movie endures or fades.

---

# 📦 Repo Contents

✔ **Jupyter Notebook** — scraping TMDB, cleaning data, engineering features, training the ML model  
✔ **All visualizations** referenced in the Medium article  
✔ **Final Medium write-up** (linked below)  
✔ **Reproducible ML workflow** for cultural longevity analysis  

---

# 🔗 Medium Article — Final Submission

**“What Makes a Movie Timeless? Using Data and Supervised Learning to Find Out”**  
👉 https://medium.com/@kwanjosh25/what-makes-a-movie-timeless-a-data-driven-look-using-tmdb-and-supervised-learning-9eff432fac6e  

This README is designed to accompany and reinforce that article.

---

# 📂 Project Structure

| Path / File | Description |
|-------------|-------------|
| `tmdb_timeless_movies.csv` | 200-row cleaned dataset |
| `movie_timeless_analysis.ipynb` | Full scraping + ML notebook |
| `visuals/` | Folder containing saved plots used in the article |
| `README.md` | This file |

# 🎯 Project Goal

Identify **non-obvious** patterns in popular films that help explain why some movies become timeless while others fade — and explore how machine learning can support decisions such as:

- film studio investment

- streaming platform catalog curation

- franchise strategy

- marketing prioritization

- long-term content licensing

# 📊 Dataset Overview

The dataset was created programmatically using the TMDB API, collecting metadata for **200 films**, including:

### Audience Metrics

- vote_average

- vote_count

- popularity

### Economic Metrics

- budget

- revenue

### Content Features

- one-hot encoded genre_ids

- cast_size

- production_companies

- runtime

### Temporal

- release_year

- movie_age

- Target Label

- timeless — manually assigned (0 or 1)

Class Breakdown
Total films: 200
Timeless = 26
Not timeless = 174
This strong imbalance influences model performance and evaluation.

# 🧹 Data Collection & Cleaning 

### ✔ Scraping (Python + TMDB API)
Libraries used:
```import requests
import pandas as pd
``` 
Scraping process:

1. Fetch popular movie IDs page-by-page
2. Query /movie/{id} to pull metadata
3. Query /movie/{id}/credits for cast size
4. Extract + normalize nested JSON fields
5. Convert genre_ids to one-hot vectors
6. Engineer features (movie_age, cast_size)
7. Append results into a structured DataFrame
Example record creation:
```record = {
    "id": movie_id,
    "title": details.get("title"),
    "release_date": details.get("release_date"),
    "release_year": int(details.get("release_date", "0000")[:4]) 
                    if details.get("release_date") else None,
    "budget": details.get("budget"),
    "revenue": details.get("revenue"),
    "runtime": details.get("runtime"),
    "popularity": details.get("popularity"),
    "vote_average": details.get("vote_average"),
    "vote_count": details.get("vote_count"),
    "genre_ids": [g["id"] for g in details.get("genres", [])],
    "production_companies": len(details.get("production_companies", [])),
    "cast_size": len(credits.get("cast", [])),
}
``` 

# ✔ Cleaning Steps
- Filled missing numeric fields with 0
- Normalized budget/revenue values
- Handled SettingWithCopyWarning correctly
- Removed malformed genre metadata
- Verified no duplicates and validated row count = 200

# 🧠 Modeling Approach

### ✔ Supervised Learning Model

Logistic Regression

### ✔ Why Logistic Regression?

- The target (timeless) is binary
- Coefficients provide interpretable insights
- Handles imbalance with class weights
- Works well with mixed numerical + one-hot features

### ✔ Feature Groups
Audience Metrics

vote_average, vote_count, popularity

Economic

budget, revenue

Content

Genres (one-hot), runtime, cast_size, production_companies

Temporal

movie_age

### ✔ Evaluation Methods
- Confusion matrix
- Classification report
- Manual inspection of misclassified samples
- Re-running the notebook to ensure reproducibility

# 🔍 Key Findings
1. Highly Rated Movies Age Better

vote_average and metrics of audience engagement were top predictors.

3. Certain Genres Contribute to Longevity

Drama, Mystery, Fantasy, and Sci-Fi appeared frequently in timeless films.

3. Age Matters

Older films outperform new releases in timelessness likelihood.

4. Budget Does Not Predict Longevity

High-budget films often fade; cultural impact matters more.

5. Timeless Films Follow Consistent Narrative Archetypes

Genre combinations and story structures appear to influence longevity.

# 🧪 Validation
To ensure correctness:

- Verified random samples against TMDB manually
- Checked outliers (invalid budgets, missing release years)
- Hand-reviewed five misclassified films
- Compared ChatGPT code guidance with notebook output
- Ran the notebook from scratch to validate reproducibility

# 📉 Limitations
- Only 200 films — larger datasets may yield more robust patterns
- Timelessness is subjective (but defined consistently)
- Class imbalance affects precision for timeless films
- TMDB popularity may skew toward newer releases
- Lacks rich textual features like scripts or reviews

# 🧰 Technologies Used
- Python
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-learn
- Requests / TMDB API
- Jupyter Notebook

This project demonstrates:
- Real API scraping
- Feature engineering
- Binary classification modeling
- Visual storytelling
- Reproducible data science workflow

🙌 Credits
Dataset collected & curated by Joshua Kwan
Analysis, visualizations, and writing by Joshua Kwan
TMDB API used under fair-use academic guidelines.
