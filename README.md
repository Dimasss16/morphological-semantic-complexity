# Morphological-Semantic Complexity Analysis

Cross-linguistic study testing the Low-Entropy Conjecture across Turkish, Russian, and English using computational morphology and semantic network analysis.

## Overview

This project investigates whether languages show systematic trade-offs between morphological complexity and semantic organization. We test three hypotheses on Russian, English and Turkish:

- H1 (Trade-off): As a language’s inflectional system gets richer (more forms per lemma or higher morphological complexity), the semantic network density decreases.
- H2 (Compensation): When a langauge has a higher I-complexity/entropy, meaning its morphology is less predictable, the semantic network shows higher clustering.
- H3 (Dimensionality): Languages with more complex morphology need more dimensions to capture semantics, so their embeddings require more principal components to reach the same variance threshold.

## Data Sources

### Wikipedia Corpora (October 2018)
**Required for Stage 1 preprocessing - download separately:**

- **Turkish:** `trwiki-20181001-corpus.xml.bz2` 
- **Russian:** `ruwiki-20181001-corpus.xml.bz2`
- **English:** `enwiki-20181001-corpus.xml.bz2`

Download from: [Linguatools Wikipedia Corpus](https://linguatools.org/tools/corpora/wikipedia-monolingual-corpora/)

Create the following directory structure:
```
data/
└── raw_corpora/
    ├── trwiki-20181001-corpus.xml.bz2
    ├── ruwiki-20181001-corpus.xml.bz2
    └── enwiki-20181001-corpus.xml.bz2
```
The contents of the data/ folder are too large to push them to this repo, but can be reproduced using the notebooks.

## Project Structure

```
morphological_semantic_complexity/
├── data/                 # Raw and processed corpora
├── notebooks/            # Jupyter notebooks for each analysis phase
├── results/              # Outputs from each analysis phase
├── outputs/              # Final figures and reports
├── requirements.txt      # Python dependencies
└── README.md            # This file
```


## Citation

Research conducted for Data Science for Linguists course, University of Tübingen, Summer 2025.
