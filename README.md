# Multi-Agent Enterprise Knowledge Assistant (MVP)

A document-grounded knowledge assistant using **LangGraph**, **Sentence Transformers**, **FAISS**, and **FastAPI**.
Three explicit graph stages: retrieval, reasoning, and verification. Supports `.txt` and `.pdf` documents.
An OpenRouter key enables LLM synthesis; without one, it returns an extractive source excerpt.

> Scope: educational MVP. Retrieval similarity is only a heuristic; it **does not prove factual grounding**.
> No claim of petabyte scale, production deployment, or hallucination elimination.

## Setup

Python 3.11 recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

Optionally copy `.env.example` to `.env` and set `OPENROUTER_API_KEY`, then export it in your shell.
The app reads environment variables; it does not automatically load `.env`.

```bash
uvicorn app.main:app --reload
```

First request downloads the embedding model. Visit http://127.0.0.1:8000/docs and POST `/ask`:

```json
{"question":"How can I reset my password?"}
```

To evaluate retrieval: `python -m app.evaluate`. To test: `pytest -q`.
Docker: `docker build -t knowledge-agent .` then `docker run -p 8000:8000 knowledge-agent`.

## Architecture

Documents → chunking → Sentence Transformer embeddings → FAISS index → LangGraph retrieval agent → reasoning agent → verification heuristic → FastAPI response.

## Next improvements

Add chunk-level labeled retrieval benchmarks, reranking, evidence-to-claim verification,
authentication, persistent indexes, rate limiting, and load testing.

## Responsible resume description

"Built a LangGraph-orchestrated document QA prototype using Sentence Transformers, FAISS, and FastAPI with source references and retrieval-confidence checks." Use only after running it yourself.
