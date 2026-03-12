# AMD Finance Newsletter Generator

Automatically generates a weekly AMD finance newsletter PDF using the AMD LLM Gateway, covering:

- **AMD Financials & Earnings** — revenue, margins, segments, guidance
- **Global Gaming Market Trends** — Ryzen demand, Steam data, regional patterns  
- **Competitor Analysis** — Intel vs AMD (CPU), Nvidia vs AMD (GPU/AI)

Each run produces a professionally formatted PDF saved to the `newsletters/` folder and pushed to this repo.

---

## Quick Start

### 1. Get an API Key
Go to [https://llm.amd.com/](https://llm.amd.com/) and request an AMD LLM Gateway API key.

> **Note:** You must be on the AMD internal network or VPN to use this key.

---

### 2. Choose: Push to the shared repo OR your own fork

**Option A — Push to the shared team repo (simplest)**

Clone directly:
```bash
git clone https://github.com/LucasbAMD/AI-Newsletter.git
cd AI-Newsletter
```
Your newsletter PDFs will appear in the shared `newsletters/` folder visible to the whole team.

---

**Option B — Push to your own fork (recommended for personal demos)**

1. Go to [https://github.com/LucasbAMD/AI-Newsletter](https://github.com/LucasbAMD/AI-Newsletter)
2. Click **Fork** in the top-right corner — this creates `https://github.com/YOUR_USERNAME/AI-Newsletter` under your own GitHub account
3. Clone your fork:
```bash
git clone https://github.com/YOUR_USERNAME/AI-Newsletter.git
cd AI-Newsletter
```
When you run the script it will push newsletters to **your own fork**, fully independent from everyone else.

---

### 3. Install dependencies
```bash
pip install openai==1.101.0 gitpython reportlab
```

### 4. Edit your API key and repo path
Open `generate_newsletter.py` and update the CONFIG block at the top of the file:

```python
# ---------------------------------------------------------------------------
# CONFIG — edit these values before running
# ---------------------------------------------------------------------------
API_KEY   = "YOUR_AMD_GATEWAY_KEY_HERE"      # Your AMD LLM Gateway key
REPO_PATH = r"C:\Users\YOUR_USERNAME\AI-Newsletter"  # Where you cloned the repo
GIT_REMOTE = "origin"   # Leave as "origin" — points to whichever repo you cloned
GIT_BRANCH = "main"
```

> **Important:** Never commit your API key to the repo. Keep it only in the local CONFIG block on your machine.

### 5. Run it
```bash
python generate_newsletter.py
```

The script will:
1. Call the AMD LLM Gateway to generate each newsletter section
2. Build a styled PDF with AMD branding
3. Save it to `newsletters/amd_finance_newsletter_YYYY-MM-DD.pdf`
4. Commit and push it to your repo (shared or fork) automatically

---

## Output

Each newsletter PDF includes:
- AMD red branded masthead with issue date
- Editor's Note
- AMD Financials & Earnings analysis
- Global Gaming Market Trends
- Competitor Analysis (Intel & Nvidia)
- Key Takeaways summary box
- Auto-generated disclaimer footer

PDFs are saved to the `newsletters/` folder with the date in the filename so every run is preserved.

---

## Scheduling (optional)

**Windows Task Scheduler:**
- Program: `python`
- Arguments: `C:\Users\YOUR_USERNAME\AI-Newsletter\generate_newsletter.py`
- Trigger: Weekly, pick your preferred day and time

**Linux/macOS cron (every Monday at 07:00):**
```bash
0 7 * * 1 /usr/bin/python3 /path/to/AI-Newsletter/generate_newsletter.py
```

---

## Requirements

- Python 3.12+
- AMD internal network or VPN access
- AMD LLM Gateway API key from [https://llm.amd.com/](https://llm.amd.com/)

```
openai==1.101.0
gitpython
reportlab
```

---

## Notes

- The AMD LLM Gateway (`llm-api.amd.com`) is only accessible from inside AMD's network — the script must be run locally, not via GitHub Actions
- Your API key should never be committed to the repo — keep it only in the CONFIG block on your local machine
- Each person on the team uses their own API key
