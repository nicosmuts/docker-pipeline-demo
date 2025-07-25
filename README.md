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
| `APP_ENV`         | `dev`                                    | App environment label (e.g. dev / staging /prod).                |
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

Then go to [http://localhost:8080/books](http://localhost:8080/books)

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

## ☸️ Helm Chart Overview

This chart supports multiple environments using different `values-{env}.yaml` files.

### Example Commands

```bash
# Deploy to dev
helm upgrade --install books-api-dev ./charts/books-api -f charts/books-api/values-dev.yaml --namespace dev --create-namespace

# Deploy to staging
helm upgrade --install books-api-staging ./charts/books-api -f charts/books-api/values-staging.yaml --namespace staging --create-namespace

# Deploy to production
helm upgrade --install books-api-prod ./charts/books-api -f charts/books-api/values-prod.yaml --namespace prod --create-namespace
```

---

## 🧪 Helm Testing

### Lint the chart

```bash
helm lint ./charts/books-api
```

### Render templates

```bash
helm template books-api-dev ./charts/books-api -f charts/books-api/values-dev.yaml
```

---

## 🐳 KIND: Local Kubernetes Testing

### Prerequisites

- Docker Desktop with WSL 2 backend
- KIND installed
- Helm installed

### Create KIND cluster

```bash
kind create cluster --name books-api
```

### Deploy Helm chart to KIND

```bash
helm upgrade --install books-api-dev ./charts/books-api -f charts/books-api/values-dev.yaml --namespace dev --create-namespace
```

### Port-forward to access the app

```bash
kubectl port-forward svc/books-api-dev-books-api 8080:80 -n dev
```

Then go to [http://localhost:8080/books](http://localhost:8080/books)

---

## 🛠 Improvements (to-do)

- External database (RDS / MySQL chart on K8S)
- Persistent storage and/or external storage (NFS / S3)
- Prometheus monitoring
- Grafana dashboard
- Alerting
- Multi-stage deployment pipeline
    - dev -> staging -> prod
    - Security testing (SonarQube)
    - QA testing
