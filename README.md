# DSA 4060XA – Week 6: Evaluating Recommender Systems

**Course:** DSA 4060XA – Recommender Systems  
**Practical Lab:** Week 6   
**Author:** Samantha Masaki  
**Project:** Movie Recommendation System Evaluation

---

## 1. Project Overview

This project evaluates and compares three approaches to movie recommendation systems: Popularity-Based Recommendation, Content-Based Filtering, and Item-Based Collaborative Filtering.

The practical focuses on measuring how effectively each model predicts user ratings and generates useful recommendations. Rather than selecting a model based on one metric alone, the evaluation considers prediction accuracy, ranking quality, catalogue coverage, novelty, and diversity.

The project demonstrates how recommendation systems can be assessed for a movie-streaming platform where users want relevant suggestions while also discovering movies beyond the most popular titles.

## 2. Project Objectives

The main objectives are to:

1. Implement and evaluate a popularity-based recommendation baseline.
2. Apply content-based filtering using movie features.
3. Evaluate item-based collaborative filtering.
4. Split the ratings data into training and testing sets using each user's latest interaction for testing.
5. Compare rating prediction performance using Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).
6. Evaluate recommendation ranking using Precision@3, Recall@3, and NDCG@3.
7. Measure catalogue coverage, novelty, and diversity.
8. Interpret the strengths, weaknesses, and trade-offs of each recommendation approach.
9. Identify an appropriate model for a streaming service seeking relevant and varied recommendations.

## 3. Dataset Description

The practical uses movie metadata and user-rating data.

The dataset contains:

| Dataset characteristic | Value |
|---|---:|
| Number of users | 12 |
| Number of movies | 20 |
| Number of ratings | 120 |
| Rating scale | 1–5 |
| Test strategy | Latest interaction per user |

### Movies dataset

The movie data includes:

- `movie_id`: Unique identifier for each movie.
- `title`: Movie title.
- `genres`: Genre information used to describe movie content.

### Ratings dataset

The ratings data includes:

- `user_id`: Identifier for the user who rated the movie.
- `movie_id`: Identifier for the rated movie.
- `rating`: User's rating on a scale of 1–5.
- `timestamp`: Time associated with the rating.

The movie features support content-based recommendations, while the user-rating history supports popularity-based and collaborative approaches.

## 4. Technologies and Libraries

The project uses Python and standard data science tools.

| Tool or library | Purpose |
|---|---|
| Python | Implementation and evaluation |
| Jupyter Notebook | Interactive development and documentation |
| pandas | Data manipulation and tabular analysis |
| NumPy | Numerical calculations |
| scikit-learn | Similarity calculations and machine-learning utilities |
| matplotlib | Data visualization |

## 5. Recommendation Approaches

### 5.1 Popularity-Based Recommendation

The popularity baseline recommends movies based on their popularity or rating statistics within the training data.

This provides a simple benchmark against which the more personalized approaches can be compared.

**Strengths**
- Simple to implement.
- Easy to understand and explain.
- Does not require a detailed user preference profile.

**Limitations**
- May recommend similar movies to many users.
- Can favour already-popular movies.
- May offer limited personalization.

### 5.2 Content-Based Filtering

Content-based filtering uses movie characteristics, particularly genres, to identify movies with similar features and recommend items aligned with a user's preferences.

The approach can provide recommendations based on the relationship between movie features and the user's rating history.

**Strengths**
- Uses movie content to support personalization.
- Can recommend items based on identifiable preferences.
- Helps explain why movies may be similar.

**Limitations**
- Depends on the quality of movie metadata and feature representations.
- May recommend movies that are too similar to previously liked items.
- Performance can be limited when user preference information is sparse.

### 5.3 Item-Based Collaborative Filtering

Item-based collaborative filtering uses patterns in user-rating data to identify relationships between movies and generate recommendations based on related items.

Unlike content-based filtering, it relies on rating patterns rather than only movie characteristics.

**Strengths**
- Can identify relationships that are not obvious from genres alone.
- Can support personalized recommendations.
- Achieved the best rating prediction results in this evaluation.

**Limitations**
- Performance depends on the availability of user-rating data.
- Sparse data can make similarity estimates unreliable.
- Good rating prediction does not automatically guarantee relevant top-ranked recommendations.

## 6. Evaluation Methodology

### 6.1 Train-Test Split

The ratings data is divided into training and testing sets by holding out the latest interaction for each user.

