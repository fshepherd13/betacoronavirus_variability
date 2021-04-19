# sarscov2-variability

## Purpose
This repo contains code for building a Nextstrain spike or nucleocapsid-specific phylogeny for a wider range of betacoronaviruses including SARS-CoV-2. It uses code forked from the [Bedford lab](https://github.com/blab/beta-cov). Most of the modifications for my build were performed in Geneious, which mainly involved organizing the sequence data into spike and nucleocapsid genes.

## Details on preparing sequence data

### 1. Preparing betacoronavirus sequences

Sequence data was retrieved from genbank by searching for "betacoronavirus NOT 'SARS-CoV-2'", in order to exclude novel coronavirus sequences which make up a huge proportion of the betacoronaviruses currently deposited in NCBI. The resulting ~1600 sequences were downloaded in full Genbank format (which includes gene annotations) and manually trimmed down to the open reading frames for the spike and nucleocapsid genes. The files were exported in .csv format, first column containing the strain accession number, and second column containing the nucleotide gene sequence. 

Since Nextstrain needs metadata associated with each sequence, and metadata is not downloaded so easily from Genbank, I used a [fasta file from the original Bedford lab repo](https://github.com/blab/beta-cov/blob/master/data/coronavirus.fasta) which contains metadata within the sequence name field. The reason I didn't use this file directly is because I needed to access the Genbank annotations in order to perform the correct trimming. 

I extracted the sequence names using:
`grep -e ">" coronavirus.fasta > seq_names.csv`

The data was wrangled a bit in excel a bit to place a column with the accession number (the third field separated by "|" characters), followed by the full sequence name. This file was saved as a csv file. An example of the first couple of lines:

|accession  |name |
|-----------|-----|
|AB257344   |Frankfurt_1\|coronavirus\|AB257344\|2003-XX-XX\|?\|na\|?\|?\|genbank\|genome\|?\|?\|?\|?\|?\|unknown\|Severe_acute_respiratory_syndrome_related_coronavirus|
|AB354579   |Kakegawa\|coronavirus\|AB354579\|?\|japan_korea\|japan\|japan\|japan\|genbank\|genome\|?\|?\|?\|?\|?\|unknown\|Betacoronavirus_1|

### 2. Editing betacoronavirus sequence names to contain metadata
Run the R script `merge_seq_names_with_metadata.R` 

### 3. Retrieving gene-specific sequences of SARS-CoV-2
This build aims to compare betacoronaviruses with a small subset of SARS-CoV-2 sequences. I used alignments that are masked to either the spike or nucleocapsid created from a Nextstrain build [fshepherd13/ncov](https://github.com/fshepherd13/ncov). 

### (readme still in progress)
