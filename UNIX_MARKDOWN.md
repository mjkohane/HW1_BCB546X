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

------

##Extra Steps:

Made directories for both maize and teosinte, keep everything in order and store the final files.

`mkdir maize` & `mkdir teosinte`

------

##Data Processing

###Maize

`grep "Group" fang_et_al_genotypes > maize_genotypes.txt`

Removal of the headers in the SNP file and sent to a new file titled maize_genotypes.txt.

```
grep "ZMM[IL,LR,MR]" fang_et_al_genotypes.txt >> maize_genotypes.txt
```

Appendage of important header data to the maize_genotypes.txt file.



```
awk -f transpose.awk maize_genotypes.txt > transposed_maize.txt
```

Now we transpose the maize_genotypes.txt file, this is not stored as transposed_maize.txt.

I used vi to change Sample_ID to SNP_ID so that the data can be correctly matched.

```
cut -f 1,3,4 snp_position.txt > maize_snp_position.txt
```

The command above was used to remove unimportant data, and save the important data into maize_position.txt

```
join -1 1 -2 1 maize_position.txt transposed_maize_genotypes.txt > joined_maize.txt
```

Now we join the files and observe. 

Everything is looking in order so far...



Now to create files for individual chromosomes:

`awk '$2 ==1' joined_maize.txt > maize_chr1.txt`

This has created a file for the first chromosome of the maize data, now to filter it in increasing and decreasing order, and make 9 more!



Sorting:

```
sort -k3,3n maize_chr1.txt > forward_maize_chr1.txt
```

Forward sort ^

This can be more efficient using piping:

`awk '$2 == 2' joined_maize.txt | sort -k3,3n > forward_maize_chr2.txt`



`sort -k3,3nr maize_chr1.txt > reverse_maize_chr1.txt`

Reverse sort ^

This can be more efficient using piping:

`awk '$2 == 2' joined_maize.txt | sort -k3,3nr > reverse_maize_chr2.txt`



Now things are sorted, but now to deal with unknown and multiple position data:

`awk '$2 == "unknown"' joined_maize.txt > unknown_maize.txt`

Unknown positions taken care of ^

 `awk '$2 =="multiple"' joined_maize.txt > multiple_maize.txt`

Multiple positions taken care of ^



Now just to change missing data in the reverse sorted files:

`sed -i 's/?/-/g' reverse_maize_chr1.txt`

This command will be distributed onto all the reverse chromosomes.

------

##Teosinte:

Everything from above will be duplicated but now for the teosinte data and information.

grep "Group" fang_et_al_genotypes > maize_genotypes.txt`

Removal of the headers in the SNP file and sent to a new file titled maize_genotypes.txt.

```
grep "ZMP[JA,IL,BA]" fang_et_al_genotypes.txt >> teosinte_genotypes.txt
```

Appendage of important header data to the teosinte_genotypes.txt file.



```
awk -f transpose.awk teosinte_genotypes.txt > transposed_teosinte.txt
```

Now we transpose the teosinte_genotypes.txt file, this is not stored as transposed_teosinte.txt.

I used vi to change Sample_ID to SNP_ID so that the data can be correctly matched.

```
cut -f 1,3,4 snp_position.txt > teosinte_snp_position.txt
```

The command above was used to remove unimportant data, and save the important data into maize_position.txt

```
join -1 1 -2 1 teosinte_position.txt transposed_teosinte_genotypes.txt > joined_teosinte.txt
```

Now we join the files and observe. 

Everything is looking in order so far...



Now to create files for individual chromosomes:

`awk '$2 ==1' joined_teosinte.txt > teosinte_chr1.txt`

This has created a file for the first chromosome of the teosinte data, now to filter it in increasing and decreasing order, and make 9 more!



Sorting:

```
sort -k3,3n teosinte_chr1.txt > forward_teosinte_chr1.txt
```

Forward sort ^

This can be more efficient using piping:

`awk '$2 == 2' joined_toesinte.txt | sort -k3,3n > forward_teosinte_chr2.txt`



`sort -k3,3nr teosinte_chr1.txt > reverse_teosinte_chr1.txt`

Reverse sort ^

This can be more efficient using piping:

`awk '$2 == 2' joined_teosinte.txt | sort -k3,3nr > reverse_teosinte_chr2.txt`



Now things are sorted, but now to deal with unknown and multiple position data:

`awk '$2 == "unknown"' joined_teosinte.txt > unknown_teosinte.txt`

Unknown positions taken care of ^

 `awk '$2 =="multiple"' joined_teosinte.txt > multiple_teosinte.txt`

Multiple positions taken care of ^



Now just to change missing data in the reverse sorted files:

`sed -i 's/?/-/g' reverse_teosinte_chr1.txt`

This command will be distributed onto all the reverse chromosomes.

From using less -S on the forward_teosinte_chr .txt files, I noticed there was far less data than there was for maize.  Maybe something went wrong in my commands or that is just the nature of the data.

