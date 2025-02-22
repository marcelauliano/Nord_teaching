# Hands on - Kmer analysis: running jellyfish

Right, so today you learned about how to analyse kmer composition of your genome sequenced reads. Now you are going to put your ‘Hands on’ data and will, yourself, count and analyse kmers. 
The species we are going to work with throughout the week is the European woodmouse *Apodemus sylvaticus*. The first thing you need to do is to create a working directory where you will run your analyses. My suggestion is to create a folder with your species name in your home directory (~/<species_name>/) and inside it, a series of other folders to structure your analyses. For example:

a_sylvaticus/  

a_sylvaticus/kmers/

a_sylvaticus/assembly/

The above basically means you have created a folder called ‘a_sylvaticus’ and inside it you have created two other folders side by side called ‘kmers’ and ‘assembly’. Let's go ahead and do it:

```
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

```
ls -ltrh <path_here> 
```

Do you files and folders listed? If you do, then copy the mApoSyl1.60.HiFi.fasta file to the `kmers` directory you have created and move back to the `kmers` directory. The file mApoSyl1.60.HiFi.fasta is inside a subfolder called 'data'. Like this:

```
cp mApoSyl1_data/mApoSyl1.60.HiFi.fasta <Path_to_your_folder>/a_sylvaticus/kmers/
cd <Path_to_your_folder>/a_sylvaticus/kmers/ 
ls -ltr
```


This data folder also contains some subdirectories, such as the one called kmers, which is where some of the data we need for today is located. You can ```ls -ltrh``` inside that directory as well.

```
ls -ltrh <path_here>/kmers
```




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




