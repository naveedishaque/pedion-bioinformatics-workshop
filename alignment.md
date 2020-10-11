[< previous](workflows.md)  |  [home](README.md)  |  [next >](snv.md) 

# Alignment workflow

- GitHub: https://github.com/DKFZ-ODCF/AlignmentAndQCWorkflows
- Documentation: https://github.com/DKFZ-ODCF/AlignmentAndQCWorkflows/wiki
- In brief: WGS alignment is performed by bwa mem (0.7.15), biobambam sort, sambamba mark duplicated
- we do not recalibrate quality, as we find this tends to remove low VAF variants in impure samples
- QC metrics calculated using samtools flagstats and picard
- genotyping of 1000 highly polymorphic markers (for resolving sample swaps)

## Output

- BAM alignments and BAI indexes (and MD5 sum)
     - File system (project): `ls /data/otp/project/pedion/*/sequencing/*_sequencing/view-by-pid/*/*/paired/merged-alignment/`
     - File system (analysis): `ls /data/otp/project/pedion/*/sequencing/*_sequencing/view-by-pid/*/alignment/`
- QC metrics:
     - File system (project): `ls /data/otp/project/pedion/*/sequencing/whole_genome_sequencing/view-by-pid/*/*/paired/merged-alignment/qualitycontrol/merged/`
     - File system (analysis): `ls /data/analysis/pedion/*/*_sequencing/results_per_pid/*/qualitycontrol/*/merged`
     - coverage plots
     - insert size distribution plot
     - plot of read pairs mapping to different chromosomes
     - picard report
     - flagstat report

## QC
- OTP top menu -> Results -> Alignment quality control
     - navigate different projects and different sequencing types
- If a metric fails, then the metric is reported in yellow or red, depending on threshold determined on analysing several thousand QC metrics
     - this has its drawbacks as the thresholds are based on sequencing type, whereas these thresholds should also consider protocol specific aspects
- If an important metric fails, then access to the sample is locked. This regulated in the "QC Status column".
     - a locked sample can be unlocked via OTP - you would click on the "failed" sample, and report a reason for unblocking it.
     
### Not covered
- the alignment workflow also performs exome, ATAC, ChIPseq, methylation seq alignment... but not discussed in this course
     
# Tasks

1. Go to the OTP website and look at the overview of the RNAseq QC for your project (if available, otherwise WGS)
2. Quickly review the QC table, ordering the samples by the duplication rate
3. Do you see any Qc outliers?
     
[< previous](workflows.md)  |  [home](README.md)  |  [next >](snv.md) 
 
