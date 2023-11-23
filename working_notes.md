## New Words

__mangrove:__ noun. 红树

__antagonistic:__ adjective. 敌对的

__saprobic fungi:__ 腐生真菌

__Coelomycetes:__ a class of conidial fungi where the conidia are formed within a cavity lined by fungal or host tissue. 

__conidium:__ is an asexual, non-motile spore of a fungus. 

__conidia:__ plural of conidium.

__motile:__ able to move by itself (especially of plants, organisms, and very small forms of life). 

__morphology:__ 形态学。The scientific study of the structure and form of animals and plants. 

__haploid:__ adjective. 单倍体



## Cytospora

__Expected genome size:__ 40Mb, haploid 

Read this paper to learn something about Cytospora - [Discovery of three novel cytospora species in Thailand and their antagonistic potential](https://www.mdpi.com/1424-2818/13/10/488) 



## Copy the dorado basecalled bam file to dayhoff

`/mnt/data/dayhoff/home/scratch/u1133824/genome-assembly/cytospora_duplex.bam` 

## How to use NanoPlot

__NanoPlot takes sorted bam files as input, what do you mean sorted? sorted by lengths?__

There is an option --ubam, we can use this option for unmapped bam file which is the bam file from dorado basecaller. 

```sh
NanoPlot --ubam $bam_file 
```

__NanoPlot results:__

The `NanoPlot-report.html` file is similar to FastQC, and it's also the main file we want to look at.

__Is the output bam file from Dorado sorted?__ 

No, they're not sorted. 

__What does N50 means in the plot?__

N50 statistic defines assembly quality in terms of contiguity. Given a set of contigs, the N50 is defined as the sequence length of the shortest contig at 50% of the total assembly length. It can be thought of as the point of half of the mass of the distribution; the number of bases from all contigs longer than the N50 will be close to the number of bases from all contigs shorter than the N50. For example, consider 9 contigs with the lengths 2,3,4,5,6,7,8,9,and 10; their sum is 54, half of the sum is 27, and the size of the genome also happens to be 54. 50% of this assembly would be 10 + 9 + 8 = 27 (half the length of the sequence). Thus the N50=8, which is the size of the contig which, along with the larger contigs, contain half of sequence of a particular genome. Note: When comparing N50 values from different assemblies, the assembly sizes must be the same size in order for N50 to be meaningful.

N50 can be described as a weighted median statistic such that 50% of the entire assembly is contained in contigs or scaffolds equal to or larger than this value.

## Trimming and Filtering

__How should I filter it? What quality threshold should I set? Should I remove any sequence shorter than or longer than something?__

... 

## Verkko Assembler

https://github.com/marbl/verkko 

Verkko is a hybrid assembly pipeline developed for telomere-to-telomere assembly of PacBio HiFi and Oxford Nanopore reads. 

Verkko uses Canu to correct remaining errors in the HiFi reads, builds a multiplex de Bruijn graph using MBG, aligns the Oxford Nanopore reads to the graph using GraphAligner, progressively resolves loops and tangles first with the HiFi reads then with the aligned Oxford Nanopore reads, and finally creates contig consensus sequences using Canu's consensus module. 

__What is de Bruijn graph?__ 

... 

Verkko installed via conda: 

```sh
conda create -n verkko -c conda-forge -c bioconda -c defaults verkko 
```

__Seems like it needs both PacBio hifi and ONT long-reads?__

Read the paper to find out. 

__Assembly without filtering:__

...

## Flye Assembler

https://github.com/fenderglass/Flye 

Flye is a de novo assembler for single-molecule sequencing reads, such as those produced by PacBio and Oxford Nanopore Technologies. It is designed for a wide range of datasets, from small bacterial projects to large mammalian-scale assemblies. 

The package represents a complete pipeline: it takes raw PacBio/ONT reads as input and outputs polished contigs. Flye also has a special mode for metagenome assembly. 

__What are single-molecule sequencing reads?__

...

__Conda install Flye:__

```sh
conda create -n flye
conda activate flye
conda install -c bioconda flye
```

__Flye cannot take .bam file as input:__ 

Go to dorado website to see if we can convert bam file to fastq? Yes, use samtools to convert. 

Use separate conda environment for samtools 1.18

```sh
samtools bam2fq sample.bam > sample.fastq 
```

__Genome assembly for unfiltered reads:__

__Assembly 01 - with default parameters:__

Flye said there is no need to filter reads. See this [do i need to preprocess my reads](https://github.com/fenderglass/Flye/blob/flye/docs/FAQ.md#do-i-need-to-preprocess-my-reads-in-any-way). 

```sh
flye --nano-raw sample.fastq --out-dir outdir --threads 10
```

Returned error:

```
[2023-11-23 05:27:14] ERROR: No disjointigs were assembled - please check if the read type and genome size parameters are correct
[2023-11-23 05:27:14] ERROR: Pipeline aborted
```

According to [GitHub - Flye does not generate any output](https://github.com/fenderglass/Flye/issues/128). It might be because there are a lot of overlaps. We can try use the `--meta` metagenome mode and `--asm-coverage 50` use the longest 50x reads for disjointig assembly. 

__Assembly 02 - with `--asm-coverage 50`:__

```sh
flye --nano-raw sample.fastq --out-dir outdir --threads 10 --asm-coverage 50 -g 40m
```

Maybe can try `--nano-hq` later. 

## Canu Assembler

https://github.com/marbl/canu

Canu is a fork of the Celera Assembler, designed for high-noise single-molecule sequencing (such as the PacBio RSII/Sequel or Oxford Nanopore MinION).

Canu is 

## Celera Assembler 

...

## Other Assembler ?? 

... 