# Content-Recommendation
Movies • Books • Anime • TV Shows • Songs

# Overview

This project implements a multi-domain hybrid recommendation system capable of generating personalized suggestions across movies, books, anime, TV shows, and songs. It is designed to run efficiently in Google Colab, with careful memory control and dataset sampling to avoid crashes. The system combines collaborative filtering and content-based techniques, allowing it to work even in cold-start scenarios where no user history is available. A Gradio interface is included to make the model easy to explore interactively.

# System Architecture

The system follows a simple, modular pipeline that makes it easy to extend or modify:

1. Data Loading – Download or upload datasets for each domain.
2. Standardization – Convert all datasets to a unified format (itemId, title, genres, userId, rating).
3. Sampling & Cleanup – Limit dataset size to maintain Colab stability.
4. Model Training – Train one standalone hybrid recommender per domain.
5. Genre Extraction – Build a clean list of genres for filtering in the UI.
6. Gradio Interface – Provide an interactive way to generate, filter, and visualize recommendations.

Each domain operates independently but uses the same underlying model pipeline, making the system scalable and easy to maintain.

# Methods / Model Used

The recommendation engine uses a hybrid approach combining the strengths of both Collaborative Filtering (CF) and Content-Based Filtering (CBF):

1. Collaborative Filtering (SVD):
-> Builds a sparse user–item matrix.
-> Applies truncated Singular Value Decomposition (SVD).
-> Learns low-dimensional embeddings for users and items.
-> Predicts affinity through vector dot products.

2. Content-Based Filtering (TF-IDF):

-> Extracts text features from genres or authors.
-> Computes item–item similarity using TF-IDF and cosine similarity.
-> When user history exists, compares new items to previously rated ones.
-> In cold-start cases, uses keyword-based matching.

3. Hybrid Model:

-> Combines CF and content scores using weighted blending (default 70% CF, 30% content).
-> Supports switching between CF-only, Content-only, or Hybrid modes in the UI.
-> This hybrid strategy ensures meaningful recommendations even with sparse data or new users.

# Datasets

The system supports multiple content domains. The main datasets used are:

1. MovieLens Latest Small (movies + ratings)
2. Goodbooks-10k (book metadata + large rating matrix)
3. Anime Recommendations Database (anime info + user ratings)
4. TV Shows & Songs (small curated datasets included in the notebook)

Large datasets are sampled (default: up to 20,000 ratings) to avoid memory issues in Colab while still providing enough signal for training.

# Requirements

1. Python 3.8+
2. Google Colab recommended (due to built-in file uploads, GPU options, and Kaggle integration)

Required Python libraries:

-> pandas, numpy, scipy, scikit-learn, gradio, requests, kaggle

Optional:

1. kaggle.json (for automatic dataset download)
2. API keys for TMDB, Google Books, or Jikan (for posters; not required)

# Conclusion

This project provides a complete and extensible framework for building hybrid recommenders across multiple domains. It is optimized for ease of use, stability, and clarity, making it suitable for learning, experimentation, academic projects, and prototyping. The modular design, standardized pipeline, and intuitive Gradio interface allow users to explore recommendations interactively while keeping technical complexity manageable.
