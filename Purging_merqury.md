
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
ln -s /home/ubuntu/Share/mApoSyl1_data/purged/purged.fa.gz
ln -s /home/ubuntu/Share/mApoSyl1_data/purged/purged.htigs.fa.gz
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



