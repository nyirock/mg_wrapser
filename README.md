# MG Wrapser



MG Wrapser is used to recruit reads or contigs from metagenomic data using reference datasets. Scripts wrap BLAST queries against the reference(s), process the output, quantify and recruit metagenomic data.

Development version of the tool is available at <https://github.com/nyirock/mg_blast_wrapper>

## Table of Contents

- [Background](#background)
  - [Directory Structure](#directory-structure)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
  - [Standalone](#standalone)
  - [BASH Wrapper](##bash-wrapper)
  - [Examples](#examples)
- [License](#license)


## Background

MG Wrapser is designed to recruit and quantify reads or contigs from metagenomes by mapping them to the referenec(s). Currently only the BLAST similarity feature is supported, while contig recruitment and binning by GC content and k-mer frequencies are in development.

It is possible to alter the stringency criteria for contigs/reads recruitments by changing minimum BLAST e-Value, % or bp of allignment length, % identiy, etc.

Recruited contigs either in fasta or csv format are placed in the results folder of the project directory with suffixes reflecting the order of metagenomes that had been supplied, e.g. \*_mg_0.fasta, \*_mg_1.fasta and so on. By design, the script treats multiple input metagenomes separatlely. However, if several reference files are supplied, they are combined into a single file and a signe database is created. If it is necessary to run software with separate reference files it is suggested to use the script with the supplied BASH Wrapper(see [BASH Wrapper section](#bash-wrapper) for the details).

Currently only fasta formats are supported for both input references and metagenomes. Default output is the recurited metagenomic sequences in fasta format. It is also possible to obtain the results in tab-delimited csv file (or both csv and fasta), that contains target sequences plus allignment features and basic parameters such as GC value, RPKM, etc.

Results summary file is also created in the end of the run. Results contain summary and basic statistic calculations of the run, such as:
- Number, %, RPKM of recruited sequences
- Average recruited sequence lengs plus STD and SEM
- Average recruited sequence GC, STD, SEM
- Average recruited sequence identity, allignment length, etc.

## Directory Structure

If no project name is specified, by default a folder called "output" containing the project files is created in the directory containing the script.
Upon running the scrip the following directory structure is created:

``` 
./ ### foleder containing the python script
  ¦
  --- mg_wrapser_latest.py ### executable file
  ¦
  --- output ### project directory
      ¦
      +-- input_files ### folder containing copied and processed reference files
      ¦  
      +-- blast_db ### folder for the BLAST database
      ¦  
      +-- results ### folder containing results files in .csv, .fasta and .tab formats
      ¦   
      --- results_log.csv ### run summary file
```

## Prerequisites

skjfslkjfs


## Usage

dkjskfjsjlksd

## Standalone
skfjskljfslkjfa
lkdfjslkfjs
 
## BASH Wrapper

