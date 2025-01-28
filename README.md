# ATAVIDE-Post-processing
FAME Metagenomics post-processing scripts 


With this code we can summarise mmseqs taxonomy data to create abundance profiles from each sample. We then bring our data into R and merge datasets into a single merged file with samples are columns and taxa string as rows. 

The script filter_tophit.slurm will identify all files in the current directory with the string "*tophit_report_subsystems_taxa" to search for the specific taxa of interest and collate the results together in a single files dynamically named for the specified taxa. 
