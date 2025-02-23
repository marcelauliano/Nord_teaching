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

Now let's copy or symlink your hifiasm contig from day 2 to that folder

```console
cp path/hifiasm/<prefix>.p_ctg.fa .
```
