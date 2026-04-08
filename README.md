# PCB 153 Exposure and RNA-Binding Protein Regulation in Differential Splicing Events

This repository contains a complete computational workflow to study how PCB 153 exposure alters RNA-binding protein (RBP) regulation, alternative splicing, and motif positioning in differential splicing events (DASEs).

---

## Project Overview

The project integrates:

- rMATS-based alternative splicing detection  
- Functional enrichment (EnrichR / enrich_omics)  
- Retained intron premature stop codon analysis  
- RBP motif enrichment and localization (RBPBench)  
- Publication-ready visualization  

---

## Workflow

<details>
<summary><b>0_rmats.ipynb</b></summary>

Defines experimental groups (PCB153 vs CTRL)

Prepares BAM file structure

Organizes input metadata

</details>

---

<details>
<summary><b>1_rmats.ipynb</b></summary>

Executes rMATS on STAR-aligned BAM files

Uses GRCh38 annotation (GTF)

Detects:

SE (Skipped exon)

MXE

A5SS / A3SS

RI (Retained intron)

Computes PSI and ΔPSI values

</details>

---

<details>
<summary><b>2_rmats.ipynb</b></summary>

Filters significant splicing events

Applies thresholds:

FDR ≤ 0.05

|ΔPSI| ≥ 0.1

coverage filtering

Generates candidate DASE dataset

</details>

---

<details>
<summary><b>Figure1.ipynb</b></summary>

Summarizes event types (SE, MXE, etc.)

Visualizes global splicing distribution

QC of rMATS output

</details>

---

<details>
<summary><b>DEGS_RBP.ipynb</b></summary>

Loads expression matrix

Load Differential expression analysis results

Filters DEGs RBPs using catRAPID annotation

</details>

---

<details>
<summary><b>rbp-degs-graph.ipynb</b></summary>

Gives visual representation of RBP DEGs.

Plots Volcano Plot with:

log2 fold change

log10 adjusted p-value

RBP genes highlighted in red

</details>

---

<details>
<summary><b>1-RBPBench-rbp-deg-specific.ipynb</b></summary>

Runs motif scanning on DASE sequences

Restricts analysis to 32 DE RBPs

Generates motif hit tables

Prepares input for ENMO and SEARCH modules

</details>

---

<details>
<summary><b>2-parse_rbpbench_output_positive-negative-psi-deg_specific.ipynb</b></summary>

Splits dataset into:

Positive ΔPSI events

Negative ΔPSI events

Runs ENMO enrichment filtering:

Fisher’s exact test

FDR correction

Runs SEARCH mapping:

Locates motifs in genomic coordinates

Produces:

enriched positive PSI dataset

enriched negative PSI dataset

</details>

---

<details>
<summary><b>3-parse_rbp_output-deg_specific.ipynb</b></summary>

Merges positive + negative datasets

Removes duplicates

Validates sequence length distribution

Ensures no bias between:

DASE sequences

background regions

Final dataset creation:
RBP_DEG_specific_final_motif_with_position.xlsx

</details>

---

<details>
<summary><b>4-rbp-plot-deg-specific.ipynb</b></summary>

Splits data into

Positive ΔPSI

Negative ΔPSI

Creates composite labels:

geneSymbol + splicing class

Plots:

X-axis: motif position (upstream / exon / downstream)
Y-axis: GeneClass

Hue: RBP identity

Output figures:

positive_PSI_events.png

negative_PSI_events.png

Aggregates RBP counts

Computes motif positional distribution per RBP

Builds hierarchical visualization:

Inner ring → RBP abundance

Outer ring → motif position distribution

Output:

nested_pie_chart.png

</details>
