# [Article] Context-Aware and Retrieval-Augmented Sarcasm Detection

This repository contains the **research paper and documentation** for the project: **"Context-Aware and Retrieval-Augmented Sarcasm Detection in Social Media"**.

---

## 🚧 Status: Work in Progress
**This project is currently under active development.** 
The research methodology and the implementation code are being refined simultaneously.

---

## 🔗 Project Ecosystem
To ensure a clean separation between research and implementation, the project is split into two repositories:

1.  **Article Repository (This one):** Contains the LaTeX source, bibliography, and the latest PDF version of the research paper.
2.  **[Code Repository (Sarcasm-Detection)](https://github.com/mina-mtb/Sarcasm-Detection):** Contains the implementation pipeline, datasets, and experiment notebooks.

---

## 📝 Abstract
Sarcasm detection is a challenging natural language processing task because the intended meaning of a text often differs from its literal wording and depends on conversational context. This research investigates whether a transformer-based classifier (RoBERTa/DeBERTa) that uses both a target comment and its conversational context can detect sarcasm more effectively than context-free baselines.

**Key Research Directions:**
*   **Contextual Modeling:** Integrating parent comments to capture conversational incongruity.
*   **Retrieval Augmentation:** Using FAISS to retrieve semantically similar sarcastic/non-sarcastic examples to support classification.
*   **Explainability:** Leveraging retrieved examples to provide evidence for model predictions.

---

## 📄 File Overview
*   `main_updated.tex`: Core LaTeX document.
*   `main_updated.pdf`: Latest compiled version for reading.
*   `references_sarcasm.bib`: Comprehensive list of citations.
*   `project_references_sarcasm.tex`: Reference formatting data.

## 🛠️ Compilation
You can compile the LaTeX files locally using `pdflatex` + `bibtex` or by importing this repository into [Overleaf](https://www.overleaf.com/).

---

## 👤 Author
**Mina Tahmasebi Berjouei**  
*Part of the "Advanced Machine Learning with Neural Networks" course.*
