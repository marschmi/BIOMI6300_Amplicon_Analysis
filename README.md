#16S Amplicon Workflow 

This is a folder containing the tutorial information for Marian's BIOMI6300 course. 

Here, we will work with real data to learn how to assign ASVs to 16S amplicon sequences with DADA2. 

Directory contents:  
- `analysis/`: 
      - `DADA2_workflow.Rmd` is the DADA2 workflow that we applied to our sequencing data.  
      - `phyloseq_PreProcessing.Rmd`: Subset samples and ASVs used for later analysis.
- `code/` includes coding files that will make parsing our data easier.  
- `data/` has all of the important data files that we have generated for the project.  
      - `raw_physeq.RData`: This is the raw output from DADA2.  
      - `ASV_taxaonomy.tsv`: Taxonomy file for `raw_physeq.RData`. 
      - `ASV_counts.tsv`: Count table for `raw_physeq.RData`.
      - `ASVs.fasta`: the fasta file for the ASV sequences in the ASV table.  
      - `metadata.csv`: The metadata file for `raw_physeq.RData`.  
      
      
      
## Setting up your folder: 

1.  Log onto the server    
**Note: You'll need to use the Cornell wifi or the Cornell VPN:https://it.cornell.edu/cuvpn**
`ssh your_netid@cbsumm39.biohpc.cornell.edu`

2. Setting up the server directory system for in class work   
**NOTE: NEVER work in the `/home/` directory, instead always work in the `/workdir`!**
`cd /workdir`

3. Make a folder for your own work that is named after your netid
`mkdir <your_netID>`

4. We will need to modify the directory permissions so that folks in the course (including Marian) can see the contents of our files, but not write them
#Assign our netID directory to CALS_Teaching_mls528 group
`chgrp -R CALS_Teaching_mls528 <your_netID>`

5. Change permission so that other users in the group can view our files (but can't overwrite)
`chmod g+s -R <your_netID>`

6. Check to make sure the permission changes worked: 
`ls -lah`  #you should see drwxr-s--- in front of your folder name

7.  Now time to create the folder that we will work in! 
`cd <your_netid>`

8. Make the directory for the in class project
```
mkdir BIOMI6300_Amplicon_Analysis
cd BIOMI6300_Amplicon_Analysis
# Create subdirectories in the folder 
mkdir data
mkdir code
# Create a read me 
echo "#16S Analysis" >> README.md
```

9. Now, we will need to link the data to our folder. First, Copy the metadata.csv file
`cp /workdir/in_class_data/metadata /workdir/<your_netid>/BIOMI6300_Amplicon_Analysis/data`

10.  Now, we will need to link all of the 16S amplicon files that we will use during class while we follow the tutorial: 

```
# Make a symbolic link of all the files 
for FASTQ_FILE in `ls /workdir/in_class_data/raw_gzipped_seqs`
do 
# Echo the file that is currently in the loop
echo $FASTQ_FILE
# Make the symbolic link - it requires two absolute paths!
# The next line is commented out. When you understand the for loop and have checked that it is working correctly, uncomment and run the code to make sure all the files are symbolically linked. (They will be turquoise in your folder! 
#ln -s /workdir/in_class_data/raw_gzipped_seqs/$FASTQ_FILE /workdir/netID/BIOMI6300_Amplicon_Analysis/data/sequencing/
done 
```
*Note about working with large data, instead of using cp create a symbolic link.* 

```
structure of the for loop:
for *file* in `list of files`
do *this*
done

(encompass all the things that you want in your list in backticks ` `)
```
```
for FASTQ_FILE in `ls /workdir/in_class_data/raw_gzipped_seqs`
do 
echo $FASTQ_FILE
#ln -s /workdir/in_class_data/raw_gzipped_seqs/$FASTQ_FILE /workdir/netID/BIOMI6300_Amplicon_Analysis/data/sequencing/
done 
```

Notes on the commands in the for loop:
- `echo` is used to debug and check that all the proper files are in the item list
- `ln` makes links between files
- `-s` makes a symbolic link (only works with absolute paths)
- absolute path (never the relative!) of where the file is
- absolute path (never the relative!) of where we want the file to be symbolically linked to

11. Check to make sure that the number of files linked is the same as the number of FastQ files in the in_class_data folder:
`ls | wc -l` # (in this case, both should be 192)


12. Check to make sure your sequencing files have successfully symbolically linked and are good to start the analysis! 
`ls -lah /workdir/<your_netid>/BIOMI6300_Amplicon_Analysis/data/`

13. Also copy over the `colors_and_shapes.R` and `functions.R` files into a folder in your `BIOMI6300_Amplicon_Analysis/code` directory using the `cp` command. Then you should have both of these files at the following path: `/workdir/your_netID/BIOMI6300_Amplicon_Analysis/code/`


If you have the following, you are ready to go: 

A. Symbolically linked sequencing files within `BIOMI6300_Amplicon_Analysis/data/sequencing/`.  
B. Copies of `colors_and_shapes.R` and `functions.R` files in the following folder: `BIOMI6300_Amplicon_Analysis/code`.  

If you don't have them, try the directions above again, do some googling to de-bug, or reach out to Marian, BIOMI6300 classmates, or lab mates that might be able to help you. You can also check out the tutorial by [AstrobioMike here](https://astrobiomike.github.io/amplicon/dada2_workflow_ex). 
