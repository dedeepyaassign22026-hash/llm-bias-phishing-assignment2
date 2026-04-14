# llm-bias-phishing-assignment2
LLM Bias, Trustworthiness and Fairness Evaluation - Phishing Vulnerability Theme


# LLM Bias, Trustworthiness and Fairness Evaluation
## Assignment 2 — COMP 6004 Advanced Topics in AI/ML
## University of Adelaide, 2026

### Project Overview
This repository contains the complete replication package for Assignment 2:
Evaluating bias, trustworthiness and fairness of open-source LLMs with
respect to phishing vulnerability assessment.

### Research Question
Do open-source LLMs exhibit demographic bias when assessing phishing
vulnerability across synthetic personas with diverse characteristics?

### Dataset Summary
- Total samples: 1530
- Provider families: 6 (Meta, Qwen, OpenAI OSS, Moonshot AI, SDAIA, NVIDIA)
- Collection method: Two-prompt pipeline (persona generation + vulnerability assessment)
- Prompt 1: Generate three diverse personas
- Prompt 2: Assess which persona is most vulnerable to phishing (10 runs per group)

### Provider Distribution
| Provider | Samples | Models |
|---|---|---|
| Meta | 450 | LLaMA 3.1, 3.3, 4 Scout |
| OpenAI OSS | 240 | GPT-OSS-20B, GPT-OSS-120B |
| Moonshot AI | 210 | Kimi-K2 |
| Qwen/Alibaba | 210 | Qwen3-32B |
| SDAIA | 210 | Allam-2-7B |
| NVIDIA | 201 | Nemotron Nano, Super, 9B |

### Repository Structure
notebooks/
    Notebook_1_Data_Collection.ipynb
    Notebook_2_Data_Extraction.ipynb
    Notebook_3_Statistical_Analysis.ipynb
    Notebook_4_Visualisations.ipynb
data/
    raw_dataset.csv
    clean_dataset.csv
    structured_dataset.csv
    raw_responses/
        all_records_checkpoint.json
README.md

### API Infrastructure
- Primary: Groq Cloud (Meta, Qwen, OpenAI OSS, Moonshot AI, SDAIA)
- Secondary: OpenRouter with credits (NVIDIA Nemotron)
- Fresh Gmail created for all API registrations to prevent history bias

### Infrastructure Findings
- Google Gemma inaccessible across all platforms tested
- OpenRouter free tier exhausts quota under rapid requests
- Groq Cloud showed 100% reliability throughout collection

### Framework
Based on DECODINGTRUST framework (Wang et al., 2023)
Reference: https://arxiv.org/pdf/2306.11698

### Author
Dedeepya Korukonda
Master of Artificial Intelligence and Machine Learning
University of Adelaide, 2026
