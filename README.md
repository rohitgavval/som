# som
Basic Self Organizing Map (SOM) implementation for genome analysis.

This repository contains code files for the undergraduate thesis project titled "Self Organizing Map for genome analysis". This project aims to generate a clustering of bacterial genomes based on a structural representation of its DNA sequence.

The programs are provided here for purely academic purposes. Use them at your own risk. 

## vector.c
Contains code to generate a vector representation of a genomic DNA sequence in fasta format. It calculates frequencies of dinucleotides. The resulting vector has dimension 16.

Usage:

```
$ zcat INPUT.fna.gz | ./vector > OUTPUT
```

## matrix.sh
Bash script to generate a matrix with the vector representations of a set of genomic sequences. It scans the subdirectory with the compressed fasta sequences, applies the program  `vector` on each sequence, and stores each vector as a line in an output file. If there are N fasta files, the resulting matrix has dimension Nx16. This script is intended to run only once, to generate the input data file for the `som` program.

Usage:
```
$ bash matrix.sh
```
Relevant variables inside the script:
```
GENOMES: the subdirectory with the fasta sequences
MATRIX: the name of the output file
```
## som.c
Contains a basic general implementation of Teuvo Kohonen's SOM algorithm. It can be used on any dataset. 

Usage:
```
$ som [-x NROWS] [-y NCOLS] [-e EPOCHS] [-a ALPHA0] [-s SIGMA0] [-o OUTPUTFILE] [-l LOG] [-r] INPUTFILE
  -x NROWS: an integer number for the x dimension of the map
  -y NCOLS: an integer number for the y dimension of the map
  -e EPOCHS: number of epochs
  -a ALPHA0: a float number representing the initial learning factor
  -s SIGMA0: a float number for the initial sigma value, used to calculate the radius
  -o OUTPUTFILE: the name of the output file
  -l LOG: if 1, save a log of the run
  -r : if present, the next input vector will be selected randomly; if not, sequentially
  INPUTFILE: the name of the dataset file; the first line must contain the dimension of the inputs.
```
INPUTFILE is the data file generated by the `matrix.sh` script.

## plot.sh
Bash script to generate a simple 3D plot of the results. It sorts the som output file according to the label of the input vector, and plots each label with a different color. Requires `gnuplot`. 

Usage:
```
$ bash plot.sh SOMFILE
```
SOMFILE is the output file of the `som` program.

Relevant variables inside the script:
```
NUMCLUST: the number of clusters to show in the plot
PAUSE: if 0, save the plot directly to a PNG file; if 1, keep the gnuplot window open; default 1
LABELS: if 0, plot only the points and a legend separately; if 1, plot the labels in each point; default 1
```

Sample plots:

![genomes](https://github.com/chuseq/som/blob/master/genomes.png "Sample genomes clustering")
![genomes2](https://github.com/chuseq/som/blob/master/genomes2.png "Sample genomes clustering without labels")
![iris](https://github.com/chuseq/som/blob/master/iris.png "Sample IRIS data set clustering")

## wget.sh
Bash script to download the Bacteria FASTA files from the NCBI FTP site. Warning: only downloads "Complete Genome" files (aprox 5GB of hard disk space needed as of April 2016).

## sompak.sh
Bash script to run the programs in the [SOM_PAK](http://www.cis.hut.fi/research/som-research/nnrc-programs.shtml) package, with the data file generated with the `matrix.sh` script.

Usage:
```
$ bash sompak.sh
```
Relevant variables inside the script: DATADIR, DATAFILE, RESULTSDIR, LOGFILE, PATH

# Other SOM implementations

- [SOM_PAK](http://www.cis.hut.fi/research/som-research/nnrc-programs.shtml) package, from the very author of the SOM algorithm.
- R packages: [som](https://cran.r-project.org/web/packages/som), [kohonen](https://cran.r-project.org/web/packages/kohonen), [SOMbrero](https://cran.r-project.org/web/packages/SOMbrero).

# Author
Alfredo José Hernández Alvarez - chuseq@gmail.com