The training set is used to build or support the recommendation models, while the test set evaluates their performance on held-out interactions.

The notebook reports:

- Training interactions: **108**
- Testing interactions: **12**

This approach helps assess recommendations against interactions that were not used for training. However, the small dataset limits how broadly the results can be generalized.

### 6.2 Rating Prediction Metrics

**Mean Absolute Error (MAE)** measures the average absolute difference between predicted and actual ratings. Lower values indicate better prediction accuracy.

**Root Mean Squared Error (RMSE)** measures prediction error while penalizing larger errors more strongly. Lower values indicate better performance.

### 6.3 Ranking Metrics

The ranking evaluation uses \(K=3\).

- **Precision@3:** The proportion of the three recommended items that are relevant.
- **Recall@3:** The proportion of relevant held-out items recovered in the recommendations.
- **NDCG@3:** Measures the ranking quality of relevant recommendations, rewarding relevant items placed higher in the list.

For the ranking evaluation, a held-out rating of **4 or higher** is treated as relevant.

### 6.4 Catalogue Coverage

Catalogue coverage measures the proportion of unique movies recommended across users relative to the total number of movies in the catalogue.

Higher coverage means the system exposes users to a larger portion of the available catalogue.

### 6.5 Novelty

Novelty measures how uncommon the recommended movies are based on their interaction frequencies in the training data.

Higher novelty scores indicate recommendations that are less common under the implemented measure.

### 6.6 Diversity

Diversity measures how different the movies within recommendation lists are using genre-based cosine similarity.

In this implementation, diversity is calculated as one minus the average pairwise similarity. Higher values indicate more varied recommendations by genre.

## 7. Rating Prediction Results

The following results were obtained from the notebook's rating prediction evaluation.

| Model | MAE | RMSE |
|---|---:|---:|
| Popularity Baseline | 1.0859 | 1.2010 |
| Content-Based | 1.0939 | 1.3807 |
| Item-Based CF | 0.9243 | 1.0697 |

### Interpretation

**Item-Based Collaborative Filtering** achieved the lowest MAE (**0.9243**) and RMSE (**1.0697**), making it the strongest model for rating prediction among the three evaluated approaches.

The popularity baseline achieved an MAE of **1.0859** and RMSE of **1.2010**.

Content-based filtering achieved an MAE of **1.0939** and RMSE of **1.3807**, performing slightly worse than the popularity baseline on both rating prediction metrics.

## 8. Ranking Evaluation Results

The notebook evaluates recommendation relevance and ranking using Precision@3, Recall@3, and NDCG@3.

| Model | Precision@3 | Recall@3 | NDCG@3 |
|---|---:|---:|---:|
| Popularity Baseline | 0.0667 | 0.2000 | 0.1000 |
| Content-Based | 0.0667 | 0.2000 | 0.2000 |
| Item-Based CF | 0.0000 | 0.0000 | 0.0000 |

### Interpretation

The popularity baseline and content-based model recorded the same Precision@3 (**0.0667**) and Recall@3 (**0.2000**).

Content-based filtering achieved the highest NDCG@3 (**0.2000**) among the three approaches, compared with **0.1000** for popularity-based recommendations.

Item-Based Collaborative Filtering recorded **0.0000** for all three ranking metrics. Although it performed best on rating prediction, its recommendations did not recover relevant held-out items under the notebook's ranking evaluation. This demonstrates why rating prediction accuracy alone is insufficient for choosing a recommender system.

## 9. Catalogue Coverage, Novelty, and Diversity

The following results compare how broadly each model recommends movies and how varied or uncommon its recommendations are.

| Model | Coverage | Novelty | Diversity |
|---|---:|---:|---:|
| Popularity Baseline | 0.3500 | 1.6894 | 0.7361 |
| Content-Based | 0.7000 | 1.3436 | 0.5417 |
| Item-Based CF | 0.8500 | 1.6948 | 0.7802 |

### Interpretation

**Catalogue Coverage:** Item-Based CF achieved the highest coverage at **0.8500**, followed by content-based filtering at **0.7000** and the popularity baseline at **0.3500**.

**Novelty:** Item-Based CF achieved the highest novelty score at **1.6948**, closely followed by the popularity baseline at **1.6894**. Content-based filtering recorded **1.3436**.

**Diversity:** Item-Based CF achieved the highest diversity score at **0.7802**, followed by popularity-based recommendations at **0.7361**. Content-based filtering recorded **0.5417**.

