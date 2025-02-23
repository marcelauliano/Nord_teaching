# Chromating conformation capture Hi-C

Right, so now you have learned about Chromating conformation capture and scaffolding genomes with the Hi-C technology. Today you are going to evaluate results generated 
by two scaffolding tools: (i) [SALSA2](https://github.com/marbl/SALSA) and (ii) [YaHS](https://github.com/c-zhou/yahs). 

Because we don't have time to run the whole command during the course (it can take days), I have generated both results for you for our species *Apodemus sylvaticus*. 

Today you will evaluate the outpus of YAHS and salsa, merqury results and BUSCO results, as well as generate the assemnbly general statistics for the primary genome after yaHS scaffolding. You will also interprete the agp output result and inspect the HiC heatmap created.

Let's create a folder in your working directory where you will be working on scaffold results:

```console
mkdir ~/a_sylvaticus/scaffolding
cd ~/a_sylvaticus/scaffolding
```

Now let's copy and symlink files from Salsa and yaHS outputs.

```console
# First let's symlink Salsa scaffolded output
cd ~/a_sylvaticus/scaffolding
ln -s path/scaffolding/mApoSyl1.salsa.fasta.gz .
# let's copy the BUSCO output for salsa
cp path/scaffolding/mApoSyl1.busco.salsa.short_summary.txt .
# and let's copy the pretext map file for salsa
cp path/scaffolding/mApoSyl1.salsa.pretext .
```

Now run the script to output the general statistics for the salsa-scaffolded assembly:

```console
export PATH=$PATH:/home/ubuntu/Share/scripts
conda activate BIO5025
cd ~/a_sylvaticus/scaffolding
asmstats mApoSyl1.salsa.fasta.gz > mApoSyl1.salsa.stats
```

Great, so now let's gather all the results for the yaHS-scaffolded assembly:

```console
# First let's symlink yaHS scaffolded output
cd ~/a_sylvaticus/scaffolding
ln -s path/scaffolding/mApoSyl1.yahs.fasta.gz .

# let's copy the BUSCO output for yaHS
cp path/scaffolding/mApoSyl1.busco.yahs.short_summary.txt .

# and let's copy the pretext map file for yahs
cp path/scaffolding/mApoSyl1.yahsa.pretext .

# For yaHS, let's also copy the agp file output
cp path/scaffolding/mApoSyl1.yahs.agp .
```

Now run the general statistics for the scaffolded yaHS assembly

```console
asmstats mApoSyl1.yahs.fasta.gz > mApoSyl1.yahs.stats
```

Now I also want you to open the pretext file for salsa and yaHS. Make screeshots of the images and put them in your slides (presentation).

Using PretextView
After opening PretextView, click on the Load Map button and then select the downloaded *.pretext file.

### Now
Analyze all the results, discuss with your team and answer the questions in your presentation:

1-) What are the assembly statistics before scaffolding?

2-) What are the assembly statistics after scaffolding with salsa?

3-) What are the assembly statistics after scaffolding with yaHS?

4-) What are the BUSCO outputs for salsa and yaHS?

5-) How is the heatmap of salsa and yaHS looking?

6-) Which heatmap has more off-diagonal signal? And why?

7-) Considering the heatmap, general statistics and BUSCO results, which software has done a better job at scaffolding: salsa or yaHS and why?

8-) Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

The [agp file](https://www.ncbi.nlm.nih.gov/genbank/genome_agp_specification/) gives us the coordinates of what contig has been included in each final scaffold in a run. If contigs were broken, it shows that as well. 

Take a few minutes to look at your agp file together with [the description on NCBI](https://www.ncbi.nlm.nih.gov/genbank/genome_agp_specification/) and try to understand it.

```console
# have a look at the agp file from yaHS
cd ~/a_sylvaticus/scaffolding
less mApoSyl1.yahs.agp
```

Now, 

How could we, for example, count of how many contigs and how many gaps is ```scaffold_1``` made of? 

I have a oneliner for you:

```console
awk '$1 == "scaffold_1" { if ($5 == "W") contigs++; else if ($5 == "N") gaps++ } END { print "Contigs:", contigs, "\nGaps:", gaps }' mApoSyl1.yahs.agp
```

The explanation of the awk command is:

* ```$1``` == ```scaffold_1``` → Selects only lines related to scaffold_1.
* ```if ($5 == "W") contigs++``` → Increments contig count when column 5 is W.
* else ```if ($5 == "N") gaps++``` → Increments gap count when column 5 is N.
* ```END { print "Contigs:", contigs, "\nGaps:", gaps }``` → Prints the final count.


After that, come back to the wider group.
