# GEN/BIOL 3490 Week 15: Programming for Biologists - BEDTools

**Original material by [Shane Dooley](https://github.com/skDooley/shell_tutorial) and Dr. Geetu Tuteja.
Modified and compiled by [Ha Vu](https://github.com/hhvu0102/unix_basic) (Tuteja Lab).**

## BEDTools overview

BEDTools is a software package that allows easy comparison of genomic data.

- Tasks that can be done using BEDtools are very common in genomic analysis.
- BEDTools is available on Galaxy and Nova. It can also be downloaded and installed on your computer.
- You may find that it is a better choice to run BEDtools on a terminal (Nova or locally) because...
	- BEDtools can be integrated with other UNIX utilities (like `sort`, `wc`, etc)
	- Don’t need to upload, run and download from Galaxy
	- May not need the computational power of the Galaxy server for basic analysis

## BEDTools documentation
[http://bedtools.readthedocs.io/en/latest/index.html](http://bedtools.readthedocs.io/en/latest/index.html)

### Loading the BEDtools module
- Login to Nova and request a partition
- First, enter the command `module load bedtools2` (this command evokes the program `bedtools2` that has been installed on our cluster. Not all programs are pre-installed like this, but most of the popular ones are). 
- **Every time you log in to NOVA, you need to load the module again.**
- Let us know when you complete the `module load bedtools2` command.

- Make sure you are in the directory `lecture`. Check where you are with `pwd`. 
- If you are not in the `lecture` directory, use the command `cd /work/classtmp/GEN349_S2025/<your-net-id>/gen349_week_14_15/lecture/`.
	- Make sure to change `<your-net-id>` to YOUR NetID! 

### `bedtools intersect` 
- `bedtools intersect` allows one to identify overlaps between two sets of genomic regions.
- Usage:

	```
	bedtools intersect [OPTIONS] -a <FILE> -b <FILE1, FILE2, ..., FILEN>
	```
	- When we want to explore `[OPTIONS]` of `bedtools intersect`, use the `flag` `-h`.
	- For whatever file we put right after the flag `-a`, that file is called the A file in this tutorial.
	- For whatever file we put right after the flag `-b`, that file is called the B file in this tutorial.

<img src="/images/File_diagram.png" />	
	
### For all the image examples below, the red boxes mark the resulting intervals of the commands.

#### Default behavior:
By default, if an overlap is found, `bedtools intersect` reports the shared interval between the two overlapping regions.

For example, `bedtools intersect -a fileA.bed -b fileB.bed`


<img src="/images/bedtools-default.PNG" />


#### -wa Reporting the original A region
Instead, one can force `bedtools intersect` to report the **original** “A” region when an overlap is found. As shown below, the entire “A” region is reported, not just the portion that overlaps with the “B” region.

```
bedtools intersect -wa -a fileA.bed -b fileB.bed
```

<img src="/images/bedtools-wa.PNG" />

#### -wb Reporting the original B region
Similarly, one can force `bedtools intersect` to report the **original** “B” region when an overlap is found. If just `-wb` is used, the overlapping portion of A will be reported followed by the **original** “B”. 

```
bedtools intersect -wb -a fileA.bed -b fileB.bed
```

<img src="/images/bedtools-wb.PNG" />

#### Both -wa and -wb
If both `-wa` and `-wb` are used, the original "A" and "B" regions will be reported.
```
bedtools intersect -wa -wb -a fileA.bed -b fileB.bed
```

#### -v
Only report those regions in A that have no overlap in B.
```
bedtools intersect -v -a fileA.bed -b fileB.bed
```
<img src="/images/bedtools-v.PNG" />
    
#### -u
Reports the **original** "A" regions that have at least one overlap found in "B".

* Note: that in the example below, -a is file**B**.bed and -b is file**A**.bed

Try `bedtools intersect -wa -a fileB.bed -b fileA.bed`

Now try: `bedtools intersect -u -wa -a fileB.bed -b fileA.bed`

What's the difference?