These results suggest that Item-Based CF exposes users to more of the catalogue and generates more varied, less common recommendations under the implemented metrics. However, its ranking scores indicate that these recommendations did not successfully retrieve the relevant held-out items in this evaluation.

## 10. Overall Findings

The results demonstrate that recommendation systems must be evaluated across several dimensions.

- **Best rating prediction:** Item-Based Collaborative Filtering, with MAE **0.9243** and RMSE **1.0697**.
- **Best Precision@3:** Popularity Baseline and Content-Based, tied at **0.0667**.
- **Best Recall@3:** Popularity Baseline and Content-Based, tied at **0.2000**.
- **Best NDCG@3:** Content-Based, at **0.2000**.
- **Best catalogue coverage:** Item-Based CF, at **0.8500**.
- **Best novelty:** Item-Based CF, at **1.6948**.
- **Best diversity:** Item-Based CF, at **0.7802**.

No model dominates every metric. The most suitable model depends on whether the primary goal is rating accuracy, relevance, discovery, diversity, or explainability.

## 11. Business Scenario and Model Recommendation

Consider a streaming service that wants to help users discover relevant movies without allowing the same popular titles to dominate every recommendation list.

Item-Based Collaborative Filtering is a promising candidate for further development because it achieved the best rating prediction, catalogue coverage, novelty, and diversity results.

However, it should **not be deployed as-is**. Its Precision@3, Recall@3, and NDCG@3 scores were all zero. The recommendation ranking logic, relevance definition, and implementation should be investigated before production use.

A practical next step is to improve the ranking approach and test it using a larger, more representative dataset.

## 12. Limitations

The evaluation has several limitations:

1. **Small dataset:** The data contains only 12 users, 20 movies, and 120 ratings.
2. **Small test set:** Only 12 interactions were held out for testing.
3. **Limited generalizability:** Results from a small dataset may not represent the behaviour of a real streaming platform.
4. **Ranking-performance gap:** Item-Based CF performs well on rating prediction but records zero ranking metrics.
5. **Limited movie information:** The content-based approach depends on the available movie features.
6. **Limited evaluation scope:** Further testing is needed to assess how performance changes for different values of \(K\), relevance thresholds, and user groups.

## 13. Possible Future Improvements

Potential extensions include:

- Evaluating Precision@K, Recall@K, and NDCG@K at different values of \(K\).
- Changing the relevance threshold from ratings of 4 or higher to ratings equal to 5.
- Comparing recommendations for multiple users to examine personalization.
- Investigating why Item-Based CF has zero ranking scores.
- Testing the approaches on a larger dataset.
- Exploring hybrid recommendation approaches that combine content features and collaborative signals.
- Improving ranking relevance while maintaining catalogue coverage, novelty, and diversity.

These are proposed extensions; they should only be reported as completed after implementation and evaluation.

## 14. How to Run the Project

1. Clone or download this repository.
2. Open the project folder in VS Code or Jupyter Notebook.
3. Ensure Python and the required libraries are installed.
4. Place the dataset files in the locations expected by the notebook.
5. Open the Week 6 `.ipynb` notebook.
6. Run the cells in order, from data loading through model evaluation.
7. Compare the generated results with the findings documented above.

### Install the main dependencies

```bash
pip install pandas numpy scikit-learn matplotlib jupyter
```

The dataset filenames and notebook filename should match the files included in the repository.

## 15. Repository Structure

The repository contains the Week 6 practical notebook and this README document.

A recommended structure is:

```text
DSA4060_W6_Movies/
├── README.md
├── DSA4060_Week6_Recommender_Evaluation.ipynb
└── data/
    ├── movies.csv
    └── ratings.csv
```

The structure above is illustrative. Actual filenames and folders may differ depending on the files committed to the repository.

## 16. Conclusion

This practical compares popularity-based recommendation, content-based filtering, and item-based collaborative filtering using rating prediction, ranking, coverage, novelty, and diversity metrics.

Item-Based Collaborative Filtering produced the strongest rating prediction results and the highest catalogue coverage, novelty, and diversity. However, its zero ranking scores reveal a significant limitation: strong rating prediction does not necessarily produce relevant top-ranked recommendations.

The key lesson is that recommender systems should be evaluated using multiple complementary metrics. A reliable recommendation system must balance accuracy, relevance, discovery, diversity, and the needs of its users.

