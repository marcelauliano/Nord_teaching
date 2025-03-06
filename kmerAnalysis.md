# Hands on - Kmer analysis: running jellyfish

## Part 1

Right, so today you learned how to analyse kmer composition of your genome sequenced reads. Now you are going to put your ‘Hands on’ data and will, yourself, count and analyse kmers. Exciting! 
The species you are going to work with throughout the week is the European woodmouse *Apodemus sylvaticus*. The first thing you need to do is to create a working directory where you will run your analyses. My suggestion is to create a folder with your species name in your home directory (~/<species_name>/) and inside it, a series of other folders to structure your analyses. For example:

a_sylvaticus/  

a_sylvaticus/kmers/

a_sylvaticus/assembly/

The above basically means you have created a folder called ‘a_sylvaticus’ and inside it you have created two other folders side by side called ‘kmers’ and ‘assembly’. Let's go ahead and do that:

```console
# make a directory called a_sylvaticus
mkdir a_sylvaticus

# change directory to inside that folder
cd a_sylvaticus

# make two extra directory called kmers and assembly
mkdir kmers
mkdir assembly
```

Great, now that you have the folders, you need to copy the working data I pre-prepared for *Apodemus sylvaticus*. This data is located at /home/marcela/mApoSyl1_data.

Now let's use the skills you learned yesterday and let's list what files are inside the ```mApoSyl1_data``` folder. For that you should do:

```console
ls -ltrh /home/marcela/mApoSyl1_data
```

Do you see files and folders listed? If you do, then copy the file ```the mApoSyl1.60.HiFi.fasta``` to the `kmers` directory you have created and move back to the ```kmers``` directory. The file ```mApoSyl1.60.HiFi.fasta``` is inside a subfolder called ```mApoSyl1_data```. As an example, with you are user1, you copy it like this:

```console
cp /home/marcela/mApoSyl1_data/mApoSyl1.60.HiFi.fasta /home/user1/a_sylvaticus/kmers/
cd /home/<your_user_name_here>/a_sylvaticus/kmers/ 
ls -ltr
# do you see the file mApoSyl1.60.HiFi.fasta ? Great!
```

### Note :grey_exclamation: 

**mApoSyl1** is the Darwin Tree of Life Project code for the species *Apodemus sylvaticus*

Now that you have created directories and copied the file to kmers, you need to activate your conda enviroment to be able to run the analyses today.
You do:

```
conda activate BIO5025
```

Your prompt should now look something like:  

```bash  
(BIO5025) user1@lmj-2022-02:~/a_sylvaticus/kmers$
```
Now, with the `BIO5025`environment actived, try calling Jellyfish:

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

### Before you proceed

Please try:

```console  
jellyfish count --help 
```

on your command line to understand what are the parameters you have imputed in the previous line. Help messages are a useful way to understand what you are running, and to see if you would like to add any other parameter for your specific analysis case. Also remember that beyond this course, the internet is always on your side. If you google ‘jellyfish user guide’, for example, you will find [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Back to our data

2-) Jellyfish histo

Now that you have counted your 31-letters kmers, we want to transform it to a histogram file so that you can plot it. 
For that, you have your second command:


```console  
jellyfish histo mApoSyl1.60.jf > mApoSyl1.60.histo
```

### Note :grey_exclamation: 

Note in the command above we have used the symbol “>” before the output. This is a command line symbol that will redirect your output to a file instead of printing it to the screen.

Note that the input for your command **jellyfish histo** is the output from your previous command, that was **jellyfish count**. Now you have the necessary result to plot a histogram on genomescope and have a look at the distribution of your DNA kmers. 

### Let's plot

