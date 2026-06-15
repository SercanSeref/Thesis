# Uncovering Trends in Illicit Drug Reporting in Dutch News Media: A Data-Driven Approach

This repository contains the code and supplementary data for the MSc thesis *"Uncovering Trends in Illicit Drug Reporting in Dutch News Media: A Data-Driven Approach"* (Şeref, 2026). The pipeline performs large-scale sentiment analysis and frame detection on a corpus of ~25,000 Dutch newspaper articles from Algemeen Dagblad, De Telegraaf, and de Volkskrant.

## Research Questions

**Core Question: How has Dutch news media reporting on illicit drugs evolved over time in terms of tone, framing, and variation across outlets?**

1. How has the volume and tone of drug-related reporting changed over time?
2. How do different news outlets (Algemeen Dagblad, De Telegraaf, and de Volkskrant) frame or tone drug issues?
3. What framing patterns dominate Dutch media coverage of illicit drugs?

## Repository Structure

```
├── Code/
│   ├── quenteda.rmd                  # R preprocessing: LexisNexis parsing, stopword removal, corpus construction
│   ├── Noise_Inspection.ipynb        # Corpus cleaning, deduplication, artefact stripping
│   ├── BERTopic.ipynb                # Frame detection using BERTopic with NewsBERTje embeddings
│   ├── Sentiment_Analysis.ipynb      # Uniform and aspect-based sentiment classification (mDeBERTa)
│   └── sample_analysis.ipynb         # Exploratory analysis and visualisations
│
├── Supplementary_Data/
│   ├── topic_classifications.xlsx    # Manual frame classification of BERTopic output
│   ├── topics_by_newspaper.csv       # Topic distribution per outlet
│   └── topics_summary.csv            # Topic model output summary
│
├── Output/                           # Generated figures and plots
│
└── Data/                             # Processed data files (see note below)
    ├── df_with_topics.csv            # Topic assignments per article 
    ├── uniform_sentiment_analysis.csv # Sentiment scores per article 
    ├── aspect_sentiment_by_drugclass.csv # ABSA scores per drug class
    └── comparison_sample.csv         # Comparative outlet analysis output
```

## Pipeline Overview

1. **R Preprocessing** (`quenteda.rmd`) — LexisNexis article parsing via `LexisNexisTools`, Dutch stopword removal via `quanteda`, and corpus construction exported to CSV
2. **Noise Inspection** — Quality control, deduplication, and artefact stripping of LexisNexis metadata from raw corpus
2. **BERTopic** — Contextual embeddings via `LoicDL/NewsBERTje-base`, topic modeling with hyperparameter tuning, topics over time, and manual frame interpretation into four categories
3. **Sentiment Analysis** — Zero-shot uniform sentiment classification and aspect-based sentiment analysis (ABSA) by drug class using `MoritzLaurer/mDeBERTa-v3-base-mnli-xnli`
4. **Sample Analysis** — Comparative outlet analysis, visualisations, and statistical testing

## Data Availability

The newspaper articles were retrieved via LexisNexis Academic under the institutional license of JADS. Due to LexisNexis licensing terms, raw article text cannot be publicly shared. The following files are therefore excluded from this repository: corpus_df.csv, corpus_df_cleaned.csv, corpus_df_processed.csv, df_zondertips.csv, paragraphs_processed.csv, and aspect_sentiment_paragraphs.csv.

Processed output files with raw text columns removed are included in the Data/ folder. All supplementary data files are included in full. Raw data is available upon reasonable request, subject to LexisNexis terms.

## Requirements

The pipeline was executed on the TU/e High Performance Computing cluster. Key dependencies include:

**R:**
- `LexisNexisTools`
- `quanteda`
- `dplyr`, `readr`, `lubridate`

**Python:**
- `bertopic`
- `sentence-transformers`
- `transformers`
- `pandas`, `numpy`
- `plotly`
- `scipy`

## Citation

If you use this code, please cite the thesis:

> Seref, S. (2026). *Uncovering Trends in Illicit Drug Reporting in Dutch News Media: A Data-Driven Approach*. MSc Thesis, Jheronimus Academy of Data Science.
