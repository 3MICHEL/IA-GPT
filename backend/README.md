# Backend FastAPI

## Lancer en local (sans Docker)
uv venv .venv && .\.venv\Scripts\activate
uv pip install .
$env:OLLAMA_SERVICE_NAME="localhost:11435"
uv run uvicorn main:app --host 0.0.0.0 --port 8000

## Lancer en Docker
docker build -f Dockerfile.advancedv2 -t backend:0.0.5 .
docker run --network autodep-net -p 8000:8000 `
  -e OLLAMA_SERVICE_NAME=ollama:11434 `
  --name backend --rm -it backend:0.0.5

## Endpoints
- GET /healthcheck
- GET /docs
- POST /v1/models/{model}/temperature/{temperature}/ (body = liste de messages r?le/content)
