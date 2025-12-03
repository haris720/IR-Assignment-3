# IR Assignment 3 - Information Retrieval System

## Overview
This is a hybrid Information Retrieval System that combines **Boolean Retrieval** and **BM25 Ranking** algorithms to search through news articles. The system is implemented in Python and designed to run on **Google Colab**.

## Features
- 🔍 **Simple Ranked Search** using BM25 algorithm
- 🎯 **Boolean Search** with AND, OR, NOT operators
- 📁 **Category Filter** to search within specific news categories
- 📊 **Evaluation Metrics**: Precision, Recall, F1-Score, MAP, MRR
- ⚡ **Performance Timing** for each query
- 📝 **Text Preprocessing** with NLTK (stopwords removal, lemmatization)

## Requirements
- Python 3.x
- Google Colab account
- Google Drive account
- Articles.csv dataset

### Python Libraries
- pandas
- nltk
- collections (defaultdict, Counter)
- re, math, time (built-in)

## Setup Instructions

### Step 1: Prepare Your Data
1. **Upload your dataset** to Google Drive:
   - File name: `Articles.csv`
   - Location: Place it in the root of "My Drive" (i.e., `/content/drive/MyDrive/Articles.csv`)
   - **IMPORTANT**: The CSV file **must** be in the exact path: `/content/drive/MyDrive/Articles.csv`

2. **CSV Format Requirements**:
   - The CSV should have the following columns:
     - `Heading`: Article title
     - `Article`: Article body/content
     - `Date`: Publication date
     - `NewsType`: Category (e.g., business, sports, tech, etc.)

### Step 2: Open in Google Colab
1. Go to [Google Colab](https://colab.research.google.com/)
2. Upload the notebook file: `IR_Assignment_3 (1).ipynb`
3. Or use: **File → Upload Notebook** → Select the `.ipynb` file

### Step 3: Run the Notebook

#### **STEP 0: Imports and Setup**
Run the first cell to install and download NLTK resources:
```python
import pandas as pd
import math
import re
import time
from collections import defaultdict, Counter
import nltk
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer

nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
```

#### **STEP 1: Mount Google Drive**
**CRITICAL**: Run this cell and authorize Google Drive access:
```python
from google.colab import drive
drive.mount('/content/drive')
file_path = "/content/drive/MyDrive/Articles.csv"
df = pd.read_csv(file_path, encoding="latin1")
```
- A popup will appear asking for permission
- Click on the link and authorize access
- **Make sure** your `Articles.csv` is in `/content/drive/MyDrive/`

#### **STEP 2-5: Preprocessing & Index Building**
Run these cells sequentially to:
- Preprocess text (cleaning, tokenization, stopword removal, lemmatization)
- Build inverted index
- Create BM25 model
- Set up Boolean retrieval

#### **STEP 6: Main Menu Options**

You have **two versions** of the main function:

##### **Option A: Hardcoded Main Menu** (Cell #VSC-03480dd5)
- Runs predefined queries automatically
- Shows examples of different search types
- Includes automatic evaluation
- Best for **demonstration purposes**

##### **Option B: User Input Main Menu** (Cell #VSC-0e5898d0)
- Interactive menu with 3 options:
  1. **Search Query**
     - Simple Ranked Search (BM25)
     - Boolean Search (AND, OR, NOT)
     - Search with Category Filter
  2. **Evaluate System**
     - Input evaluation queries
     - Mark relevant documents
     - Calculate metrics
  3. **Exit**

**Choose ONE** and run it (don't run both).

## How to Use

### Search Examples

#### 1. Simple Ranked Search (BM25)
```
Query: oil price crash
Top-K: 5
```
Returns top 5 documents ranked by BM25 score.

#### 2. Boolean Search
```
Query: karachi AND london
Top-K: 5
```
Returns documents that contain BOTH "karachi" AND "london".

**Boolean Operators:**
- `AND`: Both terms must appear
- `OR`: At least one term must appear
- `NOT`: Exclude documents with the term

Examples:
- `cricket AND pakistan`
- `economy OR politics`
- `trump NOT obama`

#### 3. Category Filter Search
```
Query: stock market
Category: business
Top-K: 5
```
Returns top 5 business articles about "stock market".

### Evaluation Metrics
The system provides comprehensive evaluation:
- **Precision@K**: Relevance of retrieved documents
- **Recall@K**: Coverage of relevant documents
- **F1-Score**: Harmonic mean of precision and recall
- **AP (Average Precision)**: Quality of ranking
- **RR (Reciprocal Rank)**: Position of first relevant document
- **MAP (Mean Average Precision)**: Average AP across queries
- **MRR (Mean Reciprocal Rank)**: Average RR across queries

## File Structure
```
IR-Assignment-3/
│
├── IR_Assignment_3 (1).ipynb    # Main Jupyter notebook
├── README.md                     # This file
└── Articles.csv                  # Dataset (must be in Google Drive)
```

## Important Notes

⚠️ **Critical Requirements:**
1. **Articles.csv MUST be in Google Drive** at `/content/drive/MyDrive/Articles.csv`
2. **Mount Google Drive first** before running any other cells
3. **Run cells in order** from STEP 0 to the final main menu
4. **Don't skip preprocessing steps** (STEP 2-5)
5. **Choose only ONE main menu version** to run

## Troubleshooting

### Issue: "File not found" error
**Solution**: Ensure `Articles.csv` is in `/content/drive/MyDrive/` and you've mounted Google Drive.

### Issue: "No module named 'nltk'"
**Solution**: Run STEP 0 cell to install NLTK and download resources.

### Issue: Drive mount permission denied
**Solution**: Clear browser cookies for Google Colab and try mounting again.

### Issue: Query returns no results
**Solution**: 
- Check if the query terms exist in the dataset
- Try simpler queries
- Use Boolean OR operator to broaden search

## Performance
- Index building: ~5-10 seconds (depending on dataset size)
- Query execution: ~0.01-0.5 seconds per query
- Evaluation: Depends on number of test queries

## Algorithm Details

### BM25 Parameters
- **k1**: 1.5 (term frequency saturation)
- **b**: 0.75 (length normalization)

### Preprocessing Pipeline
1. Lowercase conversion
2. Non-alphabetic character removal
3. Tokenization
4. Stopword removal
5. Lemmatization
6. Title weighting (2x)

## Author
Information Retrieval - Assignment 3

## License
Educational use only

---

**For questions or issues, please contact the course instructor.**
