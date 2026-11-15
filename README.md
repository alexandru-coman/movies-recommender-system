# CineMatch

**NLP-powered movie discovery and recommendation system.**

CineMatch is a full-stack web application that combines semantic search, personalised recommendations, and a responsive cinema-themed interface. It uses Word2Vec and SBERT embeddings to understand movie descriptions and return relevant results.

## Highlights

- Browse a catalogue of 500 movies
- Build a personal watchlist in the browser
- Get top-20 recommendations from watchlist preferences
- Search using natural-language descriptions in English or Romanian
- Compare Word2Vec and SBERT search results
- Load posters and movie metadata from TMDB

## Tech stack

- **Backend:** Python, Flask, Flask-CORS
- **NLP:** Gensim Word2Vec, Sentence-Transformers (SBERT)
- **Data:** HuggingFace Datasets, MovieLens 32M enriched dataset
- **Frontend:** HTML5, CSS3, vanilla JavaScript
- **Metadata:** TMDB API
- **Numerical processing:** NumPy

## Project structure

```text
app.py             Flask backend and recommendation API
index.html         Frontend shell
script.js          Search, recommendations, watchlist, and UI logic
stil.css           Dark cinema theme
requirements.txt   Python dependencies
```

## Getting started

### Requirements

- Python 3.9+
- A TMDB API key

### Run the application

```bash
pip install -r requirements.txt
python app.py
```

In a second terminal, serve the frontend:

```bash
python -m http.server 8080
```

Open <http://localhost:8080> in your browser.

The first backend startup may take a few minutes while the dataset is downloaded and the Word2Vec model is trained. SBERT loads in the background when enabled.

## How recommendations work

1. The frontend sends the user's watchlist to the Flask API.
2. Movie descriptions are represented as vectors.
3. A user profile is calculated from the selected movies.
4. Cosine similarity ranks the closest unseen movies.
5. The top results are returned to the frontend.

Natural-language search first applies metadata filters, then ranks the remaining movies semantically. SBERT provides stronger multilingual understanding, while Word2Vec starts faster and is easier to inspect.

## API

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `GET` | `/api/filme` | Load the movie catalogue |
| `POST` | `/api/recomandari` | Generate recommendations |
| `POST` | `/api/cauta` | Search by natural-language query |
| `GET` | `/api/film/<id>` | Get movie details |
| `GET` | `/api/genuri` | List available genres |
| `GET` | `/api/postere` | Get poster mappings |
| `GET` | `/api/status` | Check model readiness |

## Data sources

- [MovieLens 32M Movies Enriched](https://huggingface.co/datasets/krishnakamath/movielens-32m-movies-enriched-with-SIDs)
- [The Movie Database (TMDB)](https://www.themoviedb.org/)

## Notes

- The demo catalogue is limited to 500 movies for practical startup times.
- The Word2Vec model is trained on English movie text; SBERT is better suited to Romanian queries.
- Watchlists are stored locally in the browser and are not synchronised between devices.
- TMDB posters and metadata require an internet connection and a valid API key.
