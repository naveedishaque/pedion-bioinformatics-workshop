[< previous](workflows.md)  |  [home](README.md)  |  [next >](snv.md) 

# Alignment

- WGS alignment is performed by bwa mem (0.7.15)
- biobambam sort
- sambamba mark duplicated
- we do not recalibrate quality, as we find this tends to remove low VAF variants in impure samples
- QC metrics calculated using samtools flagstats and picard
- genotyping of 1000 highly polymorphic markers (for resolving sample swaps)

## Output

- BAM alignments and BAI indexes (and MD5 sum)

## QC
- OTP top menu -> Results -> Alignment quality control
     - navigate different projects and different sequencing types
- If a metric fails, then the metric is reported in yellow or red, depending on threshold determined on analysing several thousand QC metrics
     - this has its drawbacks as the thresholds are based on sequencing type, whereas these thresholds should also consider protocol specific aspects
- If an important metric fails, then access to the sample is locked. This regulated in the "QC Status column".
     - a locked sample can be unlocked via OTP - you would click on the "failed" sample, and report a reason for unblocking it.
     
[< previous](workflows.md)  |  [home](README.md)  |  [next >](snv.md) 
 
