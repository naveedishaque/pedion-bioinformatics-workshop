[< previous](cna.md)  |  [home](README.md) 

# RNAseq workflow

- https://github.com/DKFZ-ODCF/RNAseqWorkflow
- support single nd paired end reads
- steps:
    - alignment using STAR (2 pass per sample, with adapter trimming)
    - mark duplicates (not removed) using sambamba
    - finger printing (checking 1000 polymorphic positions)
    - RNAseQC
    - Qualimap (optional)
    - read counting using featurecounts
    - FPKM and TPM calculation
         - These calculations are optimised for removing outlier expression (i.e. problematic genes are removed from the library size calculation)
    - Exon-part level counting using featurecounts (experimental)
    - alignment free gene expression quantification using kallisto (optional)
    - fusion detection using arriba
    
## RNAseq results for PeDiOn
- current PeDiOn RNAseq results are based on Illumina TruSeq Nano Total RNA library preparation kit
     - this reports all RNA (!) in a strand specific manner
     - however, there are some quality issues associated with this kit

# Tasks
1. Review RNAseq alignment quality on OTP (OTP top menu -> alingment quality control -> select RNA bulk from the "Seq. Type" drop down menu)
2. Find a RNAseq sample on the file system for your project
3. Review the QC of the sample
4. Check the gene expression quantification in the `featurecounts` folder
5. Check the  `fusions_arriba` directory
 - example of a fusion report by arriba
![](arriba_fusions.png)
[< previous](cna.md)  |  [home](README.md)  

