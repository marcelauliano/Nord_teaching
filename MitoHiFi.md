# MitoHiFi - Background
Ok, so on the second day of our course you have assembled the mitogenome of your species with Hifiasm.
Well, the contigs are the mitochondria, but they don't represent a final mitochondrial sequences we usually find on databases, right? 
The contig size outputed by Hifiasm if much larger than a mitogenome usually is. True! This happens because of the circular nature of the molecule, 
and because of how assemblers work! Basically: the overlaps of the circular molecule makes the assembler confused and they end up concatenating 
the circular molecule multiple times, so you end up having an assembly with a repetion in both ends.

To solve this problem, I have written a pipeline that can assemble and annotation a mitochondrial genome for you! It's called MitoHiFi as you heard on the lecture.
For more information on MitoHifi, have a look here: https://github.com/marcelauliano/MitoHiFi 

Now, let's run MitoHiFi for our assembled Hifiasm contig from day 2. We will use a docker container for this run.

First let's create a directory for our mitochondrial run:

```console
cd ~/a_sylvaticus/
mkdir mitochondria
cd mitochondria
```

Now let's copy or symlink your hifiasm contig from Day 2 to ourt folder

```console
cp path/hifiasm/<prefix>.p_ctg.fa .
```

## Finding a related mitogenome  
To run MitoHiFi, first you need a close-related mitochondria in fasta and genbank format. We have a script that can help you find this input. Giving the name of the species you are assembling, the script is going to look for the closest mitochondria it can find on NCBI. You can give the parameter `-s` to the script if you would like to restrict your mitochondria search for species within your given genus, but this means the script can download partial mitochondrial sequences. Otherwise, without `-s`, the script is going to search for complete mitochondrias only and as close as possible to your species on interest.

Let's find a close-related mitochondria for our run:

```console
sudo docker run -v $(pwd):/output ghcr.io/marcelauliano/mitohifi:master findMitoReference.py --species "Apodemus sylvaticus" --outfolder . --min_length 12000
```

Finally, run MitoHiFi for the contigs test dataset: 

```console  
python mitohifi.py -c test.fa -f refData/OQ830676.1.fasta -g refData/OQ830676.1.gb -t 1 -o 5
```

The pipeline will probably take a few minutes to run. Once it's done, it will output a message saying `Pipeline finished!`.

Questions:  
1) What's the meaning of each parameter used to run MitoHiFi? Hint: if in doubt, run `python mitohifi.py -h` and/or check the official MitoHiFi documentation at [github](https://github.com/marcelauliano/MitoHiFi).    
2) Has MitoHiFi succeded creating final mitogenome fasta/genbank files? What are the names of those files?  
3) Open the final mitogenome genbank file and answer: i) what's the total length of the mitogenome?; ii) what's the first gene in that mitogenome?  
4) Go to BLAST [webserver](https://blast.ncbi.nlm.nih.gov/Blast.cgi) and do a blastn of the final mitogenome fasta file (`final_mitogenome.fasta`) against the Nucleotide collection (nr/nt). What's the first hit you get from the alignment? What species does that hit come from? Click on the hit accession number hyperlink. You should be redirected to a new page. Go to the `COMMENT` section and answer: how was this sequence assembled?    
5) Open the `contigs_stats.tsv` file and answer: is there another mitogenome assembly besides the final_mitogenome? 
 
We can discuss the results together. =)
