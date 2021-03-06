[< previous](project-folder-structure.md)  |  [home](README.md)  |  [next >](sample-QC.md) 


# Creating an "analysis" data structure

 - The data generated by OTP is organised by workflows, which isnt always the most intuitive way of organising data for analysis
 - For bioinformatics analysis, we typically organise the data in a way that is agnostic of the workflow as this this easier for navigation
 - We typically call this the **analysis** data structure
 
 ## The analysis data strcutre
 - The general datastructure that we adopt for this is:
 
 ```
 /data/analysis/pedion/${project_ID}/${sequecning_type}/results_per_pid/${pid}/${workflow_output}
 ```
 
  - An example of the folder paths for a patient in A08R:
 ```
# whole genome subfolders:
 
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/qualitycontrol/
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/alignment/
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/mpileup_tumor-bone-marrow-01_control-blood-01/ # SNVs
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/platypus_indel_tumor-bone-marrow-01_control-blood-01/ # indels
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/SOPHIA_tumor-bone-marrow-01_control-blood-01/ # SVs
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/ACEseq_tumor-bone-marrow-01_control-blood-01/ # CNAs
/data/analysis/pedion/A08R/whole_genome_sequencing/results_per_pid/A08R-WPKBAJ/YAPSA_tumor-bone-marrow-01_control-blood-01/ # mutational signatures

# rna seq subfolders:

/data/analysis/pedion/A04R/rna_sequencing/results_per_pid/A04R-ODTDCC/alignment
/data/analysis/pedion/A04R/rna_sequencing/results_per_pid/A04R-ODTDCC/qualitycontrol
/data/analysis/pedion/A04R/rna_sequencing/results_per_pid/A04R-ODTDCC/featureCounts # count matices
/data/analysis/pedion/A04R/rna_sequencing/results_per_pid/A04R-ODTDCC/featureCounts_dexseq # count matrices per exon DO NO USE!
/data/analysis/pedion/A04R/rna_sequencing/results_per_pid/A04R-ODTDCC/fusions_arriba # fusions

 ```
## Creating an analysis data structure

- This "analysis" data strcuture can be created by using the otp-project-softlinker script: https://github.com/naveedishaque/otp-project-softlinker/
- cohort level integrative analysis should be stored in e.g. `/data/analysis/pedion/A04R/cohort_analysis`
- scripts used for downstream data processing should be stored in e.g. `/data/analysis/pedion/A04R/processing_scripts`
- user level analysis should be stored in e.g. `/data/analysis/pedion/A04R/user_folders/${username}`

## General issues

- As with all collabortive projects there will be file/folder permission issues!
- It may be more intuitive to store all the data by the patient and not the sequencing type in the analysis structure. This can be accomodated - speak to naveed.ishaque@charite.de to see how this can be done
 
# Tasks
 
 1. Create a user folder containing a test analysis datastructure (example is for A04R and for my username `ishaquen`):
 ```
 # create folder
 
 cd /data/analysis/pedion/A04R/user_folders # use your project ID
 mkdir ishaquen # user your username
 cd ishaquen
 mkdir test_analysis_structure
 mkdir scripts
 ```
 2. Clone the project softlinker script
 ```
 cd scripts 
 git clone https://github.com/naveedishaque/otp-project-softlinker
 perl otp-project-softlinker/otp-project-softlinker.pl
 ```
 3. Run softlinker on your project
 ```
 perl otp-project-softlinker/otp-project-softlinker.pl -i /data/otp/project/pedion/A04R -o data/analysis/pedion/A04R/user_folders/ishaquen/test_analysis_structure > otp-project-softlinker_A04R_11thOct2020.sh
 sh otp-project-softlinker_A04R_11thOct2020.sh
 ```
 
 4. Look through the resultant structure
 ```
 cd ../test_analysis_structure
 ls
 cd whole_genome_sequencing/results_per_pid
 ls
 ls | wc -l # the number of samples in the project
 ls */alignment/*bam
 grep properlyPaired */qualitycontrol/*/merged/qualitycontrol.json
 ```
 
 [< previous](project-folder-structure.md)  |  [home](README.md)  |  [next >](sample-QC.md) 
