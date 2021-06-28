[< previous](analysis-structure.md)  |  [home](README.md)  |  [next >](workflows.md) 

# Sample Quality Control

## Sequence level QC
- Typically performed by genomics core facility
- FASTQC results are available in the OTP web interface
    - OTP top menu -> Sequences
    - Click the links to the FASTQC reports
    ![](otp-seq.png)
- FASTQC results are available on the file system
     - `ls /data/otp/project/pedion/*/sequencing/*_sequencing/view-by-pid/*/*/paired/run*/fastx_qc/`

### FASTQC - common issues with Illumina NovaSeq S4 data

There are recurrent QC issues that are highlighted by FASTQC. There are issues that are shared and specific to each of Read 1 and Read 2. Most of even the "critical" errors can have negligable effect.
- Per sequence GC content. This is pretty much always returning a warning. This is a flase positive error when the distribution has the same mode as the expected, but a less dispearsed distribution. An example of a false positive warning:<br><img src="https://user-images.githubusercontent.com/114547/123600384-ea6ef900-d7f6-11eb-95a1-3821d692f160.png" alt="FASTQC GC content false positive error" width="300"/>
- K-mer content. On Read 1, occassionally I see over representation of `TCGCGTATGCCG` k-mers at position 40. This occured frequently in sequencing data produced in mid-2020 (in some projects there are in nearly all R1's), but in 2021 we see this less often. We do not know the cause or the effect of this error:<br><img src="https://user-images.githubusercontent.com/114547/123604677-5c494180-d7fb-11eb-987f-13d32030dfaa.png" alt="kmer content error at pos 39" width="600"/>
- Over-represented sequences: `GGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGGG`. Poly-G stretches will usually accumulate at the end of reads as an artifact of the 2 colour chemistry adopted by the Novo-seq platform. This is a sign that reaggents were depleted towards the end of the run.
  - Illumina 2-colour chemistry defaults to `G` when there is no signal (source: https://www.illumina.com/science/technology/next-generation-sequencing/sequencing-technology/2-channel-sbs.html)<br><img src="https://user-images.githubusercontent.com/114547/123606300-0fff0100-d7fd-11eb-839e-07f1eb0ba85b.png" alt="Illumina 2 colour chemistry" width="150"/>
  - Interesting blog post: https://sequencing.qcfail.com/articles/illumina-2-colour-chemistry-can-overcall-high-confidence-g-bases/
- <b>Please be vigilant with FASTQC errors. Even if you see a flag for e.g. K-mer content, please check this manually to make sure it isnt another error</b>

     
## Alignment and post alignment QC

There are QC aspects spread over different workflows - they will be addressed in various sections.
    
# TASKS

1. Evaluate the QC of read 1 and read 2 for a sample in your study. Look into a WGS and RNAseq sample if avaialbe.

[< previous](analysis-structure.md)  |  [home](README.md)  |  [next >](workflows.md) 
