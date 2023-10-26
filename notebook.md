## How to do genome assembly? What are the steps?

Article [Ten steps to get started in Genome Assembly and Annotation](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5850084/) 

## Learn about nanopore long-read

What is long-read? How long it can be? What's the difference between long-read and short-read? What's the accuracy?

Nanopore sequencing is a technology that enables real-time analysis of long DNA or RNA fragments. It works by monitoring changes to an electrical current as nucleic acids are passed through a protein nanopore. [1]

__Direct DNA sequencing__

Nanopore can analyse native DNA, without the requirement for amplification, eliminates PCR bias and allows the identification of base modifications alongside nucleotide sequence. [1]

## What is fast5 and pod5 format?

__Fast5__

The Fast5 format is the standard sequencing output for Oxford Nanopore sequencers such as the MinION. In contrast to FASTA and FastQ files, a Fast5 file is binary and cannot be opended with a normal text editor. [2]

The Fast5 format is the native container for data coming out of Oxford Nanopore Technology's various nanopore sequencers. It is meant to contain the raw electrical signal levels measured by the nanopores, from which various information can be extracted. [3]

To conclude, Fast5 is the format that come out of nanopore suquencers, it is binary, and it contains electrical signal information from nanopores. 

__Pod5__

Pod5 is a file format for storing nanopore sequencing data in an easily accessible way. The format is able to be written in a streaming manner which allows a sequencing instrument to directly write the format. (I DON'T UNDERSTAND THE DIFFERENCE!!!) [4]

The Pod5 format is, at its core, a collection of Apache Arrow tables, stored in the Apache Feather 2 format, and bundled into a container format. The container file has the extension `.pod5`. [5]

Okay from my opinion, Pod5 is just another file format that has some advantages on reading/writing file contents, make it faster to access and compute. A file format to make downstream analysis easier. 

Dorado basecalling is faster when using Pod5 files. [6] 

## Learn package NanoPlot 

What are the results look like? Maybe need to read the documentation. 

## Basecalling with Dorado

__Simplex basecalling__

One strand at a time. [7]

__Duplex basecalling__

Two strands from the single molecule were reading at the same time. It represents the same sequence. We can jointly infer over both of those to obtain a more accurate individual output read. [7]

What happening on the flow cell is, a double-stranded DNA molecule. One end by chance will start sequencing first, as it goes through it unzips from the second strand. When the first strand finishes sequencing that leaves the five prime end and the motor of the second strand in very close proximity to the pore. So with some probability it will follow its mate through the same pore and sequence right after. So we detected this duplex pair in the output reads by finding two complementary sequences that went through the same pore one after another. [7]

Duplex is very beneficial to accuracies. 

## Q20 and Q30 data? How can I see it? 

## ONT ultralong and pore-c sequencing? What's the difference? 

## Telomere to Telomere (T2T) genome assemblies 

__Verkko__

Takes in data like:

* Long, high accuracy reads (~30kb at Q30), Duplex
* Ultralong reads (~100kb at Q20)
* Parental reads/chromatin conformation capture (Pore-C) 

__Hifiasm__ 




## Validation, mapping reads back to genome assembly 

## How does de novo genome assembly works? The theory. 


## References

1. Oxford Nanopore Technologies - [DNA Sequencing](https://nanoporetech.com/applications/dna-nanopore-sequencing) 
2. Tim Kahlke - [Sequence File Formats](https://timkahlke.github.io/LongRead_tutorials/APP_FORM.html) 
3. ShianSu - [A look at the Nanopore fast5 format](https://medium.com/@shiansu/a-look-at-the-nanopore-fast5-format-f711999e2ff6) 
4. [Pod5 File Format Documentation](https://pod5-file-format.readthedocs.io/en/latest/index.html)
5. [Pod5 Format Specification](https://pod5-file-format.readthedocs.io/en/latest/SPECIFICATION.html) 
6. Dorado GitHub - [README.md](https://github.com/nanoporetech/dorado) 
7. Oxford Nanopore Technologies - [Advances in basecalling research and development](https://www.youtube.com/watch?v=mnrk_5NhQUQ) 
