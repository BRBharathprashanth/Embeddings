# Embeddings
'matching_results_df' DataFrame, which stores the ranked list of resumes that best match each job description based on cosine similarity scores. This data frame is crucial for presenting the final output of the resume matching system.


# AI Resume–Job Description Matching System

An NLP-based Resume Screening and Job Matching System that automatically ranks resumes against job descriptions using Semantic Embeddings and Cosine Similarity.

This project helps recruiters and hiring teams identify the most relevant candidates by comparing resume content with job requirements using modern Transformer-based language models.

---

## Project Overview

Traditional keyword matching often misses strong candidates because different words can express similar skills.

This project uses Sentence Transformers to generate semantic embeddings for both resumes and job descriptions, allowing the system to understand meaning rather than just exact keywords.

The system:

- Extracts text from PDF resumes
- Extracts text from Job Description PDFs
- Converts text into vector embeddings
- Computes similarity scores
- Ranks resumes for each job description
- Exports top matching candidates

---

## Features

- PDF Resume Parsing
- Job Description Parsing
- Semantic Text Embeddings
- Cosine Similarity Matching
- Resume Ranking
- Batch Processing
- CSV Export of Results
- Scalable for Large Resume Collections

---

## Tech Stack

### Programming Language
- Python

### Libraries
- Sentence Transformers
- Transformers
- PyMuPDF (fitz)
- Scikit-learn
- Pandas
- NumPy
- tqdm

### NLP Model
- all-MiniLM-L6-v2

---

## Project Workflow

```text
Resume PDFs
      │
      ▼
Extract Text
      │
      ▼
Generate Resume Embeddings
      │
      ▼
Generate JD Embeddings
      │
      ▼
Calculate Cosine Similarity
      │
      ▼
Rank Resumes
      │
      ▼
Export Results CSV
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/resume-jd-matching.git
cd resume-jd-matching
```

Install dependencies:

```bash
pip install sentence-transformers
pip install transformers
pip install pymupdf
pip install scikit-learn
pip install pandas
pip install numpy
pip install tqdm
```

Or install all at once:

```bash
pip install sentence-transformers transformers pymupdf scikit-learn pandas numpy tqdm
```

---

## Dataset Structure

### Resumes Folder

```text
Education/
│
├── Resume1.pdf
├── Resume2.pdf
├── Resume3.pdf
└── ...
```

### Job Description File

```text
20_Job_Descriptions.pdf
```

Each page contains one job description.

---

## How It Works

### Step 1: Resume Extraction

The system reads all PDF resumes using PyMuPDF and extracts text.

```python
doc = fitz.open(filepath)
text += page.get_text()
```

---

### Step 2: Job Description Extraction

Each page of the JD PDF is treated as a separate job description.

```python
title = text.split("\n")[0]
```

The title is boosted to improve matching accuracy.

```python
enhanced_text = (title + " ") * 10 + text
```

---

### Step 3: Embedding Generation

The Sentence Transformer converts text into dense vector representations.

```python
model = SentenceTransformer(
    "all-MiniLM-L6-v2"
)
```

Example:

```text
Python Developer
      ↓
[0.23, -0.44, 0.15, ...]
```

---

### Step 4: Similarity Calculation

Cosine Similarity measures how closely a resume matches a job description.

Formula:

Cosine Similarity = (A · B) / (||A|| ||B||)

Where:

- A = Resume Embedding
- B = JD Embedding

Score Range:

| Score | Meaning |
|---------|---------|
| 1.0 | Perfect Match |
| 0.8+ | Strong Match |
| 0.6–0.8 | Moderate Match |
| <0.5 | Weak Match |

---

### Step 5: Ranking

Resumes are sorted in descending order of similarity score.

```python
np.argsort(scores)[::-1]
```

Top candidates are selected for each job description.

---

## Output

Generated file:

```text
top_matching_resumes.csv
```

Example:

| Job Description | Rank | Resume Filename | Similarity Score |
|---------------|------|-----------------|-----------------|
| Data Scientist | 1 | resume1.pdf | 0.92 |
| Data Scientist | 2 | resume7.pdf | 0.88 |
| Data Scientist | 3 | resume3.pdf | 0.84 |

---

## Example Use Cases

- Resume Screening
- Talent Acquisition
- Candidate Ranking
- Recruitment Automation
- HR Analytics
- ATS Enhancement
- Campus Hiring

---

## Advantages

- Faster than manual screening
- Understands semantic meaning
- Reduces recruiter workload
- Handles large resume datasets
- Improves candidate-job alignment
- Works beyond keyword matching

---

## Future Improvements

- Web Application using Flask/FastAPI
- Resume Skill Extraction
- Experience-Based Filtering
- Education-Based Filtering
- Candidate Dashboard
- Recruiter Dashboard
- Hybrid Retrieval with Vector Databases
- LLM-Powered Resume Summaries
- Integration with Applicant Tracking Systems (ATS)

---

## Author

**Bharath Prashanth BR**

AI Engineer | GenAI Engineer | Data Scientist

LinkedIn:
www.linkedin.com/in/bharath-prashanth-beluguppa-racharla

GitHub:
github.com/BRBharathprashanth

---

## License

This project is intended for educational, research, and recruitment automation purposes.
