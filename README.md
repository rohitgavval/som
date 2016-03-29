# som
Basic Self Organizing Map implementation for genome analysis.

This repository contains files for the thesis work titled "Self Organizing Map for genome analysis". The programs are provided here for purely academic purposes. Use them at your own risk. 

## som.c
Contains a basic implementation of Kohonen's SOM algorithm.

Usage:
```
$ som [-x NROWS] [-y NCOLS] [-e EPOCHS] [-a ALPHA0] [-s SIGMA0] [-o OUTPUTFILE] [-l LOG] [-r] INPUTFILE
```

## vector.c
Contains code to generate a vector representation of a genomic DNA sequence in fasta format. It calculates frequencies of dinucleotides. The resulting vector has dimension 16.

Usage:

```
$ cat input.fa | ./vector > output
```

## matrix.sh
Bash code to generate a matrix with the vector representations of a set of genomic sequences. By default it scans the subdirectory "genomes/Bacteria/", applies the program  `vector` on each fasta file, and stores each vector as a line in an output file. If there are N fasta files, the resulting matrix has dimension Nx16.

Usage:
```
$ bash matrix.sh
```


