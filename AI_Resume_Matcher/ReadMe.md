
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
```
## How the scoring works?

The final score combines multiple signals:
- TF-IDF score: lexical similarity between resume and job description
- Embedding score: semantic similarity using sentence transformers
- Skill coverage score: proportion of required skills covered by the resume
- LLM score: structured evaluation from a local LLM

## Final score formula
Final Score =
0.10 × TF-IDF
+ 0.30 × Embedding Similarity
+ 0.25 × Skill Coverage
+ 0.35 × LLM Score

This weighting gives more importance to semantic understanding and structured evaluation, while still preserving interpretable classical signals.

## Example Output
```
ml_engineer.txt
  TF-IDF Score: 0.262
  Embedding Score: 0.698
  Skill Coverage Score: 0.833
  LLM Score: 0.825
  Final Score: 0.735
  Final Score (out of 10): 7.35/10
  Match Level: High Match
  Required Skills: cloud, data pipelines, machine learning, model deployment, nlp, python
  Missing Skills: model deployment
  Strengths: data analysis, machine learning, nlp, python, statistical modeling
  Summary: Good overall fit, but notable gaps remain in: model deployment.

```

---

## Tech stack

- Python  
- scikit-learn  
- sentence-transformers  
- pandas  
- langdetect  
- Ollama  
- Mistral  

---

## How to run

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/ai-resume-job-matcher.git
cd ai-resume-job-matcher
```
### 2. Create and activate a virtual environment
```bash
pip install -r requirements.txt
```
### 3. Install dependencies
```bash
python3 -m venv venv
source venv/bin/activate
```
### 4. Make sure Ollama is installed

Install from: 
```bash
(https://ollama.com)
```
Then pull and run the model:
```bash
ollama run mistral
```
If needed, start the Ollama service:
```bash
ollama serve
```
### 5. Add your resume and job descriptions
Put your resume ```bash .txt``` file inside:
```bash
data/resumes/
```
Put job descriptions as ```bash .txt``` files inside:
```bash
data/job_descriptions/
```
### 6. Run the Matcher
```bash
python main.py
```
### 7. Check results

The ranked output will be shown in the terminal and saved to:

```bash
results/match_results.csv
```

## Why I used a TXT resume instead of PDF

PDF resumes are great for human readers, but text extraction from PDFs often introduces noise such as:

- broken words
- strange Unicode characters
- bad line reconstruction

Since this project depends on text matching, a clean ```bash .txt``` version of the resume gives much more reliable results.
The PDF can still be used for actual applications, while the ```bash .txt``` version is better for the matching pipeline.

## Limitations

This is still a prototype, not a production ATS system.

Current limitations include:

skill extraction is not perfect

- semantic skill matching is still approximate
- translation quality depends on the local LLM
- scoring weights are hand-tuned
- resume parsing currently works best with plain text input
- no web UI yet

## Possible improvements

Some natural next steps for this project are:

- add PDF resume parsing with cleanup
- cache translations so the same JD is not retranslated every run
- cache extracted required skills
- add a Streamlit interface
- support multiple resumes
- add section-aware scoring
- improve semantic skill matching
- add multilingual embedding models
- export detailed reports

## What I learned

This project was a good exercise in combining classical NLP with modern embedding-based and LLM-based methods.

A few things became very clear while building it:

- exact keyword matching alone is not enough
- multilingual handling matters in real applications
- local LLMs are useful, but need guardrails
- structured reasoning is only reliable when combined with deterministic checks
- good scoring systems need calibration, not just more models

## Author

### Rohaan Deb

If you found this project interesting, feel free to connect with me on LinkedIn.












