Fix_models_RAxML
================

This repository contains modified codes of the master RAxML to make phylogenetic inferences fixing the model. At the moment it only works with nucleotide models.
It accepts models for single and multiple partitions.
Please read the information below.

Developed by:
 
Christopher Creevey
Teagasc, Grange, Dunsany, Co. Meath, Ireland.

and

Karen Siu-Ting
Bioinformatics and Molecular Evolution Lab, NUI Maynooth, Ireland.

------------------------------------------------------------------

Please note:
This version of RAxML was hacked from the original standard version that was posted in the github in June 2012. This has not been tried with posterior versions, however it might still work if you want to give it a go!
The changes in it from the original are in the models.c and optimisemodel.c codes. This works with any of the "flavors" of RAxML (serial, PTHREADS and MPI).

You need to copy the models.c and optimizeModel.c files in this repository and paste them instead of the ones that come in the original version. 
Then compile (install) as instructed in the manual (http://sco.h-its.org/exelixis/oldPage/RAxML-Manual.7.0.4.pdf)

1. raxmlHPC just the standard sequential version, compile it with gcc by typing make -f Makefile.gcc
for LINUX and MAC.
2. raxmlHPC-PTHREADS the Pthreads-parallelized version of RAxML which is intended for shared-memory
and multi-core architectures. It is compiled with the gcc compiler by typing make -f Makefile.PTHREADS
or make -f Makefile.PTHREADS.MAC on MACs.
3. raxmlHPC-MPI the MPI-parallelized version for all types of clusters to perform parallel bootstraps, rapid
parallel bootstraps, or multiple inferences on the original alignment, compile with the mpicc (MPI)
compiler by typing make -f Makefile.MPI.

To run it:

1. You need to create the files that contain the alpha parameter values, frequencies and rates. This can be done in any text editor, but should have the names and structure as explained below.

For example, for a file that contains 4 gene partitions, you generate 3 files called: "alpha.txt", "frequencies.txt" and "rates.txt".

file name: alpha.txt
contents should be all listed in 1 column, with no empty lines before or after the values and where each value corresponds to each partition (and follows the order of the partitions as entered with the -q option). It will look like this:

0.538444
0.405577
0.363449
0.550303

filename: frequencies.txt
contents should  be all listed in a matrix way, were each row of values corresponds to each partition (and follows the order of the partitions as entered with the -q option). Each row always has 4 columns, where each value corresponds to p(A), p(C), p(G) and p(T) respectively. It will look like this:

0.252	0.250	 0.246	  0.252
0.268	0.227	 0.242    0.263
0.278	0.261	 0.195    0.266
0.338	0.232	 0.183    0.246

Note: no empty lines should be left at the beginning or end, and values are separated by "tab".

filename: rates.txt
contents should be all listed in a matrix way, were each row of values corresponds to each partition (and follows the order of the partitions as entered with the -q option). Each row always has 6 columns, where value corresponds to the rates of a<->c, a<->g, a<->t, c<->g, c<->t, g<->t respectively. It will look like this:  

1.683840 5.748882  1.477863   0.988031	  7.5330760 1
0.896114 1.968979  0.570758   0.519740	  2.7715960 1
2.638182 8.011547  2.507338   1.308824	  16.254868 1
3.921128 7.321369  5.188662   0.757087	  19.758402 1

Note: no empty lines should be left at the beginning or	end, and values are separated by "tab".

2) Once you have all the 3 files (alpha.txt, frequencies.txt and rates.txt) created, place them all in the same folder where the input alignment and partition scheme are.

3) Call RAxML following the manual instructions. (you dont need to mention any of the parameter files we created in the command line, the program will call them internally).

ANOTHER OBSERVATION: If you plan to run this in several alignments with different parameter values, then create different folders for these alignments, and place them and each alpha.txt, frequencies.txt and rates.txt in their corresponding folder. Run them in each folder separately to avoid any confusion.

