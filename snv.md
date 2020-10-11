[< previous](alignment.md)  |  [home](README.md)  |  [next >](indel.md) 

# SNV workflow
- https://github.com/DKFZ-ODCF/SNVCallingWorkflow
- https://dockstore.org/containers/quay.io/pancancer/pcawg-dkfz-workflow:2.2.0?tab=info

## Performance
![](snv-pcawg.png)
> Validation of variant-calling pipelines in PCAWG. a, Scatter plot of estimated sensitivity and precision for somatic SNVs across individual algorithms assessed in the validation exercise across n = 63 PCAWG samples. Core algorithms included in the final PCAWG call set are shown in blue.  b, Sensitivity and precision estimates across individual algorithms for somatic indels. c, Accuracy (precision, sensitivity and F1 score, defined as 2 × sensitivity × precision/(sensitivity + precision)) of somatic SNV calls across variant allele fractions (VAFs) for the core algorithms. The accuracy of two methods of combining variant calls (two-plus, which was used in the final dataset, and logistic regression) is also shown. d, Accuracy of indel calls across variant allele fractions.
Campbell, P.J., Getz, G., Korbel, J.O. et al. Pan-cancer analysis of whole genomes. Nature 578, 82–93 (2020). https://doi.org/10.1038/s41586-020-1969-6

## Somatic calling
- mpileup is used with high sensetivity in tumor, containing a combination of somatic and germline SNVs
    - `snvs_A01P-ZOMNON_raw.vcf.gz`
- each SNV is assigned a "confidence", starting at 10
- mutations lying on "problematic regions" (e.g. read attracting, black lister region, STRss) are punished, and confidence is reduced
- mutations are classified as germline if >=2 (3?) reads are found in the control
- each SNV is annotated for coding effect
- each SNV is annotated to belong to a certain region (e.g. CpGI, enhancer, miRNA, repeat...)
    - `snvs_A01P-ZOMNON.vcf.gz`
- all remaining mutations with confidence >=8 are considered as somatic candidates, and filtered as subsets
    - `snvs_A01P-ZOMNON_somatic_snvs_conf_8_to_10.vcf`
    - `snvs_A01P-ZOMNON_functional_snvs_conf_8_to_10.vcf` (with protein coding effect, or splice)    
    - `snvs_A01P-ZOMNON_germline_functional_snvs_conf_8_to_10.vcf` (potential germline, with protein coding effect, or splice - **this list is very lenient!**)
    - `snvs_A01P-ZOMNON_somatic_functional_ncRNA_snvs_conf_8_to_10.vcf` (and exonic ncRNA mutation)

## Deep annotation of SNVs

- The VCF files produced by the SNV workflow are not conformant with the VCF 4.0 standard
- The contain additional columns, which we refer to as "deep annotation" (which should be encoded in the INFO field, but use append them as tab separated columns)
    - 1:CHROM
    - 2:POS
    - 3:ID
    - 4:REF
    - 5:ALT
    - 6:QUAL
    - 7:FILTER
    - 8:INFO
    - 9:FORMAT
    - 10:genotype column
    - 11:SEQUENCE_CONTEXT
    - 12:INFO_control(VAF=variant_allele_fraction;TSR=total_variant_supporting_reads_incl_lowqual)
    - 13:**ANNOTATION_control** - somatic or germline
    - 14:DBSNP - ovrelap with dbSNP
    - 15:1K_GENOMES - overlap with 1000 genomes
    - 16:ANNOVAR_FUNCTION - e.g. exonic, splicing, intronic, UTR, upstream, intergenic....
    - 17:GENE - gencode gene name
    - 18:EXONIC_CLASSIFICATION - effect on pretein, e.g. synonymous, stoploss, non-synonymous, frameshift
    - 19:ANNOVAR_TRANSCRIPTS - codon and protein affect on transcripts
    - 20:SEGDUP
    - 21:CYTOBAND
    - 22:REPEAT_MASKER
    - 23:DAC_BLACKLIST
    - 24:DUKE_EXCLUDED
    - 25:HISEQDEPTH
    - 26:SELFCHAIN
    - 27:MAPABILITY
    - 28:SIMPLE_TANDEMREPEATS
    - 29:**CONFIDENCE**
    - 30:**RECLASSIFICATION**
    - 31:PENALTIES
    - 32:seqBiasPresent_1
    - 33:seqingBiasPresent_1
    - 34:seqBiasPresent_2
    - 35:seqingBiasPresent_2
    - 36:Enhancers
    - 37:CpGislands
    - 38:TFBScons
    - 39:ENCODE_DNASE
    - 40:miRNAs_snoRNAs
    - 41:miRBase18
    - 42:COSMIC
    - 43:miRNAtargets
    - 44:CgiMountains
    - 45:phastConsElem20bp
    - 46:ENCODE_TFBS

## OTP QC
- OTP top menu -> results -> SNV results
![](snv-results.png)
- General overview per sample, including `plots`
     - **Rainfall plots**/ intermutational distance plots: somatic hyper mutation (SHM), kataegis events
     
     ![](snv-rainfall.png)
     - **MAF** of somatic mutations (all in red, blue in dbSNP)
     
     ![](snv-maf.png)
     - **Mutational pattern** by chromosome and mutation triplet context
     
     ![](snv-pattern.png)
     - **Strand bias - PCR strand**
     
     ![](snv-pcr-stran-bias.png)    
     - **Strand bias - sequencing strand**
     
     ![](snv-seq-stran-bias.png)  
     
# Tasks

1. Go to a folder containing the SNV calls of a sample
2. Check if a known cancer gene is mutated: `cut -f 16-18 snvs_*_snvs_conf_8_to_10.vcf | grep -w 'TP53\|KRAS\|CDKN2A\|EGFR\|PI3KCA\|BRCA1\|BRCA2\|PTEN\|APC\|ARID1A' `
3. Check what type of protein coding effects are found in the sample: `cut -f 18 snvs_*_snvs_conf_8_to_10.vcf | sort | uniq -c`
4. Check if any gerline mutations are found in COSMIC: `cut -f 16-18,42 snvs_*_germline_functional_snvs_conf_8_to_10.vcf | grep basechange`

[< previous](alignment.md)  |  [home](README.md)  |  [next >](indel.md) 
