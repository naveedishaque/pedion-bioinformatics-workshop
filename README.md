# PeDiOn Bioinformatics Workshop 12th Oct 2020

Training material for understanding the output of the PeDiOn bioinformatics workflows (first trial - 12th Oct 2020 10:00-11:00)

The focus of the workshop will to provide an overview of data management and user access privileges (data security), and OTP and automatic data processing.

### [Link to join via Microsoft Teams Meeting](https://teams.microsoft.com/l/meetup-join/19%3adc6ee9195867464f94f57e6b33cfd602%40thread.tacv2/1602144919457?context=%7b%22Tid%22%3a%22afe91939-923e-432c-bc66-cbc3ec18d02c%22%2c%22Oid%22%3a%221298273b-1298-4d92-a14b-894d7df2a533%22%7d)

### Focus projects

Make sure you have access to : `/data/analysis/pedion/${project}/whole_genome_sequencing/` (please check that you have access today!)
-	A01P (Joachim)
-	A06R (Kerstin, Elias)
-	A08R (Anna)
-	OTP - http://s-bih-otp-www.bihealth.org:8080/otp/

### Requirements
- Register for the course by emailing naveed.ishaque@charite.de
- Charite compute account (Mail Antrag, or a Kooperations Antrag)
- VPN access to Charite (VPN Antrag)
- VPN access to eils-hpc and OTP (VPN Zusatz Antrag B)
- Computer with SSH access to `eils-login1.bihealth.org`
- Access to [OTP](http://s-bih-otp-www.bihealth.org:8080/otp/)

# Content

- [Getting started - what is PeDiOn, what data is produced, how to I get access](getting-started.md)
- [What is OTP?](what-is-OTP.md)
- [Data - Data managment, data access priviliges, data security](data-management.md)
- [Project overview and managment via OTP](otp-project-overview.md)
- [The Eils-HPC](eils-hpc.md)
- [**Project** Data structure created by OTP](project-folder-structure.md)
- [Creating an **analysis** data structure](analysis-structure.md)
- [Evaluating quality of samples via OTP](sample-QC.md)
- [OTP workflows:](workflows.md)
    - [Alignment: bwa](alignment.md)
    - [SNV calling: mpileup](snv.md)
    - [Indel calling: platypus](indel.md)
    - [SV calling: sophia](sv.md)
    - [Copy number abberation calling: ACEseq](cna.md)
    
### What is not covered
- how to use linux, python, R, ...
- in depth cluster usage
- in depth description of workflows

## Authors

Naveed Ishaque

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
 
