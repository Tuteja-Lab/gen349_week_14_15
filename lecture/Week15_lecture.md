# Week 15 - BEDTools - Programming for Biologists

## BEDTools overview

BEDTools is a software package that allows easy comparison of genomic data.

- Tasks that can be carried out with BEDtools are very common in genomic analysis
- BEDTools is also available on Galaxy 
- You may find yourself in a situation where it is easier to run BEDtools locally on your computer
- Can integrate with other UNIX utilities (like `sort`, `wc`, etc)
- Don’t need to upload, run and download from Galaxy
- May not need the computational power of the Galaxy server for basic (but common) analysis

## BEDTools documentation
[http://bedtools.readthedocs.io/en/latest/index.html](http://bedtools.readthedocs.io/en/latest/index.html)

## bedtools intersect
- First, do `module load bedtools2` (this command evokes the program `bedtools2` that has been installed on our cluster. Not all programs are pre-installed like this, but most of the popular ones are). 
- **Every time you log in to your account, you need to load the module again.**
- Let us know when you are able to finish `module load bedtools2`.

- Make sure you are in the directory `lecture`. Check where you are by doing `pwd`. 
- If you are not in `lecture`, do `cd /home/<your netid>/unix_basic/lecture`.

### `bedtools intersect` 
- `bedtools intersect` allows one to screen for overlaps between two sets of genomic features.
- Usage:

	```
	bedtools intersect [OPTIONS] -a <FILE> -b <FILE1, FILE2, ..., FILEN>
	```
	- When we want to explore `[OPTIONS]` of `bedtools intersect`, use the `flag` `-h`.
	- For whatever file we put right after the flag `-a`, that file is called the A file in this tutorial.
	- For whatever file we put right after the flag `-b`, that file is called the B file in this tutorial.
- For all the image examples, the red boxes mark the resulting intervals of the commands.

#### Default behavior:
By default, if an overlap is found, `bedtools intersect` reports the shared interval between the two overlapping regions.

For example, `bedtools intersect -a file1.bed -b file2.bed`

What are A file and B file in this case?

<img src="/images/bedtools-default.PNG" />


#### -wa Reporting the original A feature
Instead, one can force `bedtools intersect` to report the original “A” feature when an overlap is found. As shown below, the entire “A” feature is reported, not just the portion that overlaps with the “B” feature.

<img src="/images/bedtools-wa.PNG" />

#### -wb Reporting the original B feature
Similarly, one can force bedtools intersect to report the original “B” feature when an overlap is found. If just -wb is used, the overlapping portion of A will be reported followed by the original “B”. 

<img src="/images/bedtools-wb.PNG" />

#### Both -wa and -wb
If both `-wa` and `-wb` are used, the originals of both “A” and “B” will be reported.

#### -v
Only report those entries in A that have no overlap in B.
```
bedtools intersect -v -a file1.bed -b file2.bed
```
<img src="/images/bedtools-v.PNG" />
    
#### -u
Write original A entry once if any overlaps found in B. In other words, just report the fact at least one overlap was found in B.

Try `bedtools intersect -wa -a file2.bed -b file1.bed` and `bedtools intersect -u -wa -a file2.bed -b file1.bed`. 

What's the difference?
