# Final curated assembly results

So here we are. I don't know if you realized but you have come a long way this week. You have learned:

i) How to count and plot Kmers to understand genome composition (heterozygosity, genome size, repeat content)

ii) You have assembled your genome with hifiasm

iii) You have learned about purging genomes to exclude retained haplotypes

iv) You have learned how to evaluate genome quality with (i) kmers (Merqury, (ii) general statistics and (iii) BUSCO

v) You have learned how to interprete Hi-C scaffolding with Salsa and yaHS

Look at that? Thats is A LOT! WELL DONE! :clap: 

# Now,

Let's look at the final manually curated assembly. 
Before you look at the files, I want you to check this publication [here](https://wellcomeopenresearch.org/articles/8-442/v1). This is the genome note for the curated assembly you are working on. It is already published (general statistics might vary slighlty with the one you have). 

Now, you will manipulate the final statistics for the curated genome and update this on your group's final presentation.
Let's get the curated genome final statistics:

```console
cd ~/a_sylvaticus/
mkdir curated

# Now let's copy and symlink final curated results to this folder

cp /home/marcela/mApoSyl1_data/curated/mApoSyl1.1.primary.stats .
cp /home/marcela/mApoSyl1_data/curated/mApoSyl1_curated.pretext.gz .
cp /home/marcela/mApoSyl1_data/curated/mApoSyl1_curated_BUSCO.short-summary.txt .
```

Download the curated HeatMap and open it on pretext.

So now that you have the curated statistics, a BUSCO run for it and the final curated Hi-C heatmap, I want you to gather ALL the results for your species that you have ran during the week and make a final presentation answering all the questions bellow:

     1\. What is the name of your species? And what else have you learned online for it (do a small search to find a picture and maybe some interesting evolutionary facts about it)?

     2\. What is the genomescope plot for the TOTAL Pacbio HiFi reads histogram? What is the expected genome size? What is the expected heterozygosity? What is the estimated repeat content?

     3\. How does the reads plot length distribution looks like? What is the average read length that was inputted to assembly?

     4\. What are the statistics for the Hifiasm total reads primary assembly? What is the merqury qv? The completeness? How does busco looks like?

     5\. What are the statistics for the assembly before and after purging? What are the qvs? Completeness? How does busco looks like before and after purging?

     6\. What is the primary genome statistics just before yaHS scaffolding?

     7\. What is the primary genome statistics after yaHS scaffolding? How does the Hi-C heat map looks like?

     8\. What is the primary genome statistics after manual curation? How does the Hi-C heat map looks like? 
    
     9\. How are the BUSCO results before and after curation? Has it changed much? 
    
     10\. What is the QV diference of the primary genome (i) after purging and (iii) after scaffolding? 

     11\. For the subset of reads you have assembled for your species. Which kind of reads were they? What have you assembled there? What your blast result looks like?

   
WELL DONE! 

You have a robust knowlegde and skill set to perform eukaryotic genome assembly using Pacbio HiFi and Hi-C!!


##########
