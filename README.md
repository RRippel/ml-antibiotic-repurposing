# Repurposing the Familiar: ML-Guided Search for Antibiotics in FDA-Approved Drugs

## Overview
The global rise of antimicrobial resistance (AMR) demands accelerated drug discovery pipelines. This project bridges organic chemistry and machine learning by exploring a data-driven framework for antibiotic discovery through drug repurposing. By evaluating structural and physicochemical similarities, this project identifies hidden antibiotic potential within a curated set of FDA-approved non-antibiotic compounds.

## Dataset
*   **Source:** ChEMBL database, filtered for FDA-approved drugs targeting *Escherichia coli*.
*   **Classes:** 756 known FDA-approved antibiotics and 1,506 FDA-approved non-antibiotics.
*   **Curation:** Removed salts, diagnostic aids, supplements, and isolated amino acids to ensure a focus on bioactive, drug-like small molecules.

## Methodology
This project utilizes a hybrid unsupervised and supervised machine learning approach to navigate the chemical space without relying on highly variable Minimum Inhibitory Concentration (MIC) data.

1.  **Feature Engineering:** 
    *   Calculated global physicochemical descriptors (logP, molecular weight, TPSA, H-bond donors/acceptors) using **RDKit**.
    *   Applied SMARTS pattern matching to create binary indicators for 14 key functional groups.
    *   Generated Extended Connectivity Fingerprints (ECFP4, 1024 bits) to capture detailed substructural motifs.
2.  **Dimensionality Reduction & Chemical Space Exploration:** 
    *   Standardized features and projected the chemical space into two dimensions using **UMAP**, revealing distinct topological clustering between antibiotics and non-antibiotics.
3.  **Modeling & Candidate Prioritization:**
    *   Trained a **k-Nearest Neighbors (k-NN)** classifier on the UMAP-embedded space to predict the probability of a molecule being "antibiotic-like."
    *   Computed Tanimoto distances on ECFP4 vectors and applied **DBSCAN clustering** to group molecules by substructural coherence.
    *   Devised a hybrid scoring system (80% k-NN probability, 20% DBSCAN cluster membership) to rank candidates.

## Key Results
The pipeline successfully identified four FDA-approved non-antibiotic compounds with a >80% structural and physicochemical probability of behaving like antibiotics:
*   **Metaxalone** (Muscle relaxant) - 93% probability
*   **Gabapentin enacarbil** (Restless legs syndrome) - 87% probability
*   **Primaquine** (Antimalarial) - 87% probability
*   **Lorcaserin** (Weight-loss) - 87% probability

Metaxalone was also highly ranked by the hybrid scoring system, validating its position within a dense, structurally coherent antibiotic-like cluster.
