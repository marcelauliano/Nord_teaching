# Chromosome conformation capture Hi-C

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you are going to evaluate results generated 
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

