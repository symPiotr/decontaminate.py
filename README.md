# decontaminate.py
This is a script for contaminant removal from amplicon libraries using information from a set of negative controls (blanks). Piotr Łukasik developed and tested the approach as a part of a mothur pipeline at some point in 2014, the script was developed in 2015 and modified a few times since. 

The scripts takes a mothur-generated count_table file as well as a list of blank (negative control) library names, and conducts a contaminant removal procedure as detailed below. Briefly, it removes from the count_table any unique genotypes UNLESS:
  (a) the ratio of the maximum relative abundance it attains in any experimental sample to the maximum relative abundance in any blank is above a threshold; and 
  (b) in at least one experimental library it attains a threshold relative abundance.

Next (c), the script removes any library which lost more than a threshold proportion of reads during steps (a) and (b), as well as all blank libraries. Then (d) the script repeats step (a) using the maximum relative abundance values calculated for the remaining experimental libraries. Finally, it outputs a .decontaminated.count_table file, suitable for downstream analysis using mothur.

Usage:
> decontaminate.py <count_table> <list_of_blanks> <ThresholdA; recommended value 10> <ThresholdB; recommended value 0.001> <ThresholdC; recommended value 0.3>

For example, 
> decontaminate.py Test.count_table Test_blanks.txt 10 0.001 0.3

Parameters:
-**<count_table>** Tab-delimited table produced by mothur's count.seqs() command. It must include experimental as well as blank libraries.
-**<list_of_blanks>** Text file with names of blank (negative control) libraries, one name per line.
-**<ThresholdA>** Value representing the threshold parameter for filtation step (a) above; a unique genotype will be removed UNLESS the maximum relative abundance it attains in at least one experimental library is more than ThresholdA * of the maximum relative abundance it attains in any blank library. Recommended value: 10
-**<ThresholdB>** Value representing the threshold parameter for filtation step (b) above; a unique genotype will be removed UNLESS the maximum relative abundance it attains in at least one experimental library is more than ThresholdB. Recommended value: 0.001
**<ThresholdC>** Value representing the threshold parameter for filtation step (c) above; an experimental library will be removed if it lost more than ThresholdC of the starting number of reads. Recommended value: 0.







Reference:
Łukasik P. et al. 2017: The structured diversity of specialized gut symbionts of the New World army ants. -
Molecular Ecology 26, 3808–3825  https://doi.org/10.1111/mec.14140
