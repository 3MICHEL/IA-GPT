# Frontend Streamlit

## Lancer en local
uv venv .venv && .\.venv\Scripts\activate
uv pip install .
$env:BACKEND_SERVICE_NAME="localhost:8000"
uv run streamlit run main.py --server.address 0.0.0.0 --server.port 8501

## Lancer en Docker
docker build -f Dockerfile.advancedv2 -t frontend:0.0.7 .
docker run --network autodep-net -p 8501:8501 `
  -e BACKEND_SERVICE_NAME=backend:8000 `
  --name frontend --rm -it frontend:0.0.7

## Param?tres
- S?lecteur de temp?rature : Accurate (0), Balanced (0.7), Creative (1.0)
- Mod?le par d?faut : phi3:mini
