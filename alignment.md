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
- <b>Things to check in OTP</b> 
     - Do you achieve target coverage? For PeDiOn this is ~40x for controls, ~60-80x for primary tumors, and ~80x for relaspse or metastasis tumors
     - Mapped reads should be >99%
     - Properly paired should be  <90% (in most cases 93%-95%)
     - Single read alignments should be <1% (usually 0.01%)
     - DiffChrom (read pairs mapping to different chromosomes) should be <6% (but in some cases up to 10%). It is easy to assume this might be related to chromosomal translocations, but in reality this accounts for very few read pairs mapping to different chromosomes
     - Duplicate reads should be less than 10%, but with very high coverage samples it can go up to 15-20%
     - Median insert size. While this doesnt affect sequencing quality, one should expect that intersert size distributions are larger than twice the read length. Otherwise the ends of R1 and R2 would sequence the middle part of the fragment twice.
     - <b>Even if you have warnings/errors, if they are systematic and affect every sample then the data might still be usable</b> 
- <b>Things to check on the file system</b> 
     - QC directory: `/data/otp/project/pedion/{$project_ID}/sequencing/whole_genome_sequencing/view-by-pid/{$patient_PID}/{$sample_ID}/paired/merged-alignment/qualitycontrol/merged/`
     - overview of QC metrics: `qualitycontrol.json` and `*_commonBam_wroteQcSummary.txt`
     - coverage per 1kb bin (`coverage/*_readCoverage_1kb_windows.txt`), and basic coverage plots (`coverage/*_readCoverage_1kb_windows_coveragePlot.png`)
     - insertsize_distribution (`insertsize_distribution/*_insertsizes.txt`) and plot (`insertsize_distribution/*_insertsize_plot.png`)
     - fingerprinting (`fingerprinting/*E_merged.mdup.bam.fp`), can be used to check for sample swaps but clustering the values obtain in column 8

### Not covered
- the alignment workflow also performs exome, ATAC, ChIPseq, methylation seq alignment... but not discussed in this course
     
# Tasks

1. Go to the OTP website and look at the overview of the RNAseq QC for your project (if available, otherwise WGS)
2. Quickly review the QC table, ordering the samples by the duplication rate
3. Do you see any Qc outliers?
     
[< previous](workflows.md)  |  [home](README.md)  |  [next >](snv.md) 
 
