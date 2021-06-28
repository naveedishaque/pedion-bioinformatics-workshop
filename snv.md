[< previous](alignment.md)  |  [home](README.md)  |  [next >](indel.md) 

# SNV workflow
- https://github.com/DKFZ-ODCF/SNVCallingWorkflow
- https://dockstore.org/containers/quay.io/pancancer/pcawg-dkfz-workflow:2.2.0?tab=info

## Performance
<img src="snv-pcawg.png" width="500"/><br>Validation of variant-calling pipelines in PCAWG. a, Scatter plot of estimated sensitivity and precision for somatic SNVs across individual algorithms assessed in the validation exercise across n = 63 PCAWG samples. Core algorithms included in the final PCAWG call set are shown in blue.  b, Sensitivity and precision estimates across individual algorithms for somatic indels. c, Accuracy (precision, sensitivity and F1 score, defined as 2 × sensitivity × precision/(sensitivity + precision)) of somatic SNV calls across variant allele fractions (VAFs) for the core algorithms. The accuracy of two methods of combining variant calls (two-plus, which was used in the final dataset, and logistic regression) is also shown. d, Accuracy of indel calls across variant allele fractions.
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

## OTP QC using the SNV diagnostic plots
- OTP top menu -> results -> SNV results
![](snv-results.png)
- General overview per sample, including `plots`
     - **Rainfall plots**/ intermutational distance plots: these somatic hyper mutation (SHM) observed in clonal B-cells, and kataegis events in genomicly instable tumors. The following shows a rainfall on chr6. <br><img src="snv-rainfall.png" alt="Rainfalls" width="500"/>
     - **MAF** of somatic mutations (all in red, blue in dbSNP)<br><img src="snv-maf.png" alt="Normal sample" width="150"/>
       - The percentage of somatic SNVs in dbSNP should generally be below 20%. This may be higher when there are very few SNVs due to a fairly high FP rate. If the percentage is higher, we could be dealing with a sample swap, or maajor contamination is the tumor sample (e.g. stem cell translantation)
       - The red peak gives an indication of tumor purity (the closer it is to 50%, the more pure the tumor; the closer it is to 0%, the more impure). The following is a very impure sample<br><img src="https://user-images.githubusercontent.com/114547/123623686-0a5de700-d80e-11eb-9e6d-872790ea3c10.png" alt="Low purity sample" width="150"/>
     - **Mutational pattern** by chromosome and mutation triplet context. These are a poor mans mutational signature analysis and provide a quick insight into mutational signatures. Generally this should be dominated by C->T mutations, otherwise it would indicate another mutational process.<br><img src="snv-pattern.png" alt="Normal sample" width="500"/>
     - **Strand bias - PCR strand**. The mutational signatures may have a PCR strand specific bias. Generally speaking, this is something we do not want to see. These will appear as green or purple spots on the heatmap. They may appear very colourful when the sample have very few somatic mutations. The following shows an example of T->G PCR strand bias that is detected, and then corrected.<br><img src="https://user-images.githubusercontent.com/114547/123630862-56148e80-d816-11eb-8d24-2fd559d4dc07.png" width="500"/>
     - **Strand bias - sequencing strand**. As above, but on the sequencing strand. This can capture e.g. Guanin-Oxidation (OxoG). The following shows an example of T->A sequencing strand bias that is detected, and then corrected.<br><img src="https://user-images.githubusercontent.com/114547/123631001-83613c80-d816-11eb-837e-5b0e11f518d7.png" alt="Strand bias" width="500"/>
     
# Tasks

1. Go to a folder containing the SNV calls of a sample
2. Check if a known cancer gene is mutated: `cut -f 16-18 snvs_*_snvs_conf_8_to_10.vcf | grep -w 'TP53\|KRAS\|CDKN2A\|EGFR\|PI3KCA\|BRCA1\|BRCA2\|PTEN\|APC\|ARID1A' `
3. Check what type of protein coding effects are found in the sample: `cut -f 18 snvs_*_snvs_conf_8_to_10.vcf | sort | uniq -c`
4. Check if any gerline mutations are found in COSMIC: `cut -f 16-18,42 snvs_*_germline_functional_snvs_conf_8_to_10.vcf | grep basechange`

[< previous](alignment.md)  |  [home](README.md)  |  [next >](indel.md) 
