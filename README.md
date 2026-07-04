# 🔬 Automated Research Paper Analyzer

An AI-powered web application that reads, understands, summarizes, and answers questions about research papers — built as a Senior Design Project (SDP) at **VIT-AP University**.

Upload any research paper as a PDF and get instant AI-generated summaries, keyword & scientific term extraction, ML method detection, domain classification, similar paper recommendations, quality scoring, and an interactive chatbot that can answer questions about the paper's content.

---

## 👥 Authors

- **A. Shiva**
- **K. Siddharth** 

**Guide:** Dr. Kumar Debasis, Associate Professor Grade-1, Department of Networking and Security
**School:** School of Computer Science and Engineering, VIT-AP University

---

## 📖 Overview

Reviewing scientific literature manually is slow and demands significant domain expertise — researchers often spend days or weeks reading papers just to write a survey or literature review. This project builds an integrated, end-to-end pipeline that combines **NLP, Machine Learning, Transformer models, Vector Embeddings, and Generative AI** to automate that process.

## ✨ Features

- 📄 **Accurate PDF Text Extraction** — powered by PyMuPDF, handles multi-column layouts, embedded fonts, and complex structures
- 🧩 **Section Detection** — automatically identifies Abstract, Introduction, Methodology, Results, and Conclusion
- 📝 **Abstractive Summarization** — uses `facebook/bart-large-cnn` (BART) to generate human-like, concise summaries
- 🔑 **Keyword & Scientific Term Extraction** — hybrid approach combining RAKE, YAKE, TF-IDF, and rule-based scientific term detection
- 🤖 **ML Method Detection** — automatically identifies techniques used in the paper (CNN, RNN, LSTM, SVM, Random Forest, etc.)
- 🏷️ **Research Domain Classification** — TF-IDF + Voting Classifier (SVM + Logistic Regression + Random Forest) predicts the paper's research domain
- 📊 **Quality Scoring** — evaluates Readability (Flesch Reading Ease), Structural Completeness, and Citation strength
- 🔍 **Similar Paper Retrieval** — fetches related papers via the Semantic Scholar API
- 💬 **RAG-Based Chat with the Paper** — ask natural-language questions and get context-grounded answers using Sentence Embeddings + ChromaDB + Gemini AI
- 📈 **Interactive Visualizations** — word clouds, radar charts, gauge indicators, and bar graphs via Plotly & Matplotlib

## 🏗️ System Architecture

```
User → Streamlit UI (app.py) → Core Analysis Engine (rp.py)
     → Summarization / Keyword Extraction / Classification
     → Chunking → Embeddings (MiniLM) → ChromaDB
     → Gemini AI (RAG) → Results back to User
```

The system is organized into three main layers:
1. **Application Layer** — Streamlit-based frontend for upload, interaction, and visualization
2. **Analysis Layer** — Core NLP/ML/Summarization engine (`rp.py`)
3. **Embedding & Vector Storage Layer** — Sentence embeddings stored in ChromaDB for Retrieval-Augmented Generation (RAG)

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| **Frontend** | Streamlit |
| **PDF Processing** | PyMuPDF (fitz) |
| **NLP** | NLTK, spaCy, RAKE, YAKE, TF-IDF |
| **Summarization** | BART (`facebook/bart-large-cnn`) via Hugging Face Transformers |
| **Embeddings** | Sentence-Transformers (`all-MiniLM-L6-v2`) |
| **Vector Database** | ChromaDB |
| **Domain Classification** | TF-IDF Vectorizer + Voting Classifier (SVM, Logistic Regression, Random Forest) — scikit-learn |
| **Generative AI (RAG)** | Google Gemini AI (`google-generativeai`) |
| **Similar Paper Search** | Semantic Scholar API |
| **Visualization** | Plotly, Matplotlib, WordCloud |
| **ML Framework** | PyTorch |

## 📂 Project Structure

```
Automated-Research-Paper-Analyzer/
├── app.py                          # Streamlit frontend & UI logic
├── rp.py                           # Core analysis engine (NLP, ML, summarization, RAG)
├── 10000 generic english words.txt # Blacklist used for scientific term filtering
├── models/                         # Pretrained ML models (TF-IDF vectorizer, Voting Classifier, Label Encoder) — not tracked in Git
├── .gitignore
└── README.md
```

> **Note:** The `models/` folder (trained classifier artifacts) and `venv/` are excluded from version control via `.gitignore`. You'll need to regenerate or add your own trained models to run domain classification.

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- A Google Gemini API key (for the chat/RAG feature)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AlladaShiva/Automated-Research-Paper-Analyzer.git
   cd Automated-Research-Paper-Analyzer
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   # Windows
   .\venv\Scripts\Activate.ps1
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install streamlit pandas matplotlib wordcloud plotly sentence-transformers chromadb google-generativeai pymupdf nltk spacy rake-nltk textstat yake joblib scikit-learn torch transformers requests
   ```

4. **Add your Gemini API key**
   Create a file at `.streamlit/secrets.toml`:
   ```toml
   [gemini]
   api_key = "YOUR_GEMINI_API_KEY"
   ```

5. **Run the app**
   ```bash
   streamlit run app.py
   ```

## 📊 Results Snapshot

| Module | Performance |
|---|---|
| Text Extraction (PyMuPDF) | 96–99% accuracy across paper formats |
| Section Detection | 92–100% accuracy by section type |
| Summarization (BART) | ROUGE-1: 0.62, ROUGE-2: 0.48, ROUGE-L: 0.58 |
| Domain Classification | 87–94% accuracy across domains |
| RAG Q&A (Gemini) | Correctness: 4.8/5, Context Grounding: 4.6/5, Fluency: 4.9/5 |

*(Full evaluation methodology and results available in the project report.)*

## 🔮 Future Enhancements

- OCR support for scanned/handwritten PDFs (Tesseract / Google Vision)
- Transformer-based domain classifiers (SciBERT, PubMedBERT)
- Multi-paper comparison engine
- Plagiarism detection & citation network visualization
- Exportable reports (PDF/DOCX/LaTeX)

## 📄 License

This project was developed as an academic Senior Design Project at VIT-AP University. Feel free to reference or build upon it for educational purposes.
