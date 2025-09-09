# Morphological-Semantic Complexity Analysis

Cross-linguistic study testing the Low-Entropy Conjecture across Turkish, Russian, and English using computational morphology and semantic network analysis.

## Overview

This project investigates whether languages show systematic trade-offs between morphological complexity and semantic organization. We test three hypotheses on Russian, English and Turkish:

- H1 (Trade-off): As a language’s inflectional system gets richer (more forms per lemma or higher morphological complexity), the semantic network density decreases.
- H2 (Compensation): When a language has a higher I-complexity/entropy, meaning its morphology is less predictable, the semantic network shows higher clustering.
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
The contents of the `data/` folder are too large to push them to this repo, but can be reproduced using the notebooks. 
Here is how to use them:

```bash
git clone <repository-url>
cd morphological-semantic-complexity

pip install -r requirements.txt

# Download corpora (see Data Sources above)
# Run notebooks sequentially (01 -> 02 -> 03 -> 04)
```

## Project Structure

```yaml
morphological-semantic-complexity/
  notebooks/
    01_data_preprocessing.ipynb
    02_morphological_baselines.ipynb
    03_complexity_networks.ipynb
    04_correlation_analysis.ipynb
  outputs/
    figures/
      corpus_statistics.png
      enhanced_semantic_network_analysis.png
      ttr_curves.png
  results/
    phase1/
    phase2/
    phase3/
    .gitignore
  LICENSE
  README.md
  requirements.txt
  pearl_script.txt
```

# Research flow

## Stage 1: Data Preprocessing
At this stage we extracted and cleaned Wikipedia articles for English, Russian and Turkish (350k articles/language)  
With an equal number of articles for each langauge we got the following token counts EN: 369M tokens, RU: 164M tokens, TR: 76M tokens  
We then saved the clean corpora and Type-Token Ratios for each: (EN: 0.215, RU: 0.307, TR: 0.309).

---

## Stage 2: Baseline Analysis
We built semantic networks of surface forms for each langague using cosine similarity treshold
We took top 1000 most frequent words + similarity > 0.5  
We ended up with large densities and avg degrees for English and Turkish EN 0.149, RU 0.710, TR 0.750; Avg degree: EN 148, RU 709, TR 749  

---

## Stage 3: Phase 2 - Enhanced Analysis
Here we took a more principled approach and used 10000 lemmas instead of 1000 surface forms and built kNN graphs with k=15. We also measured morphological complexity with better established metrics such as E/I-complexity.

### Key Metrics
| Language | E-complexity | I-complexity | Density | Clustering |
|----------|-------------|--------------|---------|------------|
| English  | 1.34        | 3.45         | 0.0023  | 0.298      |
| Russian  | 2.21        | 6.66         | 0.0024  | 0.349      |
| Turkish  | 2.40        | 5.01         | 0.0026  | 0.306      |

This gave us much more realistic measurements.

---

## Stage 4: Hypothesis Testing
After obtaining reliable metrics we could proceed with the hypotheses testing. Here is what we found:

- **H1 (Trade-off)**: ρ = +1.000, p < 0.001 -> **rejected** (positive not negative!)
- **H2 (Compensation)**: ρ = +1.000, p < 0.001 -> **supprted** (**I-complexity predicts clustering** -- our main finding)
- **H3 (Dimensionality)**: ρ = +0.500, p = 0.667 -> **weak** (inconclusive)

---

## Citation
Research conducted for Data Science for Linguists course, University of Tübingen, Summer 2025.

## References
* Ackerman, F., & Malouf, R. (2013). Morphological organization: The low entropy conjecture.
* Cotterell et al. (2019). On the Complexity and Typology of Inflectional Morphological Systems.
