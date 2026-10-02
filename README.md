# DebugDesk AI — MVP

DebugDesk AI helps developers investigate errors by combining a bug report or stack trace with relevant source files. It retrieves likely relevant files using TF-IDF and produces a structured diagnosis, debugging checklist, and regression-test plan.

## Features
- Paste stack traces or describe unexpected behavior.
- Upload text source files or a ZIP of a project.
- Lightweight TF-IDF retrieval over uploaded code context.
- Model-powered analysis through an OpenAI-compatible API when configured.
- Demo mode works without an API key and produces a heuristic debugging report.
- Download the report as Markdown.
- Uploaded code is treated as text and is never executed.

## Run locally

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
streamlit run app.py
```

Open the local URL printed by Streamlit (usually http://localhost:8501). The app works in demo mode without secrets.

## Enable model-powered analysis

Set these environment variables before launching the app:

```bash
LLM_API_KEY=your_api_key
LLM_BASE_URL=https://api.groq.com/openai/v1
LLM_MODEL=qwen/qwen3-32b
```

The app uses an OpenAI-compatible `/chat/completions` endpoint. Check your provider's current model catalogue and use a model available to your account. Never commit API keys to GitHub.

## Deploy on Streamlit Community Cloud
1. Create a GitHub repository and upload `app.py`, `requirements.txt`, and this README.
2. In Streamlit Community Cloud, create an app from the repository and select `app.py`.
3. The app can be deployed without a key in demo mode.
4. For model-powered analysis, add `LLM_API_KEY`, `LLM_BASE_URL`, and `LLM_MODEL` in the app's Secrets settings.
5. Test with a harmless sample stack trace and dummy project files before sharing the URL.

## Suggested demo credentials
This MVP has no user login, so no username or password is required. If the form insists on dummy credentials, enter: `Not required — public demo, no authentication`.

## Current MVP limitations
- Retrieval is lexical TF-IDF, not semantic embeddings.
- It does not clone private repositories or execute tests.
- Demo mode is heuristic and does not use an LLM.
- Treat uploaded source code and generated fixes as sensitive; review provider privacy terms before sending code to a hosted model.
- This is a prototype, not a production debugging or security product.
