# MG Wrapser



MG Wrapser is used to recruit reads or contigs from metagenomic data using reference datasets. The script wraps BLAST queries against the reference(s), processes the output, quantifis and recruits the target sequences from metagenomic data.

Development version of the tool is available at <https://github.com/nyirock/mg_blast_wrapper>

## Table of Contents

- [Background](#background)
  - [Directory Structure](#directory-structure)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
  - [Standalone](#standalone)
  - [BASH Wrapper](#bash-wrapper)
  - [Examples](#examples)
- [License](#license)


## Background

MG Wrapser is designed to recruit and quantify reads or contigs from metagenomes by mapping them to the referenec(s). Currently only the BLAST similarity feature is supported, while contig recruitment and binning by GC content and k-mer frequencies are in development.

It is possible to alter the stringency criteria for contigs/reads recruitments by changing minimum BLAST e-Value, % or bp of allignment length, % identiy, etc.

Recruited contigs either as .fasta or .csv files are placed in the results folder of the project directory with suffixes reflecting the order of metagenomes (total of N) that had been supplied, e.g.:<br /> \*_mg_0.fasta, \*_mg_1.fasta, ..., \*_mg_N-1.fasta.<br />( \*_mg_0.csv, \*_mg_1.csv, ..., \*_mg_N-1.csv).<br /> By design, the script treats multiple input metagenomes separatlely. However, if several reference files are supplied, they are combined into a single file and a signe database is created. If it is necessary to run software with separate reference files it is suggested to use the script with the supplied BASH Wrapper (see [BASH Wrapper section](#bash-wrapper) for the details).

Currently only fasta formats are supported for both input references and metagenomes. Default output is the recurited metagenomic sequences in fasta format. It is also possible to obtain the results in tab-delimited csv file (or both csv and fasta), that contains target sequences plus allignment features and basic parameters such as GC values, RPKM, etc.

Results log file is also created in the end of the run. Results log file contains summary and basic statistic calculations of the run, such as:
- Number, %, RPKM of recruited sequences
- Average recruited sequence lengs plus STD and SEM
- Average recruited sequence GC, STD, SEM
- Average recruited sequence identity, allignment length, etc.

## Directory Structure

If no project name is specified, by default a folder called "output" containing the project files is created in the directory containing the script.
Upon running the scrip the following directory structure is created:

``` 
./ ### foleder containing the python script
  |
  ├── mg_wrapser_latest.py ### executable file
  |
  +── output ### project directory
      |
      +── input_files ### folder containing copied and processed reference files
      |  
      +── blast_db ### folder for the BLAST database
      |  
      +── results ### folder containing results files in .csv, .fasta and .tab formats
      |   
      ├── results_log.csv ### run summary file
```

## Prerequisites

MG Wrapser requires 
* Local version of NCBI BLAST
* python 2, and its packages such as: 
  * NumPy
  * pandas 
  * BioPython 
  * SciPy <br />
  
to be installed locally. The script has been tested with both legacy BLAST and BLAST+. UNIX-based workstations, running Linux or Mac OS are recommended. Using the software on Windows machines is possible however untested.


## Usage

```bash
mg_wrapser_latest.py -[OPTION]...[ARGUMENT]
````


## Standalone
For a standalone use the script is called directly with the required and optional parameters.
```
Required parameters:
-m, --metagenome       path to the metagenome file(s). Multiple files are submitted as a quoted comma-separated list.
-r, --reference        path to the reference file(s). Multiple files are submitted as a quoted comma-separated list.

Optional parameters:
-n, --name             name for a project and a project directory. Default: "output".
-a, --alignment_length minimum alignment length for the sequence to be retrieved in bp(number) or %(number followed by a "%"sign). Default: 50%.
-i, --identity         minimum identity of the sequence to be retrieved (number from 0 to 100). Default: 95.
-e, --e_value          BLAST E-value cutoff (e.g 0, 0.001, 1e-20 etc.). Defaut: 1e-5.
--shear                Enables shearing reference sequences into fragments of specified lengths in bp.
-f, format             Specifies an output format (csv and/or fasta supported). Default: fasta.
--iterations           Enables iterative run of the program. Intialize parameter to "true" or a positive number.

Optional flags:
-h, --help             Displays a help string        
--debugging            Enables debugging messages if submitted
--continue_from_previous Prevents directory re-writing
--skip_blasting        Skips blasting step. Forces the program to use previous blast results.
```
 
## BASH Wrapper
Running the software from within the BASH script enables easy way to test
* Different reference file(s) separately
* Various stringency parameters, supplied as fixed falues or with an increment parameter
* Specify list of reference shear values, etc.


To run MG Wrapser from a supplied BASH script use the following command:
```bash
cycle_wrapper_latest.bash -f mg_wrapser_latest.py -p parameters_default.txt
```
Where mg_wrapser_latest.py and parameters_default.txt are the MG Wrapser and its parameters file respectively. Sample parameter settings and the corresponding instructions could be found in parameters_default.txt file.

## Licence
