# BLAST (Basic Local Alignment Search Tool)

You have assembled a partial set of Pacbio HiFi reads for *Apodemus sylvaticus*. 
Do you think you have just assembled some portions of *Apodemus sylvaticus*. nuclear genome? Or something special? Aren’t you curious? 

Let's do something fun to find out. Let’s do a stand-alone BLAST of our assembled contig.

We already have BLAST installed in our BIO5025 conda environment. If you do not have that conda environment activated yet, run:

```console
conda activate BIO5025
```

If `BIO5025` is activated, try:

```console  
blastn -h
```  
Has `blastn` returned some Usage information with a list of accepted parameters? If yes, great.
Next thing will be to make sure you are in your hifiasm assembly directory:

```console
cd ~/a_sylvaticus/hifiasm/

```
Right. So now we want to BLAST our contig to find out what it is. This means we need to blast them against a database of sequences we must think are present in our assembly. I have already created a database for you. It’s called `database.fasta`. 
So all you have to do is to format this database in the format blast understands and uses it. So you do:

```console  
cp path/database.fasta .
makeblastdb -in database.fasta -dbtype nucl
```

Now, list your directory. Have a look. Do you see different files with the database name but with specific blast file extensions (e.g. `*.nsq`, `*.nhr`)?

```console  
ls -ltrh
```  
Now that we have formated our database, let’s run blast. Blast has many parameters. We are going to run it twice to produce two types of output files. First run to generate a standard output:

```console  
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn -evalue 1e-05
```  

PS: here you should replace `<contigs_fasta>` by the assembly you've generated at the `Part 1 - Genome Assembly` tutorial. As you are blasting the hifiasm assembly, this file should be named `<species_id>.hifiasm.p_ctg.fa`. 

Now run it with an output format 6:

```console  
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn6 -evalue 1e-05 -outfmt 6
```

The command above will tell you the accession number of the subject sequences (i.e. the sequences in the database), then you can check on NCBI what those sequences are. Alternatively, you may change the `blastn` command to direcly print the title of the subject sequences in the output file (by replacing `-outfmt 6` by `-outfmt "6 std stitle"`):  

```console
blastn -query <contigs_fasta> -db database.fasta -out <contigs_fasta>.DB.blastn6_2 -evalue 1e-05 -outfmt "6 std stitle"
```

### Attention :grey_exclamation: 

The blast database files and the contigs must be in the same folder. If they aren’t you have some options: (i) you can specify the path to the target files, (ii) you can copy files (assembly or database) to the same folder, (ii) you can symlink files. If you get stuck let us know.

# Good.

So now let’s have a look at our outputs.

1-) Based on your blast results, what have you assembled? (If you don't understand the subject ID, search it on NCBI).

2-) Let’s inspect the differences between the two outputs

3-) What each column on the output `<contigs_fasta>.DB.blastn6` mean?  
    Here you can either google it or (even better) run `blastn -help` to see what the default columns for the `-outfmt` are. By exploring the `blast -help` output you can even discover some non-default options that you may find interesting to include in your future blast alignments outputs. 

Discuss this with your colleages and then let's discuss this as a group!
