[< previous](sample-QC.md)  |  [home](README.md)  |  [next >](alignment.md) 

# Workflows

## Scientific workflow management
- There are a large number of tools for managing scientific workflows
    - 10 years ago there werent so many, so we developed our own: [Roddy](https://roddy-documentation.readthedocs.io/en/latest/)
    - Now Roddy is no longer developed and we are hoping to migrate to more established systems, e.g.:
         - nextflow/nfcore (preferred)
         - snakemake
         - CWL

## Workflow defaults
- genome: all processing is done against the 1000 genomes phase 3 assembly with decoy contigs (hs37d5) - his is a hg19 derived genome
    - migration to hg38 is late (we planned to skip this and go straight to hg39/hg40, but this will not be released)
    - 75% of workflows have been migrated to hg38
- gene models: genecode v19 complete
    - why not a higher version? Gencode 19 was the last native release for hg19, and all other were "lift overs" of hg38 builds. These lift overs introduced errors and missing important genes.
- language: bash, perl, with a bit of python and R.
    - many developers = many languages
    - the original developers were old school (i.e the code is nto well written, and not much in terms of good software engineering practices)

## Workflows
- https://github.com/DKFZ-ODCF/AlignmentAndQCWorkflows
- https://github.com/DKFZ-ODCF/RNAseqWorkflow
- https://github.com/DKFZ-ODCF/SNVCallingWorkflow
- https://github.com/DKFZ-ODCF/IndelCallingWorkflow
- https://github.com/DKFZ-ODCF/SophiaWorkflow (SVs)
- https://github.com/DKFZ-ODCF/ACEseqWorkflow (CNAs)

    
[< previous](sample-QC.md)  |  [home](README.md)  |  [next >](alignment.md) 
