# Data structure created by OTP

## Raw data managed by OTP

- All project data should be stored via OTP. Structure is managed by OTP, and is read only.
- We cal this the **project** data structure 
- Most workflows are executed via workflow management system called [`Roddy`](https://roddy-documentation.readthedocs.io/en/latest/)
- Data is usually organised per workflow
- We will only briefly go over this, and focus more on the **analysis** data structure

```
# Top level structure. "$project_umbrella" is optional. It would be something like "icgc" or "pedion"
/data/otp/project/$project_name/
/data/otp/project/$project_umbrella/$project_name/

# For sequencing data
/data/otp/project/$project_umbrella/$project_name/sequencing
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/raw
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/raw/{flowcell_ID or $submission_ID or $ilse_ID}

/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}/{$sample1}
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}/{$sample2}

/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}/{$sample1}/{$workflow1}
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}/{$sample1}/{$workflow2}
/data/otp/project/$project_umbrella/$project_name/sequencing/{$sequencing_type}/view-by-pid/{$doner}/{$sample1}/{$workflow3}
```

## Raw data not managed by OTP (work in progress!)

This would be for project not under OTP control. This would include:
*  ongoing projects that are not part of OTP that require user control (e.g. Kbiobank, ICGC, TCGA), 
*  large external datasets for general use with no restrictions (HCA, ENCODE), 
*  and reference files (human genome sequence, genome models, etc). 

Structure is managed by an Admin and select users/volunteers, and is read only to most.

```
/data/project_ext/
/data/public_datasets/  
/data/reference_files/
```
For Reference_files, `project_ext` and `public_data_sets` we'll need volunteers who maintain this folders!

All external datasets and refernce fils should be accomanied with a README outlining the exact commands used to download the data.

# Tasks

1. Find out how many different data types your project has (example for A04R)
```
cd /data/otp/project/pedion/A04R/sequencing
ls
```
2. Check to see how many whole genome sequencing samples your poject has
```
cd /whole_genome_sequencing/view-by-pid
ls
ls | wc -l
```
3. Check to see what has been processed for each sample
```
ls *
```
4. Check to see how many SNV runs have completed for your project
```
ls */snv_results/paired/*

```
