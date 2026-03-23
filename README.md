# Movie Recommender System

A full-stack movie recommender with:
- **FastAPI backend** for TMDB search, movie details, and recommendations.
- **Streamlit frontend** for search, browsing, and detail views with posters.
- **Local TF-IDF model** for content-based recommendations backed by pickled artifacts.

The app blends TMDB metadata with TF-IDF similarity over a local dataset to give both **similar-title** and **genre-based** suggestions.

---

## Features
- TMDB keyword search with suggestions and poster grid
- Movie detail page with overview, genres, and backdrop
- TF-IDF similarity recommendations (local dataset)
- Genre-based recommendations via TMDB discover
- Clean Streamlit UI with home feed (trending / popular / top rated / now playing / upcoming)

---

## Project Structure (Key Files)
- `main.py` — FastAPI backend
- `app.py` — Streamlit frontend
- `df.pkl`, `indices.pkl`, `tfidf.pkl`, `tfidf_matrix.pkl` — Local model artifacts
- `movies_metadata.csv` — Source dataset (optional reference)

---

## Requirements
Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Environment Setup
Create a `.env` file (or update the existing one) with your TMDB API key:

```
TMDB_API_KEY=your_tmdb_api_key_here
```

You can get a key from TMDB. Keep this file private and **do not commit it**.

---

## Running Locally
### 1) Start the FastAPI backend

```bash
uvicorn main:app --reload
```

The API will run at `http://127.0.0.1:8000`.

### 2) Start the Streamlit frontend

```bash
streamlit run app.py
```

Open the Streamlit URL shown in the terminal (usually `http://localhost:8501`).

---

## API Endpoints (Backend)
- `GET /health` — Health check
- `GET /home?category=popular&limit=24` — TMDB home feed
- `GET /tmdb/search?query=avatar` — Raw TMDB keyword search
- `GET /movie/id/{tmdb_id}` — Movie details
- `GET /recommend/genre?tmdb_id=603&limit=18` — Genre-based recommendations
- `GET /recommend/tfidf?title=The%20Matrix&top_n=10` — TF-IDF-only recs
- `GET /movie/search?query=The%20Matrix` — Details + TF-IDF + Genre bundle

---

## Notes
- The backend loads TF-IDF artifacts on startup. Ensure the following files exist:
  - `df.pkl`
  - `indices.pkl`
  - `tfidf.pkl`
  - `tfidf_matrix.pkl`
- If any of these are missing, the backend will fail at startup.

---

## Troubleshooting
- **TMDB errors or empty data**: confirm your `TMDB_API_KEY` is valid.
- **Streamlit cannot fetch data**: ensure the FastAPI server is running and reachable.

---

## License
This project is for learning/demo use. Add a license if you plan to distribute it.

