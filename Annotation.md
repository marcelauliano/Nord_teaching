# Working with the annotation of *Apodemus sylvaticus*

We just discussed annotation and some of the output formats that come out of annotation pipelines. Now we will have a look at the annotation done on *Apodemus sylvaticus* by the [NCBI Eukaryotic Annotation Pipeline](https://www.ncbi.nlm.nih.gov/refseq/annotation_euk/all/).

I have downloaded 2 files from the NCBI for us to work with, but I also encourage you have have a look at their [FTP server](https://ftp.ncbi.nlm.nih.gov/genomes/all/annotation_releases/10129/GCF_947179515.1-RS_2023_02/), other files are available there. 

The main files we are going to look at is a gff file and a fasta file of predicted proteins.
Make an annotation folder in your work directotry and copy and symlink files there:

```console
cd ~/a_sylvaticus/
mkdir annotation
cd annotation
cp path/annotation/GCF_947179515.1_mApoSyl1.1_genomic.gff .
cp path/annotation/GCF_947179515.1_mApoSyl1.1_protein.faa .
```
Cool, now let's da a quick manipulation of these files just to get a sense of them. 
Let's say I want to understand how many genes of "Heat shock protein beta 2" there are annotated in this genome. What do I do? I can have a quick look at the gff file.

I can, for example, grep that name from the gff file. Let's do that

```console
grep "heat shock protein beta-2" GCF_947179515.1_mApoSyl1.1_genomic.gff
```

But instead of just letting it print to the screen, let's save it to a file.

```console
grep "heat shock protein beta-2" GCF_947179515.1_mApoSyl1.1_genomic.gff > mApoSyl1.hspbeta2.gff
```
Now let's have a look at this file.
How many different isoforms of Heat shock protein beta-2 were predicted in this genome?
You can do this inspection by eye because the file is small with less.

```console
less mApoSyl1.hspbeta2.gff
```

But you can also use a oneliner to inspect this:

```console
awk -F'product=' '$2 {split($2, a, ";"); products[a[1]]++} END {for (p in products) print p}' mApoSyl1.hspbeta2.gff
```




