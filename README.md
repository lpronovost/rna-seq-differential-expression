# RNA-seq Differential Expression Analysis

RNA-seq differential expression analysis of the Bottomly dataset, comparing C57BL/6J and DBA/2J mouse strains. Pipeline includes EDA, voom normalization, limma-based testing, and gene ontology enrichment with goseq.

---

## Overview

This project walks through a complete RNA-seq analysis pipeline using the [Bottomly dataset](http://bowtie-bio.sourceforge.net/recount/), a well-established benchmark dataset comparing two inbred mouse strains across multiple sequencing lanes. The analysis is implemented in R using Bioconductor packages and is fully reproducible from source.

## Pipeline

1. **Exploratory Data Analysis** — raw count distributions, library size assessment, and surrogate variable analysis (SVA) to check for technical confounding
2. **Normalization** — TMM normalization and voom transformation via `edgeR` + `limma`, motivated by visible library size variability in EDA
3. **Differential Expression** — linear modeling with `limma`, empirical Bayes shrinkage, and Benjamini-Hochberg FDR correction
4. **GO Enrichment** — gene ontology enrichment with `goseq`, correcting for gene-length bias via a probability weighting function
5. **Sensitivity Analysis** — lane-adjusted model to assess the impact of sequencing lane as a batch effect

## Data

The Bottomly dataset is loaded directly from the ReCount project server — no local data files are required. The dataset contains RNA-seq counts from 21 mouse samples (C57BL/6J and DBA/2J strains) aligned to the mm9 reference genome using Ensembl gene IDs.

## Requirements

The following R packages are required:

- `limma`
- `edgeR`
- `goseq`
- `sva`
- `Biobase`
- `org.Mm.eg.db`

Install via Bioconductor:

```r
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("limma", "edgeR", "goseq", "sva", "Biobase", "org.Mm.eg.db"))
```

## Usage

Open `Quiz_4_Analysis.Rmd` in RStudio and knit to HTML. All data is loaded automatically from source — no additional setup is needed.

## Results

Differential expression analysis identified hundreds of genes at a 5% FDR threshold, consistent with independent benchmarking of this dataset using comparable methods. GO enrichment revealed biologically interpretable terms that were robust across both the unadjusted and lane-adjusted models.

## References

Bottomly, D. et al. (2011). Evaluating gene expression in C57BL/6J and DBA/2J mouse striatum using RNA-Seq and microarray platforms. *PLOS ONE*.

