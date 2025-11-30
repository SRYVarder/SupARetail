# 🎬 Movie Recommendation API (DRF + JWT + PostgreSQL)

A high-performance, scalable REST API for movie search, trending analysis,
and personalized recommendations.

---

## 🚀 Features

- JWT Authentication (Login, Register, Refresh)
- Search Movies (full text & fuzzy matching)
- Trending Movies (Redis cached)
- Add/Delete Favorites
- Structured API responses
- Swagger Documentation
- PostgreSQL with optimized indexing
- Render Deployment

---

## 📁 Project Structure

movie-reco-api/
│── movies/
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│── users/
│   ├── views.py
│   ├── authentication.py
│── utils/
│   ├── response.py
│── settings.py
│── urls.py

---

## 🗄️ Database Schema (ERD)

### Entities:
- **User**
- **Movie**
- **Favorite**
- **Genre** (optional upgrade)

### Relationships:
- User → Favorite (1:M)
- Movie → Favorite (1:M)
- Movie → Genre (M:M)

ERD Link: *Add Google Doc Image Link Here*

---

## 🔗 API Endpoints

### 🎥 Movies
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/movies/search/` | Search movies |
| GET | `/movies/trending/` | Trending movies |
| POST | `/movies/favorites/` | Add favorite |
| DELETE | `/movies/favorites/{id}/` | Remove favorite |

### 👤 Users
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/users/register/` | Register |
| POST | `/users/login/` | Login |
| DELETE | `/users/delete/` | Delete account |

---

## 🧪 Testing

Run test suite:
pytest -v


---

## 🚀 Deployment

1. Push to GitHub  
2. Auto build on Render  
3. Set environment variables  
4. Run migrations:




