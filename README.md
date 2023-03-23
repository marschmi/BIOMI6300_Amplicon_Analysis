#16S Amplicon Workflow 

This is a folder containing the tutorial information for Marian's BIOMI6300 course. 

Here, we will work with real data to learn how to assign ASVs to 16S amplicon sequences with DADA2. 

Directory contents:  
- `DADA2_workflow.Rmd` is the DADA2 workflow that we applied to our sequencing data.  
- `code/` includes coding files that will make parsing our data easier.  
- `data/` has all of the important data files that we have generated for the project.  
      - `raw_physeq.RData`: This is the raw output from DADA2.  
      - `ASV_taxaonomy.tsv`: Taxonomy file for `raw_physeq.RData`. 
      - `ASV_counts.tsv`: Count table for `raw_physeq.RData`.
      - `ASVs.fasta`: the fasta file for the ASV sequences in the ASV table.  
      - `metadata.csv`: The metadata file for `raw_physeq.RData`.  
      
      


