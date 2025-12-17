# Intelligent Lead Scoring Agent for Investigative Toxicology

An automated, reproducible data pipeline that identifies and prioritizes high-intent scientific and commercial leads in the **investigative toxicology and liver safety** space. The system simulates multi-source signal ingestion (publications, conferences, funding, and grants), enriches entities with structured attributes, applies a transparent scoring model, and outputs ranked leads for downstream business development or research collaboration workflows.

This project focuses on **signal design, scoring logic, and pipeline architecture** rather than live web scraping, ensuring ethical compliance and reproducibility while demonstrating real-world applicability.

---

## Demo Output

The demo produces a ranked table of leads with individual signal flags and a final composite score, suitable for export to CSV, Google Sheets, or CRM ingestion.

**Core output fields:**

* Researcher / Organization Name
* Affiliation Type (Academic / Biotech)
* Recent Publication Signal
* Conference Activity Signal
* Funding / Grant Signal
* Keyword Match Strength
* Final Lead Score
* The link: https://lead-scoring-agents-chsz2hddkmrpdy3x48ydmz.streamlit.app/

---

## High-Level Architecture

The pipeline is designed as a modular, end-to-end workflow that can later be connected to live APIs or crawlers.

**Logical stages:**

1. **Ingest** – Load structured records representing researchers, companies, and labs (mocked data derived from real-world source schemas).
2. **Normalize** – Standardize fields such as keywords, publication recency, funding stage, and affiliation type.
3. **Enrich** – Attach domain-specific signals (toxicity focus, liver model relevance, activity indicators).
4. **Score** – Apply a weighted scoring model that reflects scientific intent, market readiness, and budget availability.
5. **Rank & Export** – Sort entities by final score and output a clean, reproducible dataset.

The architecture intentionally separates **signal ingestion** from **scoring logic**, allowing future upgrades without refactoring the core model.

---

## Data Sources (Real + Mocked)

The demo dataset simulates structured outputs from the following real-world sources. Live crawling is intentionally out of scope for this phase.

### 1. Scientific Publication Databases

**Primary sources:** PubMed, Google Scholar, bioRxiv
**Signals modeled:**

* Keyword presence (DILI, hepatic spheroids, organ-on-chip, 3D cell culture)
* Publication recency (last 12–24 months)
* Authorship importance (first or corresponding author)

### 2. Biomedical Conference Events

**Primary sources:** SOT, AACR, ISSX, ACT
**Signals modeled:**

* Poster or abstract presenter
* Agenda speaker or session contributor
* Exhibitor or attending organization

### 3. Business & Funding Intelligence

**Primary sources:** Crunchbase, PitchBook, FierceBiotech, Biopharm Guy
**Signals modeled:**

* Funding stage (Seed, Series A, Series B+)
* Recent funding announcements
* Active pipeline or partnership indicators

### 4. Public Grant Databases

**Primary sources:** NIH RePORTER (USA), CORDIS (EU)
**Signals modeled:**

* Grant awards related to liver toxicity or advanced in vitro models
* Grant lifecycle stage (recently awarded vs. expiring)

This approach mirrors how production BD intelligence tools operate while remaining compliant and reproducible.

---

## Scoring Logic

The scoring model is intentionally transparent and interpretable.

| Signal Category      | Condition Met                              | Weight |
| -------------------- | ------------------------------------------ | ------ |
| Publication Recency  | Published in last 12–24 months             | +25    |
| Keyword Relevance    | ≥2 high-intent toxicology keywords         | +20    |
| Conference Activity  | Speaker / Presenter / Exhibitor            | +15    |
| Funding Stage        | Series A / B / Major Grant                 | +20    |
| Affiliation Strength | Dedicated toxicology or liver safety focus | +10    |

**Final Score = Sum of all applicable signals**

This weighting prioritizes **scientific intent first**, followed by **market readiness and budget availability**.

---

## Key Design Decisions & Problems Solved

### 1. Ethical & Legal Compliance

**Problem:** Live scraping of platforms like LinkedIn, PubMed, or paid databases introduces ToS and licensing risks.

**Solution:** The pipeline consumes mocked-but-realistic structured data that reflects how these sources would be integrated in production.

---

### 2. Signal Quality over Raw Volume

**Problem:** Raw publication or attendance counts produce noisy lead lists.

**Solution:** The model prioritizes **recent activity**, **specific domain keywords**, and **decision-maker roles** rather than aggregate metrics.

---

### 3. Budget Awareness in Lead Ranking

**Problem:** Scientifically relevant leads may lack purchasing power.

**Solution:** Funding rounds and grant awards are explicit scoring dimensions, separating high-interest researchers from high-capability buyers.

---

### 4. Reproducibility by Design

**Problem:** Many data science demos cannot be rerun consistently.

**Solution:** All inputs are deterministic, version-controlled, and free of external API dependencies, enabling consistent reruns and evaluation.

---

## Reproducibility Instructions

1. Clone the repository
2. Create and activate a virtual environment
3. Install dependencies
4. Run the scoring script to generate ranked leads

The output will be a reproducible table identical across runs, ensuring easy evaluation and extension.

---

## Tech Stack

* Python 3.x
* Pandas for data manipulation
* NumPy for scoring logic
* CSV / DataFrame outputs (extensible to Google Sheets or CRM)

The stack is intentionally lightweight to maximize portability.

---

## Future Enhancements

* Live ingestion via PubMed, Crossref, and conference APIs
* Named-entity recognition for automated author and institution extraction
* Temporal decay functions for signal freshness
* CRM integration (HubSpot / Salesforce)
* Active learning loop using BD feedback to refine scoring weights

---

This project demonstrates **product thinking, domain understanding, and scalable data design**, aligning closely with real-world scientific business development and intelligence platforms.

