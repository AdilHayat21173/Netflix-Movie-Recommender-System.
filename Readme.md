# Movie Recommender System: Step-by-Step Guide

This guide walks you through creating a movie recommender system using a Kaggle dataset, text vectorization, and cosine similarity.

## Step 1: Import Libraries and Load Dataset

First,, import the necessary libraries and load the dataset from Kaggle.

1. **Import Required Libraries**: Ensure you have libraries like `pandas` and `sklearn` installed.
2. **Load the Dataset**: Read the dataset from a CSV file into a pandas DataFrame.

## Step 2: Feature Selection

Select relevant features for the recommendation system. 

1. **Select Relevant Features**: Choose columns such as `id`, `title`, `overview`, and `genre` from the dataset.
2. **Combine Text Features**: Create a new column called `tags` by combining the `overview` and `genre` columns.
3. **Drop Original Columns**: Remove the original `overview` and `genre` columns to keep the dataset clean.

## Step 3: Text Vectorization using CountVectorizer

Vectorize the text data to convert it into numerical format.

1. **Initialize CountVectorizer**: Set up `CountVectorizer` with parameters like `max_features` and `stop_words`.
2. **Fit and Transform Data**: Apply `CountVectorizer` to the `tags` column to create a matrix of token counts.

### Why CountVectorizer?

`CountVectorizer` converts a collection of text documents to a matrix of token counts. This is useful for transforming text data into a format that can be used for machine learning algorithms. It helps in:

- **Text Normalization**: Converts text to a standardized format.
- **Dimensionality Reduction**: Limits the number of features to a specified maximum (`max_features`).
- **Stop Words Removal**: Eliminates common words that do not contribute much to the meaning of the documents (`stop_words='english'`).

## Step 4: Calculate Cosine Similarity

Calculate cosine similarity between the text vectors.

1. **Compute Cosine Similarity**: Use the transformed data to calculate the cosine similarity matrix.

### Why Cosine Similarity?

Cosine similarity is useful in recommendation systems because it:

- **Ignores Magnitude**: Focuses on the orientation of the vectors rather than their magnitudes, making it suitable for text data where document length varies.
- **Efficient**: Computationally efficient for large datasets.

## Step 5: Define the Recommendation Function

Define a function to recommend movies based on the cosine similarity scores.

1. **Find Movie Index**: Identify the index of the selected movie in the dataset.
2. **Calculate Similarity Scores**: Use the similarity matrix to find movies similar to the selected movie.
3. **Retrieve Top Recommendations**: Extract the top 5 movies with the highest similarity scores.

# Step for the app.py
# Step 1: API Integration with TMDB

## API Registration
You registered with TMDB (The Movie Database) and obtained an API key. This key allows you to access TMDB's database programmatically.

## API Endpoint
You used the API endpoint for retrieving movie details by ID. The base URL for this endpoint is "https://api.themoviedb.org/3/movie/{}?api_key=YOUR_API_KEY". You replace `{}` with the movie ID, and `YOUR_API_KEY` with your actual TMDB API key.

# Step 2: Fetching Movie Poster Path

## Fetch Poster Path Function (`fetch_poster`)
- You defined a function `fetch_poster(movie_id)` that takes a movie ID as input and returns the full URL of the movie poster.
- Inside this function, you make a GET request to the TMDB API using the provided movie ID and your API key.
- You extract the poster path from the JSON response received from the API.
- Then you construct the full URL for the poster using the base URL for poster images from TMDB ("https://image.tmdb.org/t/p/w500") and append the poster path to it.
- Finally, the function returns the full URL of the poster.

# Step 3: Loading Data and Recommendation Logic

## Loading Data (`pickle.load(open("movies_list.pkl", 'rb'))`)
- You load movie data from a pickled file named "movies_list.pkl". This file likely contains a dataset of movies with attributes like title, ID, etc.

## Loading Similarity Matrix (`pickle.load(open("similarity.pkl", 'rb'))`)
- You load a similarity matrix from another pickled file named "similarity.pkl". This matrix probably contains similarity scores between movies based on some criteria.

## Recommendation Function (`recommend`)
- You define a recommendation function that takes a movie title as input and recommends similar movies.
- Inside this function, you find the index of the input movie in your dataset.
- You use the similarity matrix to find similar movies and extract their IDs.
- For each similar movie, you fetch the movie title and poster URL using the `fetch_poster` function.
- Finally, the function returns a list of recommended movie titles and their corresponding poster URLs.

# Step 4: User Interface (Streamlit)

## Streamlit Interface
- You create a Streamlit app with a header ("Movie Recommender System") and a dropdown select box (`st.selectbox`) to choose a movie.
- When the user clicks the "Show Recommend" button, the app calls the `recommend` function to get movie recommendations.
- It then displays the recommended movie titles and poster images in a grid layout using Streamlit's `st.columns` and `st.image`.
