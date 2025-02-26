# Lowry Landfill bioreactor microbial communities: Metagenomic shotgun sequencing data analysis 

Code used to process and analyze shotgun sequencing data from support media collected from a bioreactor in the treatment plant of the Lowry Landfill Superfund Site (Colorado, USA).

## Description

This repository contains scripts used for shotgun sequencing data analyses. 

Because certain scripts were run on another server (i.e., the Alderaan cluster), these required singularity files to provide the necessary software programs. Definition files to build singularities are at: Shotgun/singularities

### Scripts
#### Initial data processing and analyses
* **Lowry-Shotgun-1-Trimming (rqcfilter2.sh)**, singularity: *bio-lowry-assembly.sif* -- Interleave raw, pre-trimmed Read 1 and Read 2 files (reformat.sh), trim interleaved reads file (rqcfilter2.sh). 
* **Lowry-Shotgun-2-TrimmingQuality (fastqc, fastqp, multiqc)**, singularity: *bio-lowry-assembly.sif* -- Assess trimmed reads quality (fastqc, fastqp), aggregate trimmed reads quality information from fastqc for all samples (multiqc).
* **Lowry-Shotgun-3-Assembly (megahit, quast)**, singularity: *bio-lowry-assembly.sif* -- Deinterleave reads (reformat.sh), assemble reads into contigs (megahit), get assembly statistics (quast).
* **Lowry-Shotgun-4-MapBin (bbmap, samtools sort)**, singularity: *bio-lowry-map-bin.sif* -- Map all sample reads to all sample contigs (bbmap), sort reads (samtools sort).
* **Lowry-Shotgun-5-MapBin2 (reformat.sh, samtools calmd, jgi_summarize_bam_contig_depths)**, singularity: *bio-lowry-map-bin.2022-03-14.sif* -- Trim contig information in bam files (reformat.sh), generate MD tags for bam files (samtools calmd), calculate coverage (jgi_summarize_bam_contig_depths).
* **Lowry-Shotgun-6-MapBin3 (metabat2, runMetaBat.sh)**, singularity: *bio-lowry-map-bin.2022-03-14.sif* -- Bin mapped reads (metabat2/runMetaBat.sh).
* **Lowry-Shotgun-7-BinQualityTaxonomy (checkm, gtdbtk)**, singularity: *bio-lowry-bin-qual-tax.sif* -- Assess bin quality (checkm), assign taxonomy to bins (gtdbtk).
* **Lowry-Shotgun-8-Prodigal (prodigal)** -- Predict protein and gene sequences (prodigal).
* **Lowry-Shotgun-9-BLAST (blastp)** -- BLAST to search for 39 soluble di-iron monooxygenase (SDIMO) alpha hydroxylase protein query sequences from Goff & Hug (2022) in prodigal-predicted sample protein sequences (blastp).
* **Lowry-Shotgun-10-CoverM**, singularity: *bio-lowry-genes-tree.sif* -- Estimate gene (contig) abundances (coverm).

#### All SDIMOs
* **Lowry-Shotgun-11-allSDIMOs-BLASTFilter (filterbyname.sh)** -- Filter out all BLASTp hits (i.e., all SDIMOs) into a new file (filterbyname.sh).
* **Lowry-Shotgun-11.1-allSDIMOs-Align (mafft)** -- Align all SDIMOs with all SDIMO query sequences (mafft).

