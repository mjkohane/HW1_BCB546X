#UNIX Assignment

\##Data Inspection

\###Attributes of `fang_et_al_genotypes`



`wc fang_et_al_genotypes`

The fang file contains 2783 lines, 27744038 and 11051939 bytes of information.

`ls -lh fang_et_al_genotypes`

In using this command, I determined the size of the file was 11MB, this is a very large file and I am sure there are much larger!

`head fang_et_al_genotypes`

Running this command does nothing but confuse the reader, thus there are needed steps to transform the data for better understanding and analysis.

Now to determine the number of columns in the fang file:

`awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt`

In running this we determine that there is a total of 986 total columns, the huge amount of columns is what is making our file apparently unreadable.

Duplicating these commands on the snp.position.txt file:

`wc snp_position.txt`

Shows that the snp_position.txt file contains 984 words, 13190 lines and 82763 bits of information.

`ls -lh snp_position.txt`

Results in 81KB.

`awk -F "\t" '{print NF; exit}' snp_position.txt`

Results in 15 total columns.

Now to process the data.



##Extra Steps:

Made directories for bother maize and teosinte, keep everything in order and store the final files.

`mkdir maize` & `mkdir teosinte`



##Data Processing

###SNP_position 



`grep "SNP_ID" snp_position.txt > SNP_headers.txt`

Removal of the headers in the SNP file and sent to a new file titled SNP_headers.txt



`cut -f 1,3,4 snp_position.txt > data_snp_position.txt`

Removes unimportant data, saving simply the chromosome and locations of nucleotides into a new file named data_snp_position.txt

##Maize:

`grep "SNP_ID" fang_et_al_genotypes.txt > maize_genotypes.txt`

This command was used to remove the maize genotypes and save them separately.



`grep "ZMM[IL,LR,MR]" fang_et_al_genotypes.txt >> maize_genotypes.txt`

This command was used to append the groups that we are looking for the the separate file, maize_genotypes.txt.



`awk -f transpose.awk maize_genotypes.txt > transposed_maize_genotypes.txt`

Now, we transpose the maize_genotype.txt file and save as a new file named transposed_maize_genotypes.txt.



Now to join the files:

`join -1 1 -2 1 data_snp_position.txt transposed_maize_genotypes.txt > joined_maize_genotypes.txt`

Completed!



Now, we move our joined files into their respective folders:

`mv joined_maize_genotypes.txt maize` 



In this folder we will make 3 more directories for the information of Increasing and Decreasing SNP position and an extra directory for whatever else turns up.

`mkdir Increasing_SNP_position` `mkdir Decreasing_SNP_position`  `mkdir extras`



Copied our join_maize_genotypes.txt into the respective directions based on increasing and decreasing values, while replacing the "?" characters to "-" for the needs of our assignment.

`sed 's/?/-/g' joined_maize_genotypes.txt > Decreasing_SNP_position/decreasing_joined_maize.txt`



`grep "unknown" joined_maize_genotyes.txt > unknown_maize.txt`

`grep "multiple" joined_maize_genotypes.txt > multiple_maize.txt`

Created two new files containing the unknown and multiple position data.

















``





##Teosinte:

The above commands were duplicated, but now for the teosinte information that we need to analyze.

`grep "SNP_ID" fang_et_al_genotypes.txt > teosinte_genotype.txt`

This command was used to remove the teosinte genotypes and save them separately.

`grep "ZMP[JA,IL,BA]" fang_et_al_genotypes.txt >> teosinte_genotype.txt`

This command was used to append the groups that we are looking for the the separate file, maize_genotypes.txt.

`awk -f transpose.awk teosinte_genotype.txt > transposed_teosinte_genotypes.txt`

Now, we transpose the maize_genotype.txt file and save as a new file named transposed_maize_genotypes.txt.

Now to join the files:

`join -1 1 -2 1 data_snp_position transposed_teosinte_genotypes.txt > joined_teosinte_genotypes.txt`

Completed!

Now, we move our joined files into their respective folders:

 `mv joined_teosinte_genotypes.txt teosinte`



In this folder we will make 3 more directories for the information of Increasing and Decreasing SNP position and an extra directory for whatever else turns up.

`mkdir Increasing_SNP_position` `mkdir Decreasing_SNP_position`  `mkdir extras`



Copied our join_maize_genotypes.txt into the respective directions based on increasing and decreasing values, while replacing the "?" characters to "-" for the needs of our assignment.

`sed 's/?/-/g' joined_teosinte_genotypes.txt > Decreasing_SNP_position/decreasing_joined.teosinte.txt`



`grep "unknown" joined_teosinte_genotyes.txt > unknown_teosinte.txt`

`grep "multiple" joined_teosinte_genotypes.txt > multiple_teosinte.txt`

Created two new files containing the unknown and multiple position data.







\###Maize Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does

```



$ awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt

[mjkohane@hpc-class HW1_BCB546X]$ grep "Sample_ID" fang_et_al_genotypes.txt > fang_IDs.txt

[mjkohane@hpc-class HW1_BCB546X]$ grep -v "Sample_ID" fang_et_al_genotypes.txt > fang_data.txt


```



By inspecting this file I learned that:

1. point 1
2. point 2
3. point 3

or

- point 1
- point 2
- point 3

\###Attributes of `snp_position.txt`

```
here is my snippet of code used for data inspection

[mjkohane@hpc-class HW1_BCB546X]$ grep "SNP_ID" snp_position.txt < snp_headers.txt

[mjkohane@hpc-class HW1_BCB546X]$ grep -v "SNP_ID" snp_position.txt > snp_locations.txt

[mjkohane@hpc-class HW1_BCB546X]$ sort -k1,1n snp_position.txt > sorted_snp.txt

```

By inspecting this file I learned that:

1. point 1
2. point 2
3. point 3

or

- point 1
- point 2
- point 3

##Data Processing

\###Maize Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does

\###Teosinte Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does
