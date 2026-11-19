# insulin-conservation-12-species comparing the functional chains of insulin with the C-peptide across 12 animals.
# Cross-Species Conservation of Insulin

Comparing the functional chains of insulin with the C-peptide across 12 animals.

**Olivia Aghamie** — BIOL 5340 Bioinformatics, Prof. Jeff Demuth, UTA — Fall 2026
**Student ID:** 1002095139

## Question

How similar is insulin to the human sequence across 11 animals, and are the A and B
chains of the mature hormone more conserved than the C-peptide that is removed when
insulin is made?

## Background

Human insulin is made as a 110-amino-acid precursor. The cell cuts it into four parts:
signal peptide (positions 1–24), B chain (25–54), C-peptide (57–87) and A chain (90–110).
Two disulfide bonds connect the A and B chains, and a third sits inside the A chain. The
joined A and B chains are the 51-amino-acid mature hormone. The C-peptide is removed when
the mature hormone forms. This project measures how similar each region is to human in
11 other animals.

## Repository contents

| File | What it is |
| --- | --- |
| `insulin_conservation.ipynb` | The analysis notebook. Runs start to finish in Google Colab. |
| `insulin_12_animals.fasta` | The 12 sequences as downloaded from UniProt on 2026-11-09. Not edited. |
| `insulin_aligned.fasta` | The MAFFT alignment of the 12 sequences. |
| `insulin_muscle.fasta` | The same 12 sequences aligned with MUSCLE, for the second-aligner check. |
| `results.csv` | Percent identity to human for each animal in each region. |
| `figure1_paired_plot.png` | Figure 1: mature hormone vs C-peptide identity for each animal. |
| `figure2_heatmap.png` | Figure 2: identity to human for every animal and region. |
| `figure3_positions.png` | Figure 3: number of animals differing from human at each of 106 scored positions. |
| `ai_usage.md` | Log of AI assistance and how each output was checked. |
| `README.md` | This file. |

## Data

Twelve reviewed insulin precursor sequences from UniProtKB/Swiss-Prot, downloaded by
accession through the UniProt REST API on 2026-11-09.

| Species | Accession | Species | Accession |
| --- | --- | --- | --- |
| Human | P01308 | Cat | P06306 |
| Chimpanzee | P30410 | Rabbit | P01311 |
| Pig | P01315 | Mouse (Ins2) | P01326 |
| Cow | P01317 | Guinea pig | P01329 |
| Sheep | P01318 | Chicken | P67970 |
| Dog | P01321 | Zebrafish | O73727 |

## How to run it

1. Open `insulin_conservation.ipynb` in Google Colab.
2. Choose Runtime → Run all. The first code cell downloads the sequences, so no data file
   is needed to start.
3. MAFFT and MUSCLE are installed inside the notebook with `apt-get`.
4. The notebook writes the FASTA files, `results.csv` and the three figures.

## How identity is measured

Alignment inserts gaps, so an alignment column number is not a human residue number. The
notebook builds a lookup table from human residue number to alignment column and reads
every region through it. Percent identity is the number of human positions where the
animal has the same amino acid, divided by the number of scored human positions (24, 30,
31 and 21 for the four regions; 51 for the mature hormone). A gap in the animal counts as
a mismatch. Columns where human has a gap are not scored. Positions 55–56 and 88–89 are
cutting sites and are not scored.

## Checks

1. **Known answer.** Pig differs from human at B30 and cow at B30, A8 and A10, matching
   Yang et al. (2025). Passed.
2. **Cysteines.** The six cysteines that anchor the three disulfide bonds are identical in
   all 12 species. Passed.
3. **Second aligner.** MUSCLE gave the same mature-hormone percentages as MAFFT for every
   animal. The strict check (the same percentage everywhere) did not pass: the C-peptide
   differs for chicken (22.6% vs 19.4%) and zebrafish (16.1% vs 9.7%). The main result is
   the same with both programs.
4. **Gap rule.** Leaving out animal gaps keeps the main result (9 of 11 animals).

## Main result

The mature hormone is more similar to human than the C-peptide in 9 of 11 animals.
Chimpanzee ties at 100%. Guinea pig is the one reversal (64.7% mature hormone, 71.0%
C-peptide).

## Software

Google Colab; Python 3.13.18; requests 2.32.4; pandas 2.2.3; Matplotlib 3.10.0;
MAFFT 7.505; MUSCLE 5.2. Versions are printed in the notebook.

## References

- Edgar, R. C. (2022). Muscle5: High-accuracy alignment ensembles enable unbiased
  assessments of sequence homology and phylogeny. *Nature Communications, 13*, 6968.
- Katoh, K., & Standley, D. M. (2013). MAFFT multiple sequence alignment software
  version 7. *Molecular Biology and Evolution, 30*(4), 772–780.
- Opazo, J. C., Palma, R. E., Melo, F., & Lessa, E. P. (2005). Adaptive evolution of the
  insulin gene in caviomorph rodents. *Molecular Biology and Evolution, 22*(5), 1290–1298.
- The UniProt Consortium. (2025). UniProt: The Universal Protein Knowledgebase in 2025.
  *Nucleic Acids Research, 53*(D1), D609–D617.
- Vinther, T. N., et al. (2013). Insulin analog with additional disulfide bond has
  increased stability and preserved activity. *Protein Science, 22*(3), 296–305.
- Ward, C. W., & Lawrence, M. C. (2011). Landmarks in insulin research. *Frontiers in
  Endocrinology, 2*, 76.
- Yang, Y., et al. (2025). Impact of structure and formulation changes on the function of
  insulin products. *Frontiers in Endocrinology, 16*, 1601119.
