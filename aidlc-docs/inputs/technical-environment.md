# Technical environment

AI Job Application Agent · November 24, 2026 · Proposed for whole-team review

A student runs one local web app to confirm claims extracted from several resumes, review recent job postings, and save opportunities. This document proposes the implementation environment for the six MVP features in the [reviewed vision](vision.md). The team uses AI-DLC v1.0.1.

## Stack and local deployment

| Area | Choice | Purpose |
|---|---|---|
| Language and packages | Python 3.12, uv, `pyproject.toml` and `uv.lock` | Record exact dependency versions during Construction so teammates can reproduce the demo. |
| Web app | FastAPI, Uvicorn with one worker, Jinja2 templates | Serve upload, profile correction and shortlist screens and JSON endpoints from one process. |
| Validation and import | Pydantic 2, python-multipart, pypdf | Validate requests and model output. Accept multiple text-bearing PDFs, UTF-8 text files, or pasted text. Offer paste when a scan has no extractable text. |
| Storage | SQLite via Python's sqlite3 | Preserve confirmed claims, source evidence, job status and last successful scan across restarts. |
| HTTP and LLM | HTTPX, official OpenAI Python SDK with Responses API | Retrieve listings and generate grounded explanations using the team's planned hosted model, `gpt-6.1-terra`. |
| Tests and style | pytest, HTTPX mock transports, Ruff | Run repeatable tests without credentials and check Python formatting. |

Cloud hosting provider: none. The browser connects to a server on the student's laptop. A hosted LLM processes selected text. macOS and Linux are the initial targets. Codespaces can run the same app using private port forwarding. The planned commands from the repository root after implementation are:

```bash
uv sync --locked
uv run --locked uvicorn app.main:app --host 127.0.0.1 --port 8000 --workers 1
uv run --locked pytest
```

Open `http://127.0.0.1:8000`. Keep the SQLite file and uploaded resumes in an ignored `data/` directory. Commit synthetic fixtures so a teammate can review the same examples offline.

## Retrieval, matching and delivery

- The agent may search the Adzuna US and USAJOBS APIs and read a stored listing. Each adapter returns the source ID, title, employer, location, text actually received, link, retrieval time and publication date when supplied. Label and link Adzuna results and use only the available snippet. Accept LinkedIn and other pasted job text with an optional URL. For text without a URL, link to the locally stored source.
- Profile extraction produces claims with source references. Matching uses the user's confirmed version. Validate every explanation against a confirmed claim ID and a phrase in the listing. Missing facts stay unknown. For resume suggestions, accept an ordered subset of existing confirmed bullet IDs, render their original text, and save the arrangement only after user acceptance.
- Application code puts verified postings from the last 72 hours first. Merge listings that share a source and requisition ID or normalized employer, title, location and URL. Preserve saved, hidden, applied and rejected statuses when refreshing.
- Run a scan every four hours while the server is running, or on **Scan now**. Both triggers share a lock. On launch, show saved results and run one catch-up if the last success was more than four hours ago. Stopping the server stops scans and email. Deliver results in-app by default. Send via TLS SMTP only to the user's configured address after opt-in.
- On API throttling, respect the provider's retry interval. Bound source requests to 15 seconds and model calls to 45 seconds, with at most one transient retry per call. Preserve the last successful results on retrieval failure. Display source facts with an explanation-unavailable message on model failure. Label fixture replay explicitly. The vision's alternative provider, Anthropic with `claude-haiku-5-5`, requires deliberate configuration and validation before sending data.

## Prohibited libraries

| Excluded use | Reason | Alternative |
|---|---|---|
| LinkedIn scraping or session automation libraries | The agreed LinkedIn input is text supplied by the user. | Paste the job description and optionally its URL. |
| CAPTCHA-solving or access-control bypass libraries | Live retrieval is limited to the supported APIs under their access terms. | Use the official API, a user-provided description or a synthetic demo fixture. |

## Security basics

Keep model, Adzuna, USAJOBS and SMTP credentials in environment variables. Commit only example variable names. Exclude raw resumes, the database and local configuration from Git. Log source names, timings and status codes, and redact credentials, query strings and personal text. Send the provider only the text needed for the current task. Support deletion of the local profile, uploads and associated recommendations.

Use parameterized SQL, escaped HTML templates, size-limited uploads and generated storage names. Treat resumes, listings and model output as untrusted input. Restrict retrieval to fixed API hosts and validate tool arguments in Python. Saving a shortlist or bullet arrangement requires a user action. Protect browser writes against cross-site requests.

## Endpoint, function and test examples

The shortlist displays a freshness label computed from the source's posting timestamp. The following small route shows how the API and tests can share that rule. Use UTC-aware timestamps. When only a calendar date is available and its precision cannot establish freshness, pass no exact timestamp.

`app/freshness.py`

```python
from datetime import datetime, timedelta

def classify_posting(posted_at: datetime | None, now: datetime) -> str:
    if now.utcoffset() is None:
        raise ValueError("Expected a timezone-aware clock")
    if posted_at is None or posted_at.utcoffset() is None:
        return "unknown"
    age = now - posted_at
    if age < timedelta(0):
        return "unknown"
    return "fresh" if age <= timedelta(hours=72) else "older"
```

`app/main.py` — `POST /api/listings/freshness` accepts a nullable timestamp. Sending `{"posted_at":null}` returns HTTP 200 and `{"freshness":"unknown"}`. A malformed timestamp returns HTTP 422.

```python
from datetime import datetime, timezone

from fastapi import FastAPI
from pydantic import AwareDatetime, BaseModel

from app.freshness import classify_posting

app = FastAPI()

class PostingTime(BaseModel):
    posted_at: AwareDatetime | None

@app.post("/api/listings/freshness")
def listing_freshness(body: PostingTime):
    return {"freshness": classify_posting(body.posted_at, datetime.now(timezone.utc))}
```

`tests/test_freshness.py`

```python
from datetime import datetime, timedelta, timezone

from app.freshness import classify_posting

def test_freshness_uses_posting_time_and_includes_72_hour_boundary():
    now = datetime(2026, 11, 24, 18, tzinfo=timezone.utc)
    assert classify_posting(None, now) == "unknown"
    assert classify_posting(now - timedelta(hours=72), now) == "fresh"
    assert classify_posting(now - timedelta(hours=72, seconds=1), now) == "older"
    assert classify_posting(now + timedelta(minutes=1), now) == "unknown"
```

## Evaluation during Construction

Run fixture tests with two synthetic resumes, a corrected claim, a pasted job, fresh/older/undated listings and a repeated saved listing. Verify the corrected claim is used, each explanation cites both sources, and the saved role does not reappear as new. Reject fabricated bullet IDs and verify that rejecting a suggestion leaves the profile unchanged. Use a temporary SQLite file, a fixed clock and simulated HTTP/model/SMTP responses to check restarts, catch-up scans and failure handling. Test live provider access separately on a team laptop and record the results in the shared workflow.
