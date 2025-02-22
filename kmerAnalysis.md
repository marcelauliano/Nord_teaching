# Hands on - Kmer analysis: running jellyfish

## Part 1

Right, so today you learned about how to analyse kmer composition of your genome sequenced reads. Now you are going to put your ‘Hands on’ data and will, yourself, count and analyse kmers. 
The species we are going to work with throughout the week is the European woodmouse *Apodemus sylvaticus*. The first thing you need to do is to create a working directory where you will run your analyses. My suggestion is to create a folder with your species name in your home directory (~/<species_name>/) and inside it, a series of other folders to structure your analyses. For example:

a_sylvaticus/  

a_sylvaticus/kmers/

a_sylvaticus/assembly/

The above basically means you have created a folder called ‘a_sylvaticus’ and inside it you have created two other folders side by side called ‘kmers’ and ‘assembly’. Let's go ahead and do it:

```console
# make a directory called a_sylvaticus
mkdir a_sylvaticus

# change directory to inside that folder
cd a_sylvaticus

# make two extra directory called kmers and assembly
mkdir kmers
mkdir assembly
```

Great, now that you have the folders, you need to copy the working data I pre-prepared for *Apodemus sylvaticus*. This data is located at <path_here>.

Now let's use the skills we learned yesterday and let's list what files are inside <path_here> folder. For that you should do:

```console
ls -ltrh <path_here> 
```

Do you see files and folders listed? If you do, then copy the mApoSyl1.60.HiFi.fasta file to the `kmers` directory you have created and move back to the `kmers` directory. The file mApoSyl1.60.HiFi.fasta is inside a subfolder called 'mApoSyl1_data'. We copy like this:

```console
cp mApoSyl1_data/mApoSyl1.60.HiFi.fasta <Path_to_your_folder>/a_sylvaticus/kmers/
cd <Path_to_your_folder>/a_sylvaticus/kmers/ 
ls -ltr
```

### Note :grey_exclamation: 

mApoSyl1 is the Darwin Tree of Life Project code for the species:

• mApoSyl1 - *Apodemus sylvaticus*

Now that you have created directories and copied the file to kmers, you need to activate your conda enviroment to be able to run the analyses today.
You do:

```
conda activate BIO5025
```

Your prompt should now look like:  

```bash  
(BIO5025) userX@IP-address:working_directory$
```
With the `BIO5025`environment active, try calling Jellyfish:

```console  
jellyfish --help
``` 

Do you see the help message? Great! (If not, call Laure!)

Jellyfish has many steps. The first one we'll run is the *count* to count kmers in our genomic reads. The kmer size we are going to use is 31. 

1-) Jellyfish count

So here comes the command:

```console  
jellyfish count -C -m 31 -s 1000 -t 1 -o mApoSyl1.60.jf mApoSyl1.60.HiFi.fasta
``` 

### Before we proceed

Please try:

```console  
jellyfish count --help 
```

on your command line to understand what are the parameters you have imputed in the previous line. Help messages are a useful way to understand what you are running, and to see if you would like to add any other parameter for your specific analysis case. Also remember that beyond this course, the internet is always on your side. If you google ‘jellyfish user guide’, for example, you will find [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Back to our data

2-) Jellyfish histo

Now that you have counted your 31-letters kmers, we want to transform it to a histogram file so that you can plot it. Then you have your second command:


```console  
jellyfish histo mApoSyl1.60.jf > mApoSyl1.60.histo
```

### Note :grey_exclamation: 

Note in the command above we have used the symbol “>” before the output. This is a command line symbol that will redirect your output to a file instead of printing it to the screen.

Note that the input for your command **jellyfish histo** is the output from your previous command, that was **jellyfish count**. Now you have the necessary result to plot a histogram on genomescope and have a look at the distribution of your genome kmers. 

### Let's plot

Download the file mApoSyl1.60.histo to your local machine (if you need help for that, we have instructions on downloading/uploading files in [this](https://eukaryotic-genome-assembly.github.io/logging_on/) tutorial), go to the [Genomescope](http://genomescope.org/genomescope2.0/) page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the mApoSyl1.60.histo file. 

Did you look at the distribution of kmer counts in the plot? Does it look ok? Does Genome scope says "Failed to Converge" ?

Ok, it looks like your kmer plotting didn't, work right? Well, why is that? Let's investigate a bit the file we are working on. Do you know, for example, how many reads are in the file mApoSyl1.60.HiFi.fasta? How can we find that out? One way if to grep the symbol ">" as we did yesterday. Let's do that.

```console
grep ">" mApoSyl1.60.HiFi.fasta | wc
```

With that we are grepping how many times the symbol ">" appears in the file, and we are sending thay information to the next command after the "|" which is "word count". 

What is the result of that command? How many sequences are there in the file?

But we can go further, we can calculate how many DNA bases there are in our reads. I have a script you can run to generate general statistics:

```console
export asmstats PATH
asmstats mApoSyl1.60.HiFi.fasta > mApoSyl1.60.HiFi.stats
```

Now look at the results. How many reads are there? How many bases in total (this will be under SUM)? 

We are working with a mouse genome. Can you go online and find out what is the average size of a mouse genome? You will find out that with the reads you have worked so far, you have not enough coverage of the mouse genome represented, that is why it fails to converge. You have ran into a case where your amount of reads are not enough to plot a kmer plot.

## Part 2

But nothing to worry about. I have ran jellyfish for a complete set of reads for 


, and genomescope has calculated for your (i) the estimated genome size, (ii) the heterozygosity and (iii) the percentage of repeats of your species genome. 

The histogram you have just plotted is for a jellyfish count of the **total** PacBio HiFi reads sequenced to assemble your species. We have generated it for you because it takes time. However, when you are back to real life and need to run it for your sample, you will run the same commands ran for the subsample (`*600.fasta`) as you just did! =) Yeah!! 



# BUT STOP!

# STOP STOP! 

...

Before you plot this result, I want you to plot a genomescope plot for another file FIRST!! 

Inside the shared directory for your species (`/home/ubuntu/Share/<species-Code>_data/`), you are going to find two files called:

```console  
<species>.ccs.total.fasta.gz
<species>.total.histo
```

Download the file \<species\>.total.histo to your local machine (if you need help for that, we have instructions on downloading/uploading files in [this](https://eukaryotic-genome-assembly.github.io/logging_on/) tutorial), go to the [Genomescope](http://genomescope.org/genomescope2.0/) page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the \<species\>.total.histo file, and genomescope has calculated for your (i) the estimated genome size, (ii) the heterozygosity and (iii) the percentage of repeats of your species genome. 

The histogram you have just plotted is for a jellyfish count of the **total** PacBio HiFi reads sequenced to assemble your species. We have generated it for you because it takes time. However, when you are back to real life and need to run it for your sample, you will run the same commands ran for the subsample (`*600.fasta`) as you just did! =) Yeah!! 








you need to go and copy the working data for your species. The data will be inside /home/ubuntu/Share/



I have raw reads and pre-processed data you need to transfer or symlink to your wok


Need to have a slide on 
how to connect to the machine from mac and windows, 
how to download files with scp and from windows.

















Where? /home/marcela/bIO5025/
1-) Run jelly fish count and hist for small dataset.
2-) asmstats and plot read distribution.

Now work with the pre-processed data for the whole dataset.
Need to run asmstats again to get to 20 something times coverage. done
need to get the plot of the reads distribution

bLAST