#### Tier 1
* **Lowry-Shotgun-12-Tier1-BLASTFilter (filterbyname.sh)** -- Filter out all Tier 1 SDIMOs (i.e., BLASTp hits with: minimum 90% amino acid identity with a query sequence, minimum 125 amino acid alignment length, minimum 60% query coverage) into a new file (filterbyname.sh).
* **Lowry-Shotgun-12.1-Tier1-Align (mafft)** -- Align all Tier 1 SDIMOs with all SDIMO query sequences (mafft).
* **Lowry-Shotgun-12.1.1-Tier1-Tree (FastTree)** -- Build a phylogenetic tree with the alignment of all Tier 1 SDIMOs and all SDIMO query sequences (FastTree).
##### *Tier 1, non-redundant contigs*
* **Lowry-Shotgun-13-Tier1-NonredundantContigs (filterbyname.sh, CD HIT EST)** -- Obtain all Tier 1 contig nucleotide sequences (filterbyname), obtain a non-redundant set of Tier 1 contigs by clustering these (CD HIT EST).
* **Lowry-Shotgun-13.1-Tier1-NonredundantContigs-SDIMOs (filterbyname.sh, mafft, FastTree)** -- Obtain SDIMO protein and nucleotide sequences from non-redundant Tier 1 contigs (filterbyname.sh), align those SDIMO proteins with all SDIMO query sequences (mafft), build a phylogenetic tree from this alignment (FastTree).
* **Lowry-Shotgun-13.2-Tier1-NonredundantContigs-SDIMOs-Clustering (CD HIT, CD HIT EST)** -- Cluster SDIMO protein (CD HIT) and nucleotide sequences (CD HIT EST) from non-redundant Tier 1 contigs at various percent identity levels.
* **Lowry-Shotgun-13.3-Tier1-NonredundantContigs-SDIMOs-ManualClustering (mafft, FastTree)** -- Manual clustering of SDIMO proteins from non-redundant Tier 1 contigs, align those SDIMO proteins with all SDIMO query sequences (mafft), build a phylogenetic tree from this alignment (FastTree).

#### Tier 2
* **Lowry-Shotgun-14-Tier2-BLASTFilter (filterbyname.sh)** -- Filter out all Tier 2 SDIMOs (i.e., BLASTp hits with: 50-90% amino acid identity with a query sequence, minimum 125 amino acid alignment length, minimum 60% query coverage) into a new file (filterbyname.sh).
##### *Tier 2, non-redundant contigs*
* **Lowry-Shotgun-14.1-Tier2-NonredundantContigs (filterbyname.sh, CD HIT EST)** -- Obtain all Tier 2 contig nucleotide sequences (filterbyname), obtain a non-redundant set of Tier 2 contigs by clustering these (CD HIT EST).
* **Lowry-Shotgun-14.2-Tier2-NonredundantContigs-SDIMOs (filterbyname.sh, mafft, FastTree)** -- Obtain SDIMO protein and nucleotide sequences from non-redundant Tier 2 contigs (filterbyname.sh), align those SDIMO proteins with all SDIMO query sequences (mafft), build a phylogenetic tree from this alignment (FastTree).

#### Additional data processing and analyses
* **Lowry-Shotgun-15-MITEs (MITETracker)** -- Identify candidate miniature inverted-repeat transposable elements (MITEs) in sequences (MITETracker). 
* **Lowry-Shotgun-16-GFF (prodigal)** -- Generate a GFF file of Tier 1 contigs to upload to KBase for gene annotation (prodigal).

## Authors

Jessie Romero (jessieromero418@gmail.com) 

## Acknowledgments

* Thanks to the Lowry Trust for site access and permission to sample bioreactors.
* Thanks to Parsons Engineering tours of the treatment plant, relaying site history including updates 
on remediation efforts, sampling assistance, and providing chemistry data from the treatment 
plant.
* Thanks to Dr. Jan Mandel at the University of Colorado Denver for access to the Alderaan cluster from the Center for Computational Mathematics at the University of Colorado Denver (supported by National Science Foundation award OAC-2019089).
* Thanks to Dr. Chris Miller at the University of Colorado Denver for access to the miller-lab server at the University of Colorado Denver.
* 39 SDIMO query sequences obtained from Goff & Hug (2022): Goff, K. L., & Hug, L. A. (2022). Environmental Potential for Microbial 1,4-Dioxane 
Degradation Is Sparse despite Mobile Elements Playing a Role in Trait Distribution. Applied and 
Environmental Microbiology, 88(7), e02091-02021. https://doi.org/doi:10.1128/aem.02091-21
