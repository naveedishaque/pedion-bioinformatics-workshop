[< previous](sv.md)  |  [home](README.md)  |  [next >](rnaseq.md) 

# ACEseq CNA workflow
- https://github.com/DKFZ-ODCF/ACEseqWorkflow
- https://aceseq.readthedocs.io/en/latest/
- https://www.biorxiv.org/content/10.1101/210807v1.full

## Somatic calling
- ACEseq models allele specific copy numbers
- An exahusive search of combinations of purity and ploidy are performed.
    - visualised in the star plot , with the best model reported with a star: `*_tcn_distances_combined_star.png`
    ![](aceseq-star.png)
    - the godness of fit for best hits reported in: `*_ploidy_purity_2D.txt`
- A TSV file of the solution reported: `*_most_important_info{est_ploid}_{est_purity}.txt`
- Plots of the solution are also reported: `*_plot_*_*_ALL.png`
- The lower bound of tumor purity that can be identified is 15% (parametisable)
    - **if the estimated purity is below 15%, ACEseq reports the purity as 100%**

## The `most_important` CNA file

- The columns in the ACEseq `most important file`:
    - 1:chromosome
    - 2:start
    - 3:end
    - 4:length - length of segment
    - 5:covRatio - coverage ratio of tum:control
    - 6:TCN - estimated total copy number of the segment
    - 7:SV.Type - annotation of the SV overlaping the segment border - IGNORE!
    - 8:c1Mean - minor allele copy number
    - 9:c2Mean - major allele copy number
    - 10:dhEst - raw decrease in heterozygosity estimated
    - 11:dhSNPs - 
    - 12:genotype - ratio of rounded allele copy numbers
    - 13:CNA.type - DUP/DEL/LOH/TCNneutral/HomoDel 
    - 14:NbrOfHetsSNPs - number of control heterozygous SNPs in segment (**if this is below 5 it is not trustworthy**)
    - 15:minStart - last SNP prior to segment start
    - 16:maxStart - first SNP after segment start
    - 17:minStop - last SNP prior to segment end
    - 18:maxStop - first SNP after segment end


## OTP QC
- OTP top menu -> results -> CNV results
- click on plots
- The diagnostic plots show:
     - raw coverage counts per 1 kb window
     - coverage stratified by GC content (and correction)
     - coverage stratified by replication timing (and corrected)
     
# Tasks

1. Go to a folder containing the ACEseq CNV calls of a sample
2. Check how many copy number solutions were estimated: `cat *_ploidy_purity_2D.txt`
3. Check if any homozygous deletions exist: `grep HomoDel *most_important* | wc -l`
 - do they have more than 5 heterozygous SNPs supporting them? `grep HomoDel *most*grep HomoDel *most_important* | awk '$14>5' | wc -l`
4. Check the CNV plots of a sample on OTP:
 - do any samples show GC or replication timing bias?
 - evaluate the plausbility of the ACEseq solution plot (last pages of the PDF)

[< previous](sv.md)  |  [home](README.md)  |  [next >](rnaseq.md) 
