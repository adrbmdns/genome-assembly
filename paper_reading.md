# 01 - Nanopore sequencing technology and tools for genome assembly

https://academic.oup.com/bib/article-abstract/20/4/1542/4958758

# 02 - Canu Tutorial 

https://canu.readthedocs.io/en/latest/tutorial.html

By default, all needed top-level tasks are performed (-pacbio and -nanopore are assumed to be raw and untrimmed while -pacbio-hifi are assumed to be corrected and trimmed). It is possible to run exactly one task by specifying your read characteristics and a step name. These options can be useful if you want to correct reads once and try many different assemblies. We do exactly that in the Canu Quick Start. Additionally, suppling pre-corrected reads with -pacbio -corrected or -nanopore -corrected will run only the trimming and assembling stages. Specifying reads as -corrected -untrimmed will run only the assembly step.

__Canu Outputs:__

* `<prefix>.contigs.layout.tigInfo`: A list of the contigs, lengths, coverage, number of reads and other metadata. Essentially the same information provided in the FASTA header line.