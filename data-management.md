[< previous](data-management.md)  |  [home](README.md)  |  [next >](eils-hpc.md) 

# Data - Data managment, data access priviliges, data security

## File/folder structure

- in order to process and analyse data effectively it has to be stored in a structured way
- primary data ingested by OTP and directly created by OTP is read only to prevent accidental modification

## Data access management

- data access is detemrined by data *owners*
- data ownership is a hot topic - who owns the data? Sample curator? Financer of generation of data? **Patient?** 
   - all have a claim, but the **most** important owner is the patient - their right to privacy supercedes all secondary claims
- Datanschutz is king

## Data security
- in order to adhere to data protection requirement, data access is highly regulated
- user access is granted through linux user groups
- all primary and dervied data is stored in project specific directories with group level management
- all primary and derived data from a project has to remain in the managed directories (i.e. no data in your home folder or laptop!)
- on publication, data is uploaded to the European Genome/Phenome Archive (EGA) hosted at EMBL-EBI
    - data is registered so people know its there, but it cannot be accessed without approval
    - data access is regulated via a Data Access Committee Officer (DACO), which would be PeDiOn Directors, Co-ordinator, Project PIs
- data can be made available to the project PI
    - it then becomes the project PIs responsibilty to ensure data security
    - project PI would need to make an official request via the PeDiOn coordinator (Bianca Hennig), which will be followed up by the HPC admin (Stefan Schneider)

# Tasks (this is theoretical task)
1. Find your project directory on the cluster
2. Copy FASTQ files to your laptop
3. Go to jail, do not pass go
    - seriously, please remember that we are dealing with sensetive data which can identify individual, and their families, so treat the data with respect

[< previous](data-management.md)  |  [home](README.md)  |  [next >](eils-hpc.md) 