Download the file mApoSyl1.60.histo to your local machine (if you need help for that, we have instructions on downloading/uploading files in [this](https://github.com/marcelauliano/Nord_teaching/blob/main/Connecting_downloading.md) tutorial), go to the [Genomescope](http://genomescope.org/genomescope2.0/) page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Example of downloading for a user1

```console
scp user1@52.138.157.130:/home/user1/a_sylvaticus/kmers/mApoSyl1.60.histo .
```


Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the mApoSyl1.60.histo file. 

Did you look at the distribution of kmer counts in the plot? Does it look alright? Or does Genome scope says "Failed to Converge" ?

Ok, it looks like your kmer plotting didn't work, right? Yeah... Well, why did that happen? 
Let's investigate a bit the file we are working on. 
Do you know, for example, how many reads are in the file ```mApoSyl1.60.HiFi.fasta```? How can you find that out? One way if to grep the symbol ">" as we did yesterday. Let's do that.

```console
grep ">" mApoSyl1.60.HiFi.fasta | wc
```

With that we are grepping how many times the symbol ">" appears in the file, and we are sending that information to the next command after the "|" which is "word count". 

What is the result of that command? How many sequences are there in the file?

But we can explore further, we can calculate how many DNA bases there are in our read set. I have a script you can run to generate this general statistics:

```bash
export PATH=$PATH:/home/marcela/scripts/
asmstats mApoSyl1.60.HiFi.fasta > mApoSyl1.60.HiFi.stats
```

Now look at the results. How many reads are there? How many bases in total (this will be under SUM)? 

We are working with a mouse genome. Can you go online and find out what is the average size of a mouse genome? You will find out that with the reads you have worked so far, you don't have enough coverage of the mouse genome represented, that is why it fails to converge. You have ran into a case where your amount of reads are not enough to plot a kmer plot distribution.

## Part 2

But nothing to worry about. I have ran jellyfish for a complete set of reads for your species and you can plot those now. In order to do that, you need to copy other files from our shared data folder. Let's do that:

```
pwd
# where are you? If you are inside your kmers folder, that is good. Otherwise change there
```

Now copy the files

```console
cp /home/marcela/mApoSyl1_data/mApoSyl1.all.HiFi.stats . 
cp /home/marcela/mApoSyl1_data/mApoSyl1.all.HiFi.k31.histo . 
cp /home/marcela/mApoSyl1_data/mApoSyl1.all.HiFi.readsLength.png .
```

Download the file ```mApoSyl1.all.HiFi.k31.histo``` to your local machine as you did before and go to the [Genomescope](http://genomescope.org/genomescope2.0/) page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the ```mApoSyl1.all.HiFi.k31.histo``` file, and Genomescope has calculated for your (i) the estimated genome size, (ii) the heterozygosity and (iii) the percentage of repeats of your species genome. 

## Now
You have also copied a file called ```mApoSyl1.all.HiFi.stats``` which is the statistics for the total reads I have ran for you. You need this file to understand your dataset and calculate genome sequenced coverage. Another file you have copied is a plot of reads length distribution called ```mApoSyl1.all.HiFi.readsLength.png```. I want you to download this file to your local machine.

 # Now, let's finish and interprete everything. Answer the following questions:

You have now the kmer plot, reads statistics and kmer reads plot distribution for your complete PacBio HiFi read set. Which conclusions can you draw from these results?

Is the kmer distribution fitting the model? If yes, then

a- What is the expected genome size of *Apodemus sylvaticus*?

b- What is the estimated heterozygosity?

c- What is the estimated repeat content?

d- Taking into consideration the estimated genome size, and the statistics of the total reads you have, how much read coverage you have to assemble this genome?
 

# Considering the small dataset from which you counted kmers:

e- How do the observed and model curves compare now that you are analysing just a handful of sequences? How about the Model Fit values?

f- Looking at the asmstats result for this smaller file, how much coverage of the genome you have in this file giving the estimated genome size from the kmer plot of the total file?


You can also plot the reads length distribution for this smaller file. Let's do that with a script which will print the distribution to the screen.

```
ln -s /home/marcela/scripts/plot_readsLength_screen.py
python plot_readsLength_screen.py mApoSyl1.60.HiFi.fasta

```

Great. Now let’s look at it all together: considering the kmer plot of the total file and its statistics, we can have a good look at the kmer composition of the DNA in this genome. How does it look? Discuss with your partners and then later in the big group.

### One last comment :grey_exclamation: 

## Plotting reads length distribution

Imagine if we have a good genome coverage but our reads are all small? It would not be very useful to assemble across repeats. This is why its always a general practice to have the length distribution of your reads plotted before you start assembling.







