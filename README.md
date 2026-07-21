# Information Retrieval Project - Group Rosenblatt

<p align="center">
  <img src="https://www.ifrax.it/scuola.png" alt="University of Pisa Logo" width="1200">
</p>

This project was developed as part of the **Multimedia Information Retrieval and Computer Vision** course (A.Y. 2025-2026, Prof. Nicola Tonellotto) for the Master's Degree in *Artificial Intelligence and Data Engineering* at the University of Pisa.

**Authors (Group Rosenblatt):**
* Nilo Fabiano
* Gabriele Frassi
* Samuele Marchi
* Lorenzo Valtriani

## 🚀 Project Overview
The goal of this project is the complete implementation of an efficient and effective **Information Retrieval System (IRS)**. The system covers the entire IR lifecycle: from dataset downloading and preprocessing to the construction of a compressed inverted index, query processing, and performance evaluation.

### Key Features
* **Dataset:** Built using **MSMARCO** (3.2M documents, 8.8M passages), integrating queries and qrels from the 2019 and 2020 TREC Deep Learning tracks for robust benchmarking.
* **Hybrid Python-C++ Approach:** Combines Python's flexibility for preprocessing with C++'s performance (via `pybind11` and `SDSL`) for indexing and high-speed retrieval.
* **Quasi-Succinct Inverted Index:** Implementation of a compressed inverted index using the **Elias-Fano** algorithm to minimize RAM footprint while ensuring fast access.
* **Advanced Scoring:** Support for various ranking functions, including **BM25**, **TF-IDF**, and optimization algorithms like **WAND** (Weak AND).

## 🛠 Technical Architecture

### 1. Text Processing
A rigorous preprocessing pipeline featuring:
* **Tokenization:** Regex-based tokenizer designed to handle acronyms, IP addresses, alphanumeric IDs, and ordinal numbers.
* **Stopwords & Stemming:** Utilizes the *Snowball* algorithm (via `PyStemmer`) optimized with an **LRU Cache**. The cache is sized according to **Heap's** and **Zipf's laws** to maximize hit rate (achieving ~97%).

### 2. Indexing & Compression
The core of the system is the **Quasi-Succinct** index:
* **Elias-Fano Compression:** Posting lists are compressed to drastically reduce memory usage compared to standard inverted indexes.
* **Efficiency:** Leveraging the **SDSL** (Succinct Data Structure Library), `next_geq` operations (essential for WAND) are performed in $O(1)$ time.

### 3. Query Processing & Evaluation
* **Performance:** Comprehensive evaluation of efficiency (latency) and effectiveness (Mean Average Precision, nDCG) using the `ir_measures` library.
* **Benchmarking:** Direct comparison with established baselines such as **PyTerrier**.

## 📁 Notebook Structure
The `IR Project - Rosenblatt.ipynb` notebook is organized into logical sections:
1.  **Environment Setting:** Setup of dependencies (C++ compilers, SDSL, Python libraries).
2.  **Text Processing:** Preprocessor class definition and statistical analysis (Heap/Zipf).
3.  **Inverted Index:** Construction of the base index and the compressed version.
4.  **Query Processing:** Implementation of scoring models and retrieval algorithms.
5.  **Evaluation:** Significance testing and performance reporting.

## ⚙️ Requirements
To run the notebook, **Google Colab** (or a Linux environment with C++17 support) is recommended. Key dependencies include:
* `pybind11` for Python/C++ interfacing.
* `SDSL` (Succinct Data Structure Library).
* Python libraries: `ir_datasets`, `PyStemmer`, `ir_measures`, `python-terrier`.

## 📖 Usage
The notebook supports two execution modes:
* **Drive Mode:** For developers; saves and loads data structures to/from Google Drive to avoid long re-computations.
* **External Mode:** Automatically downloads pre-processed structures from a remote archive for quick consultation without rebuilding the entire index.
