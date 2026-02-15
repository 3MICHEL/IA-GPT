# Autodep Project ? JuniaGPT

## Pr?requis
- Docker Desktop (Linux engine) + Compose V2
- 6?8 Go de RAM conseill?s, au moins 5 Go libres pour `phi3:mini`
- Ports libres : 11435 (Ollama), 8000 (backend), 8501 (frontend)

## D?marrage rapide (conteneurs)
docker network create autodep-net

docker run -p 11435:11434 `
  -v "${PWD}/ollama/ollama:/root/.ollama" `
  -v "${PWD}/ollama/entrypoint.sh:/entrypoint.sh" `
  --entrypoint /usr/bin/bash `
  --network autodep-net `
  --name ollama --rm -it ollama/ollama:latest /entrypoint.sh

docker run --network autodep-net -p 8000:8000 `
  -e OLLAMA_SERVICE_NAME=ollama:11434 `
  --name backend --rm -it backend:0.0.5

docker run --network autodep-net -p 8501:8501 `
  -e BACKEND_SERVICE_NAME=backend:8000 `
  --name frontend --rm -it frontend:0.0.7

Frontend : http://localhost:8501  
Backend  : http://localhost:8000 (docs /docs)  
Ollama   : port h?te 11435

## Mod?le
- Par d?faut : phi3:mini (l?ger).
- Pour changer : `ollama pull <modele>` puis ajuster `frontend/main.py` (champ model) et rebuilder.

## Tests (optionnel)
cd backend && container-structure-test test --image backend:0.0.5 --config tests/cst-advancedv2.yaml
cd frontend && container-structure-test test --image frontend:0.0.7 --config tests/cst-advancedv2.yaml
