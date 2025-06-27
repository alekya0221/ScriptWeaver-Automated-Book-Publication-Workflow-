# ScriptWeaver-Automated-Book-Publication-Workflow
AI-powered book publication pipeline with scraping, rewriting, human-in-the-loop editing, versioning, and intelligent retrieval.



**Scriptweaver** is a human-in-the-loop system that transforms raw chapter content into professionally refined narratives — with full versioning, provenance tracking, and reproducibility built in. Designed for authors, editors, and AI practitioners, it combines intelligent automation with creative control.

---

## Features

- **Web scraping + screenshot capture** for reproducibility and transparency  
- **Multi-agent AI drafting** (language polishing + review agents)  
- **Optional human edits** with audit trail and version lineage  
- **Version control** using `chapterXX_vY.txt` and `version_manifest.csv`  
- **Visual evidence** stored in `assets/` (PNG snapshot per chapter)  
- **Structured logs** written to `logs/pipeline.log`  
- **Timezone-aware metadata** in both UTC and IST  

---

## Directory Structure

```
ScriptWeaver/
├── assets/                 # Screenshot snapshots per chapter
├── chromadb_data/         # ChromaDB vector store (future use)
├── logs/
│   ├── final_text/        # All .txt versions + version_manifest.csv
│   ├── pipeline.log       # Structured audit trail
│   └── raw_text/          # Raw chapter dumps (timestamped)
├── Interface/
│   └── main.py            # Entry point
├── AI_Pipeline/
│   ├── AIAgent_Writer.py  # Language model rewrite logic
│   ├── AIAgent_Reviewer.py# Content review logic
│   └── Human_Loop.py      # Prompts for human feedback
├── Scraping/
│   └── Scrape_Screenshot.py # Headless scrape + screenshot
├── Storage/
│   └── RL_Learn.py        # (Optional) reinforcement-based search logic
├── Save_Screenshot.py     # Logging + image handling
├── requirements.txt       # All dependencies
├── rl_rewards.json 	   # Stores feedback for RL version selection
├── Simulate_RL_test       # Demo script to test RL-based retrieval
├── run_pipeline.sh 	   # Optional script to run full pipeline
└── README.md              # You're reading it now

Demo Video Link: https://1drv.ms/v/c/f5acb3ec174cc281/EUQDurJNz1hFs_oY07Y_YwcBucG-g4fP69H0rTN09m2UVg

ScriptWeaver_Presentation.pdf: A visual walkthrough of the entire system.

```

---
## Setup Instructions:

1. Create a Virtual Environment: (optional but recommended)

```bash
python -m venv softnerve_env
```

2. Activate the Environment

```bash
softnerve_env\Scripts\activate
```

3. Install Dependencies


```bash
pip install -r requirements.txt
```

- Compatible with **Python 3.9+**
- Key packages: `openai`, `playwright`, `httpx`, `rich`, `chromadb`, etc.

Also install Playwright browsers (once):

```bash

pip install playwright chromadb openai
playwright install
playwright install-deps


```

---

## Quickstart

```bash
python -m Interface.main 2> >(grep -v "pthread_setaffinity_np")
```

This command triggers the full end-to-end pipeline:

1. Scrapes and screenshots the input chapter  
2. Creates the first AI-generated version (v1)  
3. Prompts for optional human edits (v2, v3…)  
4. Saves finalized versions, metadata, and screenshots  
5. Logs the entire process with timestamps

Note: This command "grep -v "pthread_setaffinity_np" filters out any problematic lines containing pthread_setaffinity_np during logs or script output. It’s a harmless workaround sometimes used in environments where specific system calls cause warnings or crashes.

---


## Suggested Workflow

1. Launch chapter pipeline via CLI  
2. Review AI-generated content (accept or edit)  
3. Check saved `.txt` file in `logs/final_text/`  
4. Inspect `version_manifest.csv` for change history  
5. Review `logs/pipeline.log` for detailed processing trail  


---

## Author and License

**Author:** Alekya Rani Seerapu  
**License:** For project use only. Not for commercial distribution.

