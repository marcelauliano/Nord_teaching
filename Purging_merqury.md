
# Purging and Merqury evaluation

Ok, today you learned about Purge Dups and purging assemblies. You also learned that Hifiasm and other assemblers are not perfect in separating haplotypes of diploid species, 
and then many times the primary assembly retains haplotigs, and that this redanduncy is not real and must be removed before assemblies are scaffolded. Later, you learned how 
to evaluate assembly completeness and quality having a look at the shared kmers between the assembly and high-quality reads (eg., as Illumina or PacBio HiFi).
Now you are going to inspect merqury outputs to evaluate the assembly of *Apodemus sylvaticus* before and after purging. 

Earlier today you worked with the outputs of a run I ran previously for *Apodemus sylvaticus*. In addition to the files you already have (statiscs and BUSCO run), I have also
generated a merqury run for the assembly coming out of hifiasm. I want you to create a folder in your working directory and copy these results there.

The merqury results for hifiasm are here:

```console
ls path/assembly/merqury

# You need to copy those results to your working directory, so perhaps first let's create a subirectory for the merqury results
cd ~/a_sylvaticus/hifiasm/
mkdir merqury
cd merqury

# Now copy all the files there
cp path/assembly/merqury/* .
```

## Great.
Now you have all the results for your assembly before purging, including merqury plots and other results.

## Evaluation after Purge Dups

Now, let's gather the results and evaluate the purged version of *Apodemus sylvaticus* genome. We don't have time to run [Purge_dups](https://github.com/dfguan/purge_dups) here, 
but the **most important** thing in science is to learn how to interprete outputs. Eventually, with time, you can learn how to run all the commands for different softwares, and that is great. But if you don't know how to 
critically evaluate the outputs, is it worth just learning how to simply run a linux command? No! Running commands is just the beggining. The real science starts after.
So let's learn how to evaluate our outputs!
I have geneated a purge dups run for you which generates (i) purged assemblies. After purging, then I generated the (ii) merqury plots and (iii) BUSCO results.  

1-) First thing you need to do to gather all this results is to symlink the purged version of the assembly and calculate the general statistics for the primary and haplotigs files. Let's create a new directory to save the purged results and create the symlinks there:

```console  
mkdir ~/a_sylvaticus/purged/
cd ~/a_sylvaticus/purged/
ln -s path/mApoSyl1_data/purged/purged.fa.gz
ln -s path/mApoSyl1_data/purged/purged.htigs.fa.gz
```  
Now export our scripts directory and activate our main conda environment:

```console
export PATH=$PATH:/home/ubuntu/Share/scripts/
conda activate BIO5025
```

And then run the `asmstats` script for each file:

```console
asmstats purged.fa.gz > purged.fa.gz.stats
asmstats purged.htigs.fa.gz > purged.htigs.fa.gz.stats
```

Great!

2-) Now, I want you to take a look and take notes of the BUSCO results **before** and **after** purging. The BUSCO file from before purging you already have from
the assembly tutorial. Now let's gather the BUSCO results for after purging. 

```console
# if you are not there yet, go back to your purging directory
cd ~/a_sylvaticus/purged/
# then copy the busco file for the purged primary assembly
cp path/mApoSyl1_data/purged/purged.busco.short_summary.txt . 
```
Right, now let's copy over the merqury results after purging. Make a folder for the merqury outputs in your working directory and copy files over.

```console
# if you are not there yet, go back to your purging directory
mkdir ~/a_sylvaticus/purged/merqury
cd ~/a_sylvaticus/purged/merqury
# then copy the busco file for the purged primary assembly
cp path/mApoSyl1_data/purged/merqury/* . 
```
## Good.

Now you have all the results you need for evaluation of your assembly before and after purging.

 
# About the Merqury output files
 
As we discussed earlier in the lecture today, Merqury creates a lot of different output files: (i) different plot (.png) files, (ii) a <outname>.completeness.stats and (iii) a <outputname>.qv file.  
    
For the plot files, you will have 3 types: st (stacked), ln (line) and fl (filled). 
### These three graphs will represent the same data
These files are just a different way of plotting the (same) data. For further information I have a look at the manual [here](https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation).
   
# Further
Apart from having st, fn and ln, merqury outputs 2 types of plot files, *asm* and *cn*. The plots containing *cn* shows all kmer counts of primary + haplotigs assembly in the plot, without descriminating them as primary or haplotigs. In contrast, Ff containing *asm* shows kmers belonging to each assembly (purged and haplotigs) in the different colours. 

DEEP BREATH.

You are going to get it! (It's not very easy to understand merqury plots at the first time we look at them. So well done; you are becoming an expert). 

Is it difficult to get it all? Discuss with your group! Don't be shy!

## In addition to the plots

Understand what each column of the files qv and completeness mean by reading the manual here:  https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation


## Let's go back interpreting our results

Now we will take a look at everything. 
All the merqury results are now copied to your working folder. Download the plots to your local machine.
  
  1-) Gather the merqury output plots for the primary assembly before (```mApoSyl1.ccs.mApoSyl1.p_ctg.spectra-cn.st.png``` and after purging ```mApoSyl1.ccs.purged.spectra-cn.st.png```. 
    
  2-) Gather the completeness results for the run. The file ends in `completeness.stats`
  
  3-) Gather the QV results for the run. The file is called `purged.qv`

  4-) Gather the BUSCO result for the primary assembly after purging.

  Now that you have all of these gathered, do the same for the assembly before purging. We ran all of this yesterday. You need general statistics, BUSCO and merqury results.
  
  
Now that you have all the results organized, let's interpret them and discuss with your group while you make your group presentation.
  
  - show the statistics for the Hifiasm p_ctg and a_ctg assemblies
  - show the busco short summary for the Hifiasm p_ctg assembly
  - show the spectra plot for the Hifiasm p_ctg assembly (let's use ```mApoSyl1.ccs.mApoSyl1.p_ctg.spectra-cn.st.png```)
  - show the completeness for the Hifiasm assemblies
  - show the QV for the Hifiasm assemblies.
  
  Go and do the same for the primary purged assembly:
  
  - show the statistics for the purged and htigs assembly
  - show the busco short summary for the purged assembly
  - show the spectra plot for the purged assembly (let's use ```mApoSyl1.ccs.purged.spectra-cn.st.png```)
  - show the completeness for the purged assembly
  - show the QV for the purged assembly.
  
 # Now  
  
  I don't know if you realised, but you have for now (i) ran kmer analyses to understand the DNA composition of your reads, (ii) genome assembly and you are learning how to (iii) interprete the BUSCO run results and how to run (iv) and interpret (v) kmer assembly evaluation results with merqury! **THIS IS A LOT FOR THREE DAYS!** Really well done! Now its time to gather all of the results and answer the following questions with your team and later on we will go through them together as a group.
  
  
  a-) What has happened with the assembly general statistics after it was purged?
  
  b-) After purging, what the files purged and htigs mean?
  
  c-) How is the BUSCO duplication before purging?
  
  d-) How is the busco duplication in the purged assembly after purging? Why has it changed?
  
  e-) What are all the QVs of the assemblies before and after purging? Are they good QVs? 
  
  f-) What a QV of 50 means?

  g-) How is the completness for the primary before and after puring? Why did it change?
  
  Well done! Let's come back to the group all together now!
 


