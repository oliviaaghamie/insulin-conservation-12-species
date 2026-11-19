 # Cross-Species Conservation of Insulin: Comparing the functional chains of insulin with the C-peptide across 12 animals.

## Research question

Across 11 animals, are the A and B chains together more similar to human than the C-peptide is?

## What this project looks at

I wanted to compare the parts that remain in mature insulin with the C-peptide that is removed.

Human insulin starts as a 110-amino-acid precursor. The signal peptide and C-peptide are removed during processing, leaving the A and B chains as the 51-amino-acid mature hormone. I compare these regions separately instead of treating the whole precursor as one piece. The region boundaries come from the [human UniProt entry, P01308](https://www.uniprot.org/uniprotkb/P01308/entry).

I used MAFFT to line up the sequences and repeated the alignment with MUSCLE to check whether the choice of program changed the result (Katoh & Standley, 2013; Edgar, 2022).

## Files in this repository

| File | What it contains |
| --- | --- |
| `Insulin_Conservation_Across_12_Species.ipynb` | My analysis notebook, with the code, explanations, checks, and saved results. |
| `insulin_12_animals.fasta` | The 12 insulin sequences from UniProt. The amino-acid sequences are unchanged, but the headers use the animal name and accession. |
| `insulin_aligned.fasta` | The sequences aligned with MAFFT. |
| `insulin_muscle.fasta` | The sequences aligned with MUSCLE. |
| `results.csv` | The MAFFT results table, including percent identity to human for each region and the mature hormone, plus mature-hormone difference counts. |
| `figure1_paired_plot.png` | A comparison of mature-hormone and C-peptide identity for each animal. |
| `figure2_heatmap.png` | A heatmap showing identity to human across the four regions. |
| `figure3_positions.png` | A plot showing how many of the 11 animals differ from human at each of the 106 scored positions. |
| `ai_usage.md` | How I used AI, what I changed, and how I checked its suggestions. |
| `README.md` | This guide to the project and its files. |

## Data

I used 12 reviewed insulin precursor sequences from UniProtKB/Swiss-Prot, a public protein database (The UniProt Consortium, 2025). I downloaded them on November 9, 2026. The sequences are stored in FASTA format. Human insulin is the reference, so the results compare the other 11 animals with human.

| Species | UniProt accession |
| --- | --- |
| Human | P01308 |
| Chimpanzee | P30410 |
| Pig | P01315 |
| Cow | P01317 |
| Sheep | P01318 |
| Dog | P01321 |
| Cat | P06306 |
| Rabbit | P01311 |
| Mouse (Ins2) | P01326 |
| Guinea pig | P01329 |
| Chicken | P67970 |
| Zebrafish | O73727 |

## How to run the notebook

1. Open `insulin_conservation.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Connect to a Python runtime and select **Runtime > Run all**.
3. Let the cells run in order. The notebook downloads the sequences and installs MAFFT and MUSCLE.
4. Read the tables, checks, and figures below the code. The notebook also saves the FASTA files, `results.csv`, and the three figure files in the Colab Files panel.

## How I measured similarity

I used **percent identity**, which is the percentage of scored positions with the same amino acid as human.

The comparisons use these positions in the original human sequence:

| Region | Human positions | Positions scored |
| --- | --- | --- |
| Signal peptide | 1–24 | 24 |
| B chain | 25–54 | 30 |
| C-peptide | 57–87 | 31 |
| A chain | 90–110 | 21 |
| Mature hormone, A and B chains together | 25–54 and 90–110 | 51 |

Alignment adds gaps, so the numbers in an aligned sequence can shift. The code tracks each original human position through each alignment before comparing the regions.

**Percent identity = matching positions / scored positions × 100**

For the main calculation:

- A gap in an animal's sequence counts as a difference.
- Columns where the human sequence has a gap are left out.
- Human positions 55–56 and 88–89 are left out because they are processing-site residues outside the four regions.

This gives 106 scored positions across the precursor. I also repeated the calculation without animal gaps to see whether that choice changed the main result.

## Checks I used

1. **Pig and cow comparison:** The code found one difference between pig and human mature insulin, at B30. It found three for cow, at B30, A8, and A10. These counts and positions match the published comparison in Yang et al. (2025).
2. **Cysteine positions:** All six cysteines involved in the three disulfide bonds matched the human sequence in all 12 species.
3. **MAFFT and MUSCLE comparison:** Both programs gave the same mature-hormone percentages. They did not agree everywhere. For C-peptide, MAFFT gave 22.6% for chicken and 16.1% for zebrafish, while MUSCLE gave 19.4% and 9.7%. The main result stayed the same.
4. **Gap comparison:** Leaving out animal gaps also kept the main result at 9 of 11 animals.

## Main result

The mature hormone was more similar to human than the C-peptide in **9 of the 11 animals**.

- Chimpanzee was a tie: both were 100% identical to human.
- Guinea pig showed the opposite pattern: 64.7% identity for the mature hormone and 71.0% for C-peptide. Guinea pig insulin has been described as unusually divergent before (Opazo et al., 2005).

My prediction was supported for most animals, but not all. These results describe sequence similarity in the selected animals. I did not test how well their insulin binds to the human receptor or works as a treatment.

## Software

These are the versions shown in the saved notebook run:

| Software | Version |
| --- | --- |
| Python | 3.13.18 |
| requests | 2.32.4 |
| pandas | 2.2.3 |
| Matplotlib | 3.10.0 |
| MAFFT | 7.505 |
| MUSCLE | 5.2 |

The notebook prints the software versions so they can be checked again after a rerun. 

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
