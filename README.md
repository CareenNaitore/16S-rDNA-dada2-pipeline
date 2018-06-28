# ![kviljoen/16S-rDNA-dada2-pipeline](/assets/cbio_logo.png)

# 16S rRNA gene amplicon sequencing pipeline using DADA2, implemented in Nextflow

A dada2-based workflow using the Nextflow workflow manager.  The basic pipeline is currently implemented, including some basic read-tracking. This pipeline is adapted from https://github.com/HPCBio/dada2-Nextflow for implementation on the UCT high-performance compute cluster

## Basic usage:

    The typical command for running the pipeline is as follows:
    nextflow run uct-cbio/16S-rDNA-dada2-pipeline --reads '*_R{1,2}.fastq.gz' --trimFor 24 --trimRev 25 --reference 'gg_13_8_train_set_97.fa.gz' -profile uct_hex
    Mandatory arguments:
      --reads                       Path to input data (must be surrounded with quotes)
      -profile                      Hardware config to use. Currently profile available for UCT's HPC 'uct_hex' - create your                                     own if necessary
      --trimFor                     Set length of R1 (--trimFor) that needs to be trimmed (set 0 if no trimming is needed)
      --trimRev                     Set length of R2 (--trimRev) that needs to be trimmed (set 0 if no trimming is needed)
      --reference                   Path to taxonomic database to be used for annotation (e.g. gg_13_8_train_set_97.fa.gz)
    
    Other arguments:
      --pool                        Should sample pooling be used to aid identification of low-abundance ASVs? Options are                                         pseudo pooling: "pseudo", true: "T", false: "F"
      --outdir                      The output directory where the results will be saved
      --email                       Set this parameter to your e-mail address to get a summary e-mail with details of the run                                     sent to you when the workflow exits
      -name                         Name for the pipeline run. If not specified, Nextflow will automatically generate a random                                     mnemonic.
    
    Trimming arguments (optional):
      --truncFor                    Select minimum acceptable length for R1 (--truncFor). Reads will be truncated at truncFor                                     and reads shorter than this are discarded (default 0, no trimming).
      --truncRev                    Select minimum acceptable length for R2 (--truncRev). Reads will be truncated at truncRev                                     and reads shorter than this are discarded (default 0, no trimming).
      --maxEEFor                    After truncation, R1 reads with higher than maxEE "expected errors" will be discarded. EE                                     = sum(10^(-Q/10)), default=2
      --maxEERev                    After truncation, R2 reads with higher than maxEE "expected errors" will be discarded. EE                                     = sum(10^(-Q/10)), default=2
      --truncQ                      Truncate reads at the first instance of a quality score less than or equal to truncQ;                                         default=2
      --maxN                        After truncation, sequences with more than maxN Ns will be discarded. Note that dada()                                         does not allow Ns; default=0
      --maxLen                      Remove reads with length greater than maxLen. maxLen is enforced before trimming and                                           truncation; default=Inf (no maximum)
      --minLen                      Remove reads with length less than minLen. minLen is enforced after trimming and                                               truncation; default=20
      
      Merging arguments (optional):
      --minOverlap                  The minimum length of the overlap required for merging R1 and R2; default=20 (dada2                                           package default=12)
      --maxMismatch                 The maximum mismatches allowed in the overlap region; default=0.
      --trimOverhang                If "T" (true), "overhangs" in the alignment between R1 and R2 are trimmed off. "Overhangs"                                     are when R2 extends past the start of R1, and vice-versa, as can happen
                                    when reads are longer than the amplicon and read into the other-direction primer region.                                       Default="F" (false)
      
      Taxonomic arguments (optional):
      --species                     Specify path to fasta file. See dada2 addSpecies() for more detail.
     
     Help:
      --help                        Will print out summary above when executing nextflow run uct-cbio/16S-rDNA-dada2-pipeline                                     --help

## Prerequisites

Nextflow, dada2 (>= 1.8), R (>= 3.2.0), Rcpp (>= 0.11.2), methods (>= 3.2.0), DECIPHER, phangorn, biomformat

## Documentation
The uct-cbio/16S-rDNA-dada2-pipeline pipeline comes with documentation about the pipeline, found in the `docs/` directory:

1. [Installation](docs/installation.md)
2. [Running the pipeline](docs/usage.md)

## Built With

* [Nextflow](https://www.nextflow.io/)
* [Docker](https://www.docker.com/what-docker)
* [Singularity](https://singularity.lbl.gov/)


## Credits

The initial implementation of the DADA2 pipeline as a Nextflow workflow (https://github.com/HPCBio/dada2-Nextflow) was done by Chris Fields from the high performance computational biology unit at the University of Illinois (http://www.hpcbio.illinois.edu). Please remember to cite the authors of [DADA2](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4927377/) when using this pipeline. Further development to the Nextflow workflow and containerisation in Docker and Singularity for implementation on UCT's HPC was done by Dr Katie Lennard and Gerrit Botha, with inspiration and code snippets from Phil Ewels http://nf-co.re/

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details


