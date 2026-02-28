# DVC with Google Cloud Storage
### IE7300 - MLOps | Northeastern University

## Architecture

```
┌─────────────────────────────────────────┐
│              Git (GitHub)               │
│  - Source code                          │
│  - .dvc pointer files  ◄── tracks data  │
└──────────────────┬──────────────────────┘
                   │ dvc push / dvc pull
┌──────────────────▼──────────────────────┐
│        Google Cloud Storage (GCS)       │
│  - Raw datasets (CSV)                   │
│  - Content-addressed (MD5 hashed)       │
│  - Versioned blobs under /files/md5/    │
└─────────────────────────────────────────┘
```

## Project Structure

```
labs/
├── data/
│   └── Student_data.csv           # DVC-tracked (gitignored)
├── .dvc/
│   └── config                     # Remote storage config
├── data/Student_data.csv.dvc      # DVC pointer file (committed to Git)
├── requirements.txt
├── .gitignore
└── README.md
```

## Setup & Reproduction

```bash
# 1. Clone
git clone https://github.com/Vignesh4110/Labs_dvc.git
cd Labs_dvc

# 2. Virtual environment
python3.10 -m venv .venv
source .venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure GCP credentials
dvc remote modify myremote credentialpath /absolute/path/to/keys.json

# 5. Pull data from GCS
dvc pull
```

## Key Commands

| Command | Description |
|---|---|
| `dvc init` | Initialize DVC in a Git repo |
| `dvc add data/file.csv` | Track a data file with DVC |
| `dvc remote add -d myremote gs://bucket/` | Set GCS as default remote |
| `dvc push` | Upload tracked data to GCS |
| `dvc pull` | Download tracked data from GCS |
| `dvc status` | Check if local data matches remote |

## Reproducing a Specific Data Version

```bash
git checkout <commit-hash>
dvc pull
```

## Tech Stack
`DVC` · `Google Cloud Storage` · `Git` · `Python 3.10`

---
*IE7300 MLOps · Northeastern University · Boston, MA*