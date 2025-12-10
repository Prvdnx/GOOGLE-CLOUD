
# Conversational Analytics (Gemini Data Analytics)

This sample demonstrates streaming interactions with the Gemini Data Analytics (formerly Conversational Analytics) services to:
- Resolve schemas and data sources
- Generate SQL
- Retrieve tabular data
- Produce Altair charts and preview them locally

Reference codelab: [Introduction to the Conversational Analytics API](https://codelabs.developers.google.com/ca-api-bigquery#0)


## Prerequisites

- Python 3.12+
- Google Cloud project with billing enabled
- gcloud CLI installed and initialized
  - Install: https://cloud.google.com/sdk/docs/install
  - Initialize: `gcloud init`
- Local auth using Application Default Credentials (ADC)
  - `gcloud auth application-default login`
- Enable required APIs in your project (at minimum):
  - Gemini Data Analytics API: `geminidataanalytics.googleapis.com`
  - BigQuery API (if your agent queries BigQuery): `bigquery.googleapis.com`


## Setup

1) Clone and enter the project
```
cd "ca-42-workshop(Conversational Analytics)"
```

2) Create a Python environment and install dependencies

Option A: uv (recommended)
```
uv python install 3.12
uv sync
```

Option B: venv + pip
```
python3.12 -m venv .venv
. .venv/bin/activate
pip install --upgrade pip
pip install -e .
```

3) Authentication
```
gcloud auth application-default login
```

4) Project ID environment variable
- If you are using Cloud Shell, `DEVSHELL_PROJECT_ID` is set automatically.
- If you are running locally, export your project ID:
```
export DEVSHELL_PROJECT_ID="YOUR_PROJECT_ID"
```


## Run

```
# With uv
uv run python main.py

# Or with venv
python main.py
```

What happens:
- The script sends a question to Gemini Data Analytics using a predefined agent.
- It streams responses that may include resolved schemas, generated SQL, and results.
- If a chart is generated, an `index.html` is written and a simple HTTP server starts on port 8080 for preview.
  - Cloud Shell: use Web Preview on port 8080.
  - Local: open http://localhost:8080


## Configuration

Defaults (see `main.py`):
- `location = "global"`
- `data_agent_id = "google_trends_analytics_agent"`
- `conversation_id = "my_first_conversation"` (set in the `__main__` block)
- The question is set in the `ask` variable.

To change behavior:
- Edit the `ask` variable or the call to `stream_chat_response(ask)`.
- Adjust `data_agent_id` if you want to use a different agent in your project.
- Set `DEVSHELL_PROJECT_ID` to target a different Google Cloud project.


## Troubleshooting

- API not enabled: `gcloud services enable geminidataanalytics.googleapis.com` (and `bigquery.googleapis.com` if needed)
- Permission errors: ensure your account has necessary roles to access Gemini Data Analytics and BigQuery.
- Credentials not found: run `gcloud auth application-default login` or set `GOOGLE_APPLICATION_CREDENTIALS` to a service account key JSON.
- Port 8080 in use: edit `preview_in_browser(port=...)` in `main.py` to another free port.


## License

Sample code provided for educational purposes. Review and adapt to your needs before production use.
