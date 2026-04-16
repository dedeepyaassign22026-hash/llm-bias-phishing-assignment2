# LLM Bias, Trustworthiness and Fairness Evaluation
## COMP 6004 — Deep Learning Applications — Assignment 2
## Adelaide University, 2026

---

## Project Overview

This repository contains the complete replication package for Assignment 2: Evaluating bias, trustworthiness and fairness of open-source LLMs in the context of phishing vulnerability assessment. The study evaluates 15+ models across 6 provider families using a two-prompt synthetic persona pipeline, testing five demographic bias hypotheses and mapping findings to the DECODINGTRUST trustworthiness framework (Wang et al., 2023).

**Research Question:** Do open-source LLMs exhibit statistically significant demographic bias when assessing phishing vulnerability across synthetic personas with diverse characteristics?

**Answer:** Yes — 4 out of 5 demographic dimensions show significant bias. Experience (p<0.001) and education (p<0.001) biases are strongest. Gender shows no significant bias (p=0.261).

---

## Key Findings

| Finding | Result | Significance |
|---|---|---|
| Experience bias | Junior 57.6% vs Expert 8.8% | p<0.001 |
| Education bias | High School 48.5% vs Master 18.6% | p<0.001 |
| Age bias | Middle-aged 33.7% vs Older 13.0% | p=0.006 |
| Geographic bias | Global North 29.8% vs South 24.5% | p=0.031 |
| Gender bias | Female 46.8% vs Male 42.1% | p=0.261 (NOT significant) |
| Personality bias | Neuroticism 75.0% vs Conscientiousness 18.5% | p<0.001 |
| Cultural name bias | Latin American 64.2% vs South Asian 27.2% | p<0.001 |
| Cross-context | Phishing 25.7% vs Healthcare 4.3% vs Cybersecurity 0.0% | p<0.001 |
| Toxicity | Mean 0.0019 — all below 0.05 threshold | PASS |
| DECODINGTRUST | 1/7 dimensions pass, 2/7 fail, 4/7 partial | — |

---

## Repository Structure

├── notebooks/

│   ├── Notebook_1_Data_Collection.ipynb

│   ├── Notebook_2_Data_Extraction.ipynb

│   ├── Notebook_3_Statistical_Analysis.ipynb

│   ├── Notebook_4_Toxicity_and_Context_Analysis.ipynb

│   ├── Notebook_5_Extended_Analysis.ipynb

│   └── Notebook_6_Bias_Mitigation_Testing.ipynb
├── data/
│   ├── raw_dataset.csv
│   ├── clean_dataset.csv
│   ├── structured_dataset.csv
│   ├── toxicity_dataset.csv
│   ├── healthcare_context.csv
│   ├── cybersecurity_context.csv
│   ├── bias_interpretations.csv
│   └── mitigation_results.csv
├── figures/
│   ├── fig1_provider_vulnerability.png
│   ├── fig2_education_vulnerability.png
│   ├── fig3_experience_vulnerability.png
│   ├── fig4_age_vulnerability.png
│   ├── fig5_region_vulnerability.png
│   ├── fig6_significance_summary.png
│   ├── fig7_toxicity_analysis.png
│   ├── fig8_context_comparison.png
│   ├── fig9_decodingtrust_summary.png
│   ├── fig10_consistency_analysis.png
│   ├── fig11_factors_analysis.png
│   ├── fig12_personality_bias.png
│   ├── fig13_cultural_bias.png
│   ├── fig14_wordcloud.png
│   └── fig15_mitigation_results.png
└── README.md


---

## Dataset Summary

| Metric | Value |
|---|---|
| Total samples | 1527 |
| Provider families | 6 |
| Models tested | 15+ |
| Runs per persona group | 10 |
| Collection method | Two-prompt pipeline |
| Contexts evaluated | 3 (Phishing, Healthcare, Cybersecurity) |

---

## Models Used

### Meta (450 samples)
- LLaMA-3.1-8B via Groq
- LLaMA-3.3-70B via Groq
- LLaMA-4-Scout-17B via Groq

### OpenAI OSS (237 samples)
- GPT-OSS-20B via Groq
- GPT-OSS-120B via Groq

### Moonshot AI (210 samples)
- Kimi-K2 via Groq

### Qwen/Alibaba (210 samples)
- Qwen3-32B via Groq

### SDAIA (210 samples)
- Allam-2-7B via Groq

### NVIDIA (201 samples)
- Nemotron-Super-120B via OpenRouter
- Nemotron-Nano-30B via OpenRouter
- Nemotron-9B via OpenRouter

### Google (9 samples — infrastructure limited)
- Gemma3-4B via Together AI
- Note: Google Gemma models were inaccessible across OpenRouter free tier, OpenRouter paid tier, and Together AI free tier. 9 samples collected before quota exhaustion. Excluded from main analysis.

---

## API Infrastructure

| Platform | Models | Notes |
|---|---|---|
| Groq Cloud | Meta, Qwen, OpenAI OSS, Moonshot AI, SDAIA | Primary platform — 100% reliable |
| OpenRouter | NVIDIA Nemotron | $10 credits purchased for rate limit bypass |
| Together AI | Google Gemma | Free tier quota exhausted — 9 samples only |

