# Context-Aware and Retrieval-Augmented Sarcasm Detection

This repository contains the academic article and poster materials for the project
**Context-Aware and Retrieval-Augmented Sarcasm Detection in Social Media**.

The implementation, experiments, generated outputs, and source code for the full
machine learning pipeline are maintained in the main project repository:

**Project repository:** [mina-mtb/Sarcasm-Detection](https://github.com/mina-mtb/Sarcasm-Detection)

## Overview

Sarcasm detection is a challenging natural language processing task because the
intended meaning of a sentence can conflict with its literal wording. This is
especially difficult in social media, where comments are short, informal, noisy,
and often depend on conversational context.

This project studies sarcasm detection as a binary classification task over
Reddit parent-reply pairs from the SARC dataset. The central research question is
whether a transformer classifier can identify sarcasm more effectively when it
receives both the parent comment and the target reply, rather than the reply
alone. The project also evaluates retrieval-based evidence as an auxiliary
signal for prediction and interpretation.

## Repository Contents

The repository is organized into two main folders:

```text
.
|-- Poster/
|   |-- poster.tex
|   |-- Makefile
|   |-- beamerthemegemini.sty
|   |-- beamercolorthemenott.sty
|   `-- logos/
|       |-- chalmers_emblem_white.png
|       `-- university_of_gothenburg_emblem_white.png
|
|-- Report/
|   |-- main.tex
|   `-- biblio-TIF360-FYM360.bib
|
|-- .gitignore
`-- README.md
```

### `Poster/`

The `Poster` folder contains the LaTeX source for the final academic poster.
It uses the Gemini Beamer poster theme and is formatted as an A3 portrait
research poster.

The poster summarizes:

- the motivation for sarcasm detection in social media;
- the SARC-based binary classification task;
- the lexical, transformer, and retrieval-augmented methods;
- the main performance results;
- the key conclusions from the experiment.

### `Report/`

The `Report` folder contains the full article source written in LaTeX using the
`revtex4-2` document class. It includes the complete research narrative,
methodology, evaluation results, discussion, limitations, and bibliography.

The report covers:

- the background and motivation for context-aware sarcasm detection;
- related work on sarcasm, transformers, and retrieval-augmented NLP;
- preprocessing and dataset construction;
- TF-IDF logistic regression baseline;
- `distilroberta-base` reply-only and parent-reply classifiers;
- retrieval-augmented stacking with nearest-neighbor evidence;
- final test-set evaluation and error analysis.

## Project Relationship

This repository is the **article and presentation repository**. It is intended
for writing, documenting, and presenting the research.

The companion repository contains the actual project implementation:

[https://github.com/mina-mtb/Sarcasm-Detection](https://github.com/mina-mtb/Sarcasm-Detection)

That main repository contains the code and experiment pipeline used to produce
the results discussed in this article, including data preparation, training,
evaluation, retrieval artifacts, prediction files, and final metrics.

## Research Summary

The project compares several approaches to sarcasm detection:

| Model family | Input setting | Role |
| --- | --- | --- |
| TF-IDF + Logistic Regression | Target reply only | Lightweight lexical baseline |
| DistilRoBERTa classifier | Target reply only | Context-free transformer baseline |
| DistilRoBERTa classifier | Parent comment + target reply | Main context-aware model |
| Retrieval stacker | Supervised probabilities + retrieval features | Calibrated retrieval-augmented model |

The key experimental control is input construction. The two transformer
experiments use the same `distilroberta-base` architecture, but differ in
whether the model receives only the target reply or the parent comment together
with the reply.

## Main Results

The final evaluation is performed on a held-out test set of 151,496 Reddit
examples, with 75,759 sarcastic and 75,737 non-sarcastic instances.

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| TF-IDF + Logistic Regression | 0.722 | 0.739 | 0.686 | 0.712 | 0.795 |
| DistilRoBERTa, reply only | 0.772 | 0.757 | 0.803 | 0.779 | 0.859 |
| DistilRoBERTa, parent + reply | 0.782 | 0.765 | 0.816 | 0.790 | 0.869 |
| Retrieval stacker | 0.790 | 0.809 | 0.759 | 0.784 | 0.871 |

The context-aware DistilRoBERTa model achieves the best F1-score and recall
among the single-model systems. This supports the hypothesis that conversational
context improves sarcasm detection, although the gain is moderate rather than
dramatic.

The retrieval-augmented stacker achieves the highest accuracy, precision, and
ROC-AUC, but has lower recall. This suggests that retrieval is most useful as a
supporting and calibrating signal, rather than as a replacement for supervised
context-aware classification.

## Key Findings

- Conversational context improves sarcasm detection when the architecture is
  held fixed.
- The strongest single model is the parent-reply `distilroberta-base`
  classifier, with an F1-score of 0.790.
- Retrieval-augmented stacking improves precision and ROC-AUC, but trades off
  recall.
- Retrieval-only nearest-neighbor prediction is not strong enough to serve as a
  standalone sarcasm classifier.
- Sarcasm remains difficult because many examples require pragmatic context,
  community knowledge, author intent, or broader world knowledge.

## Compilation

### Requirements

To compile the LaTeX sources locally, install a modern TeX distribution such as:

- TeX Live
- MiKTeX
- MacTeX

The poster should be compiled with LuaLaTeX because it uses `fontspec`.
The report can be compiled with a standard LaTeX workflow.

### Compile the report

From the repository root:

```bash
cd Report
latexmk -pdf main.tex
```

If `latexmk` is unavailable, use:

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

### Compile the poster

From the repository root:

```bash
cd Poster
make main
```

On systems without `make`, run:

```bash
latexmk -pdflatex="lualatex -interaction nonstopmode" -pdf poster.tex
```

## Notes on Figures and Generated Artifacts

The LaTeX files reference figures produced by the experiment pipeline. If a
figure directory is missing locally, regenerate or copy the final figures from
the main project repository:

[mina-mtb/Sarcasm-Detection](https://github.com/mina-mtb/Sarcasm-Detection)

The article repository is focused on the written research artifacts, while the
main project repository is the source of the data-processing, training,
evaluation, and figure-generation workflow.

## Dataset

The experiments are based on the SARC Reddit sarcasm dataset. The report cites
the dataset source and related literature in `Report/biblio-TIF360-FYM360.bib`.

The project treats sarcasm detection as a balanced binary classification task:

- label `1`: sarcastic reply;
- label `0`: non-sarcastic reply;
- target input: Reddit reply;
- context input: parent comment.

## Academic Context

This work was completed as part of the **Advanced Machine Learning with Neural
Networks** course. The report and poster present the final research output for
the project.

## Author

**Mina Tahmasebi Berjouei**

## Links

- Article repository: [mina-mtb/Sarcasm_Detection_Article](https://github.com/mina-mtb/Sarcasm_Detection_Article)
- Project repository: [mina-mtb/Sarcasm-Detection](https://github.com/mina-mtb/Sarcasm-Detection)
- SARC dataset reference: [A Large Self-Annotated Corpus for Sarcasm](https://aclanthology.org/L18-1102/)
