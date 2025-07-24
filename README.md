# 📚 Bookstore API

A containerized FastAPI service to manage a bookstore.

---

## ⚙️ Environment Configuration

| Variable          | Default                                  | Description                                                      |
|-------------------|------------------------------------------|------------------------------------------------------------------|
| `DATABASE_URL`    | `sqlite:///./books.db`                   | SQLAlchemy database connection string.                           |
| `LOG_LEVEL`       | `INFO`                                   | Root logger level (e.g. DEBUG, INFO, WARNING).                   |
| `LOG_FORMAT`      | `%(levelname)s:%(name)s:%(message)s`     | Python `logging` format string.                                  |
| `PAGE_SIZE`       | `10`                                     | Number of items per page on the `/books/` endpoint.              |
| `APP_ENV`         | `dev`                                    | App environment label (e.g. dev / staging / prod).               |
| `HOST`            | `0.0.0.0`                                | Uvicorn host binding.                                            |
| `PORT`            | `8080`                                   | Uvicorn port.                                                    |
| `RELOAD`          | `False`                                  | Whether Uvicorn runs in reload mode (`True`/`False`).            |
| `ALLOWED_ORIGINS` | `*`                                      | Comma-separated list for CORS allowed origins (`*` = all).       |
| `DB_POOL_SIZE`    | `5`                                      | SQLAlchemy connection-pool size.                                 |
| `DB_MAX_OVERFLOW` | `10`                                     | SQLAlchemy max overflow connections beyond the pool size.        |

---

## 🐳 Docker

### Build

```bash
docker build -t docker-pipeline-demo .
```

### Run

```bash
docker run -p 8080:8080 docker-pipeline-demo
```

The service will be running on [http://localhost:8080/books](http://localhost:8080/books)

---

## 🚀 CI/CD with GitHub Actions

Every push to `main` will:

- Build the Docker image
- Push it to GitHub Container Registry (GHCR)

Image: `ghcr.io/nicosmuts/docker-pipeline-demo:latest`

### Required GitHub Secrets

| Secret Name   | Description                        |
|---------------|------------------------------------|
| `GHCR_TOKEN`  | GitHub token with packages access  |

---