**Fresh Gmail account** created for all API registrations to prevent prior conversation history bias: dedeepya.assign2.2026@gmail.com

---

## How To Replicate This Study

### Prerequisites
- Google Colab account (free tier sufficient for most notebooks)
- T4 GPU runtime recommended for Notebook 4 (Detoxify)
- API keys required (see below)

### Step 1 — Get API Keys
Register for free accounts at:
- **Groq:** https://console.groq.com — primary collection platform
- **OpenRouter:** https://openrouter.ai — for NVIDIA models (free tier or $10 credits)
- **GitHub:** Personal access token for pushing results

### Step 2 — Set Up Colab Secrets
In each notebook add these secrets via the 🔑 icon:

GROQ_API_KEY = your_groq_key
OPENROUTER_API_KEY = your_openrouter_key
GITHUB_TOKEN = your_github_pat

### Step 3 — Run Notebooks In Order

**Notebook 1 — Data Collection** (~4 hours)
- Collects raw responses from all providers
- Saves raw_dataset.csv and clean_dataset.csv
- Expected output: 1500+ samples

**Notebook 2 — Data Extraction** (~3 minutes)
- Extracts structured fields using universal regex parser
- Handles 6 different response formats across providers
- Saves structured_dataset.csv

**Notebook 3 — Statistical Analysis** (~2 minutes)
- Runs 5 hypothesis tests plus provider analysis
- Generates Figures 1-6
- Saves all statistical results

**Notebook 4 — Toxicity and Context Analysis** (~30 minutes)
- Runs Detoxify on all 1527 responses (requires GPU)
- Collects Healthcare and Cybersecurity context data
- Maps findings to DECODINGTRUST 7 dimensions
- Generates Figures 7-9

**Notebook 5 — Extended Analysis** (~45 minutes)
- Consistency and hallucination rate analysis
- Factors mentioned, personality, cultural bias
- Word cloud and bias interpretation generation
- Generates Figures 10-14

**Notebook 6 — Bias Mitigation Testing** (~20 minutes)
- Tests three prompt-based mitigation strategies
- Compares against baseline vulnerability rates
- Generates Figure 15

### Step 4 — Expected Outputs
After running all notebooks you will have:
- 1527 structured records across 6 providers
- 15 publication-quality figures
- Statistical test results for 8 hypotheses
- DECODINGTRUST dimension mapping
- Bias mitigation comparison

---

## Prompt Design

### Prompt 1 — Persona Generation
Generates three culturally diverse synthetic personas with mandatory fields: name, age, personality trait (Big Five), domain of work, geographical location, education level, years of experience. Each persona limited to 300 characters.

### Prompt 2 — Vulnerability Assessment
Asks model to select which persona is most susceptible to phishing/scam attack with detailed reasoning. Run 10 times per persona group to measure consistency.

### Mitigation Prompts
Three variations tested:
- **Mitigation A:** Explicit instruction to ignore demographic factors
- **Mitigation B:** Counter-stereotype with research citation
- **Mitigation C:** System-level fairness instruction

---

## Statistical Methods

| Test | Used For | Justification |
|---|---|---|
| Chi-square | Age, education, experience, provider | Multiple categories |
| Fisher Exact | Gender, geographic region | Binary categories |
| T-test (independent) | Age mean, experience mean | Continuous variables |
| ANOVA | Toxicity by group | Multiple group comparison |

Significance threshold: p < 0.05 throughout.

---

## DECODINGTRUST Results Summary

| Dimension | Verdict | Key Evidence |
|---|---|---|
| Toxicity | TRUSTWORTHY | Mean 0.0019, zero above threshold |
| Stereotype Bias | NOT TRUSTWORTHY | Education p<0.001, Experience p<0.001 |
| Adversarial Robustness | PARTIALLY TRUSTWORTHY | 15.3% hallucination rate |
| Privacy and Security | REQUIRES MONITORING | Demographic profiling patterns |
| Factuality | PARTIALLY TRUSTWORTHY | Age pattern contradicts literature |
| Fairness | NOT TRUSTWORTHY | 4/5 dimensions significant |
| Machine Ethics | CONTEXT-DEPENDENT | Cybersecurity 0% vs Phishing 25.7% |

**Overall: 1/7 pass, 2/7 fail, 4/7 partial**

---

## Limitations

1. **Google Gemma inaccessibility** — infrastructure restrictions across all tested platforms
2. **Gender coverage** — 43% of records due to models not using explicit pronouns
3. **Name coverage** — 54% extraction rate due to varied response formats
4. **Mitigation sample size** — n=9 per condition due to rate limit exhaustion
5. **Perspective API** — pending Google manual approval at submission time; Detoxify used as equivalent
6. **Cultural name classification** — 64% classification rate; results directional only

---

## Framework References

- Wang et al. (2023) DECODINGTRUST: https://arxiv.org/pdf/2306.11698
- Sarker et al. (2023) Personalised Phishing Guidelines: arXiv:2311.12827
- Hanu and Unitary (2020) Detoxify: https://github.com/unitaryai/detoxify

---

## Author

**Dedeepya Korukonda**
Master of Artificial Intelligence and Machine Learning
Adelaide University, 2026

Assignment 2 — COMP 6004 Deep Learning Applications
Submission: April 16, 2026
