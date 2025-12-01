# Movie Recommendation API

A lightweight API for discovering and recommending movies.
This repository contains the backend API, database models, and documentation for a movie recommendation service.

## Table of Contents

* [Demo / Live site](#demo--live-site)
* [Features](#features)
* [Architecture](#architecture)
* [Quickstart (local)](#quickstart-local)
* [Environment variables](#environment-variables)
* [Database & migrations](#database--migrations)
* [Run with Docker (recommended)](#run-with-docker-recommended)
* [API documentation (OpenAPI / Swagger)](#api-documentation-openapi--swagger)
* [Key endpoints](#key-endpoints)
* [Testing](#testing)
* [Deployment notes](#deployment-notes)
* [Design docs (ERD)](#design-docs-erd)
* [Slides / Presentation](#slides--presentation)
* [Contributing](#contributing)
* [License](#license)

---

## Demo / Live site

**Status:** The current live URL provided previously returned a `404` when checked; if you expect a running demo, check your host (Render/Heroku) logs and environment variables. If the site is running, paste the public URL here.

---

## Features

* Movie resources with metadata (title, genres, synopsis, release date)
* User ratings / reviews
* Watchlist / favorites
* Recommendation endpoint (basic heuristic or collaborative filtering)
* Pagination, filtering, and sorting on list endpoints
* Health and metrics endpoints

---

## Architecture (high level)

```
Client (web/mobile)
    ↕
API (this repo) — RESTful endpoints + OpenAPI
    ↕
Postgres (persistent storage)
    ↕
Redis (optional caching)
    ↕
Background workers (optional: Celery/RQ for heavy computation)
```

---

## Quickstart (local)

> Assumes Python 3.10+ (adjust for your project)

1. Clone the repo:

```bash
git clone https://github.com/SRYVarder/alx-project-nexus.git
cd alx-project-nexus/movie-reco-api
```

2. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

3. Create a `.env` file (see `.env.example`) and set required vars:

```
FLASK_ENV=development
DATABASE_URL=postgres://postgres:password@localhost:5432/movie_reco
SECRET_KEY=replace_with_secret
REDIS_URL=redis://localhost:6379/0
```

4. Initialize the database:

* If using Flask + Alembic:

```bash
flask db upgrade
```

* If Django:

```bash
python manage.py migrate
```

5. Seed dummy data (optional):

```bash
python manage.py loaddata fixtures/movies.json
```

6. Run locally:

```bash
# Flask example using gunicorn for production-like run
gunicorn -w 4 -b 127.0.0.1:8000 app:app

# Or for quick dev
flask run --host=0.0.0.0 --port=8000
```

---

## Environment variables

Provide a `.env.example` listing:

```
SECRET_KEY="django-specific-key"
TMDB_API_KEY=your exact tmdb api key"
POSTGRES_DB=moviedb
POSTGRES_USER=postgres
POSTGRES_PASSWORD="your unique password"
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
CELERY_BROKER_URL=amqp://guest:guest@rabbitmq:5672//
REDIS_URL=redis://localhost:6379/1
```

---

## Database & migrations

* Use migrations (Alembic for Flask or built-in Django migrations). Commit migrations to repo.
* Recommended indexes: `CREATE INDEX ON ratings(movie_id); CREATE INDEX ON ratings(user_id); CREATE INDEX ON movies(title);`
* Use UUIDs for public IDs if you prefer non-sequential IDs:

  * Example: `id = db.Column(UUID(as_uuid=True), primary_key=True, default=uuid.uuid4)`

---

## Run with Docker (recommended)

Example `Dockerfile` and `docker-compose.yml` should be provided. Quick commands:

```bash
docker build -t movie-reco-api .
docker run -p 8000:8000 \
  -e DATABASE_URL=postgres://... \
  -e SECRET_KEY=... \
  movie-reco-api
```

Or using docker-compose:

```bash
docker-compose up --build
```

---

## API documentation (OpenAPI / Swagger)

* Add an OpenAPI spec at `openapi.yaml` or generate automatically from code.
* Add a `/docs` route to host Swagger UI or ReDoc for interactive exploration.

---

## Key endpoints



### Authentication

```
POST /admin/
POST /api/users/register/
POST /api/users/login/
DELETE /api/users/delete/
POST /api/token/
POST /api/token/refresh/
```

### Movies

```
GET /movies/favorites/
POST /movies/favorites/
DELETE /movies/favorites/{id}
GET /movies/search/?query=?
GET /movies/trending/
```

### Recommendation

```
GET /movies/users/{user_id}/recommendations/?type=cf&limit=10
GET /api/movies/users/1/recommendations/?type=popular
GET /movies/users/{user_id}/recommendations/?type=content&limit=5

```


## Testing
run 
```
pytest -v

```

* Add GitHub Actions workflow to run tests on push/PR.

---

## Deployment notes

* For Render: ensure `Start Command` is correct (e.g., `gunicorn app:app`), and environment variables are set. If the live URL returns 404, check the build logs and health port.
---

## Design docs (ERD)

* I recommend creating an ERD (draw.io or Lucidchart), exporting it as PNG, and 

---

## Slides / Presentation

Create a Google Slides file with:

1. Title slide
2. Problem statement & objective
3. Architecture diagram
4. ERD slide
5. Key endpoints examples (cURL)
6. Testing and CI
7. Deployment summary
8. Future work
9. 






Method	Endpoint	Authentication	Description
AUTH /USER			
POST	POST /admin/	Yes	Admin user for the API
POST	POST /api/users/register/	No	Create User
POST	POST /api/users/login/	Yes	Login existing User
DELETE	DELETE /api/users/delete/	Yes	Delete existing User account
POST	POST /api/token/	No	Get JWT access token
POST	POST /api/token/refresh/	Yes	Refresh Expired or invalid Token
MOVIES			
GET	GET /api/movies/favorites/	Yes	Search for favorite
POST	POST /api/movies/favorites/	Yes	Add to favorite
DELETE	DELETE /api /movies/favorites/{id}	Yes	Delete Favorites
GET	GET /api/movies/search/?query=?	No	Search movies
GET	GET /api/movies/trending/	No	Check trending movies
RECOMMENDATION			
GET	GET /api/movies/users/{user_id}/recommendations/?type=cf&limit=10	Yes	Collaborative filtering based recommendations
GET	GET /api/api/movies/users/1/recommendations/?type=popular	Yes	Popularity based recommendations
GET	GET /api/movies/users/{user_id}/recommendations/?type=content&limit=5	Yes	Content /genre based recommendations
DOCUMENTATION			
GET	GET /api/docs/	No	Swagger UI
GET	GET /api/redoc/	No	Redoc/ Open.ai
			
<img width="1094" height="442" alt="image" src="https://github.com/user-attachments/assets/41154a76-270e-4a64-a9cb-f6b0ab3446c8" />

























































































