# Lowry Landfill bioreactor microbial communities: 16S rRNA data analysis 

Code used to process and analyze 16S rRNA data from support media collected from a bioreactor in the treatment plant of the Lowry Landfill Superfund Site (Colorado, USA).

## Description

This repository contains scripts and R markdown files and output files from certain 16S analyses.

### Scripts

* **PAPER--Lowry-16S-1-QIIME2** -- Initial data processing with QIIME2. Steps include: Demultiplexing, denoising and generating representative sequences with DADA2, searching representative sequences (ASVs) against a BLAST nr database, filtering reads and unwanted ASVs, assigning taxonomy, generating phylogenetic trees. Four files were imported from this script into R for further analysis (analysis shown in PAPER--Lowry-16S-2-R.html).
* **PAPER--Lowry-16S-2-R.html** -- Further analysis and plot generation in R. Steps include: obtaining relative abundances at the phylum and family levels, alpha diversity (i.e., Observed Richness, Shannon, Simpson, Faith Phylogenetic Diversity metrics), beta diversity (unweighted and weighted non-metric multidimensional scaling analyses), taxonomy bar plots at the phylum and family levels.

### Output files

* **dna-sequences.fasta** -- Representative nucleotide sequences for the filtered 16S dataset.
* **min5300_noChlorMitoUnassigned_fam_FALSE_REL.tsv** -- Relative abundance values down to the family level for the filtered 16S dataset.
* **min5300_noChlorMitoUnassigned_phy_REL.tsv** -- Relative abundance values down to the phylum level for the filtered 16S dataset.
* **table-with-taxonomy.biom**  -- ASV table (BIOM format) for the filtered 16S dataset.
* **table-with-taxonomy.txt** -- ASV table (readable text format) for the filtered 16S dataset.

## Authors

Jessie Romero (jessieromero418@gmail.com) 

## Acknowledgments

* Thanks to the Lowry Trust for site access and permission to sample bioreactors.
* Thanks to Parsons Engineering tours of the treatment plant, relaying site history including updates 
on remediation efforts, sampling assistance, and providing chemistry data from the treatment 
plant.
* Thanks to the students of General Biology (BIOL2021) at the University of Colorado Denver for help with 16S rRNA library preparation.
* Thanks to the lab of Dr. Daniel Frank at the University of Colorado Anschutz Medical Campus for assistance with MiSeq sequencing. 
* Thanks to Dr. Chris Miller at the University of Colorado Denver for access to the miller-lab server at the University of Colorado Denver.
* 16S R analyses based [Orchestrating Microbiome Analysis (OMA)](https://microbiome.github.io/OMA/)
