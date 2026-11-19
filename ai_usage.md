# AI Use Log

**Project:** Cross-Species Conservation of Insulin  
**Student:** Olivia Aghamie  
**Course:** BIOL 5340 Bioinformatics, Fall 2026

I used ChatGPT, Gemini, and Claude on this project. This file records what I asked for, what each tool produced, what I changed, and how I checked the work.

## Tools and assistance

- **Claude & Gemini:** Helped propose the insulin comparison and assemble the accession list.  They wrote the first analysis code and draft report, helped revise notebook explanations, and wrote the Figure 2 formatting change.
- **ChatGPT:** Helped review the notebook outputs and identify problems.

## 2026-11-08: Choosing a project

**Asked for:** Help finding a topic that used tools we covered in class.

**AI produced:** Claude and Gemini proposed comparing insulin across species, region by region, and assembled the list of 12 UniProt accessions.

**I changed:** I chose the project and decided its scope.

**I checked it by:** Confirming that each accession was a reviewed Swiss-Prot entry for the species listed.

## 2026-11-09: Downloading the sequences

**Asked for:** Help writing a code cell to download 12 insulin sequences from UniProt by accession.

**AI produced:** A Python loop using `requests` that writes the sequences to one FASTA file.

**I changed:** Nothing in the code.

**I checked it by:** Reading the output for all 12 entries and confirming that each sequence was a full precursor, 105–110 amino acids long, rather than the 51-amino-acid mature hormone.

## 2026-11-16: Alignment and measurement code

**Asked for:** Code to align the sequences with MAFFT, build the human-position lookup table, calculate percent identity for each region, and run the known-answer and cysteine checks.

**AI produced:** The Step 1 and Step 2 code cells.

**I changed:** The headers, filenames, dictionary names, and similar labels.

**I checked it by:** Running the code in Colab and reading the output. The lookup table returned the expected human B-chain and A-chain sequences. Pig differed from human at one mature-insulin position and cow at three, matching Yang et al. (2025). All six checked cysteines matched in all 12 species.

## 2026-11-16: Second aligner and follow-up checks

**Asked for:** Code to repeat the analysis with MUSCLE, name the differing positions, compare the guinea pig changes with receptor-binding residues, recalculate identity without animal gaps, and make Figures 2 and 3.

**AI produced:** The Step 4 and Step 5 code cells.

**I checked it by:** Running every cell and reading the outputs. MUSCLE gave the same mature-hormone percentages as MAFFT. The C-peptide percentages differed for chicken and zebrafish, so the strict agreement check did not pass. I reported that difference. The named pig and cow differences matched Yang et al. (2025). Leaving out animal gaps kept the result that mature insulin had higher identity to human than the C-peptide in 9 of the 11 other animals.

## 2026-11-16: Draft report and review

**Asked for:** Help reviewing the notebook and report against the rubric.

**AI produced:** A review listing problems from ChatGPT. I also reviewed the notebook and report against the rubric.

**What was changed:**

- The bond description was wrong. I corrected it to explain that two disulfide bonds connect the chains and the third is within the A chain.
- “Discarded” was the wrong word for the C-peptide. I changed it to “removed.”
- Some sentences claimed a mechanism, an evolutionary rate, or that errors had been ruled out. My analysis compares sequences only, so I removed those claims.
- The report said all checks passed. The strict aligner agreement check did not pass, so I updated the report to reflect that.
- Figure 3 covers 106 scored positions, not 110. I corrected that description.
- I had cited the 2004 MUSCLE paper. Since I used MUSCLE 5.2, I changed the citation to the 2022 Muscle5 paper.
- I removed a chance calculation, or p-value, for the guinea pig binding-site result. It was added after seeing the result and assuming that changes were equally likely across the positions being considered. I could not support that assumption.

**I checked it by:** Comparing every number in the report and notebook with my own Colab output. I reran the whole notebook using **Runtime → Run all** and compared the outputs with the report.

## 2026-11-18: Final formatting check of the draft

**What I found:** The Table 2 note was separated from its table, the chimpanzee markers in Figure 1 overlapped, and the Figure 2 numbers were hard to read on dark cells.

**What I changed:** I kept the note with Table 2, added “The chimpanzee markers overlap at 100%” to the Figure 1 caption, and enlarged the Figure 2 labels with white text on dark cells. Claude wrote the Figure 2 code change. I made the same change in my notebook and reran it.

**I checked it by:** Opening the report and confirming that it was still five pages and every figure was readable.

## How I handled AI suggestions

- When an AI tool supplied a numerical value it had not computed, I treated it as a claim to check.
- The guinea pig binding-site comparison was added after I saw the guinea pig result. I report it as an exploratory observation.
  
## How I verified AI output

- **Known answers:** I checked whether the code reproduced the published pig and cow differences (Yang et al., 2025). It found the same positions and changes.
- **Cysteine check:** I checked the six cysteine positions involved in insulin’s disulfide bonds. All six matched across the 12 species in my output.
- **Second program:** I repeated the alignment with MUSCLE and reported where the two programs differed.
- **Gap rule:** I repeated the calculation without animal gaps. The main conclusion stayed the same: mature insulin had higher identity to human than the C-peptide in 9 of the 11 other animals.
- **Analysis results:** I compared the numerical results reported in the notebook and report with my Colab outputs.
- **Sources:** I checked each citation’s title and DOI. I removed claims that the sources or my data could not support.
- **Full rerun:** I reran the notebook from the top using Runtime → Run all after every round of changes.

## Data and responsibility

The protein sequences came from UniProt. The tables and figures came from running the notebook, which includes AI-assisted code. The project uses public reference protein sequences. To prevent bias, Before using the real insulin sequences, I asked Claude to test the position lookup and measurement code on small, made-up alignments with known answers. Claude used these examples to check whether the code mapped positions and calculated identity as expected.
