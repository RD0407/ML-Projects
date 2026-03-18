
# AI Resume Job Matcher

A hybrid NLP project that matches a resume to job descriptions using a combination of classical text similarity, semantic embeddings, skill coverage analysis, and local LLM-based evaluation.

The goal of this project is to go beyond simple keyword matching and build a more realistic resume-job fit system that can handle both English and Italian job descriptions.

---

## Why I built this

Many job applications are filtered by systems that rely heavily on keywords, even when a candidate is actually a strong fit. This becomes even more difficult in multilingual settings, especially when a resume is written in English and the job description is written in Italian.

I built this project to explore a more practical and explainable way to evaluate resume-job alignment by combining:

- lexical matching
- semantic similarity
- required skill coverage
- structured LLM reasoning

This project is designed as a small but realistic prototype of a resume matching system.

---

## What the project does

For each job description, the pipeline:

1. loads the resume and job descriptions
2. detects whether the job description is in English
3. translates non-English job descriptions into English using a local LLM
4. computes TF-IDF similarity
5. computes semantic similarity using sentence embeddings
6. extracts required skills from the job description
7. checks which required skills are missing from the resume
8. runs a local LLM evaluation for:
   - skill match
   - experience match
   - tooling match
   - responsibility alignment
9. combines all of these signals into a final score
10. outputs a ranked list of job matches with explanations

---

## Features

- Resume to job matching
- English and Italian job description support
- Automatic translation only when needed
- TF-IDF based lexical similarity
- Sentence-transformer based semantic similarity
- Required skill extraction from the job description
- Missing skill detection
- Skill coverage scoring
- Local LLM evaluation using Ollama
- Final weighted scoring
- CSV export of results

---

## Project structure

```text
ai_resume_job_matcher/
│
├── data/
│   ├── resumes/
│   │   └── rohaan_cv.txt
│   └── job_descriptions/
│       ├── ml_engineer.txt
│       └── data_analyst.txt
│
├── results/
│   └── match_results.csv
│
├── src/
│   ├── preprocessing.py
│   ├── vectorization.py
│   ├── similarity.py
│   ├── embedding_matcher.py
│   ├── translator.py
│   ├── llm_evaluator.py
│   └── utils.py
│
├── main.py
├── requirements.txt
└── README.md
