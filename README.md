# nanopore_pipeline_resources

Here's a set of resources for sequence processing and assembly starting from long reads generated with Nanopore. 

There are two pipelines that we explore using long-read data:

1. Hybrid assembly of short reads generated with Illumina MiSeq? V2? and long Nanopore reads using UniCycler.
2. Assembly of long Nanopore reads alone, where we explore two routes:
    1. Minimap2 + Miniasm + Racon (covered via Unicycler? -- see below)
    2. Flye

These pipelines assume you have already performed the base-calling step with your data, and have fastq (rather than fast5) files available for the analyses.

### Quality control and trimming
The quality checks and filtering steps are common to the two approaches. To visualize the quality of the long-read data, we use pycoQC. This is the [GitHub repository to pycoQC](https://tleonardi.github.io/pycoQC/), which includes extensive documentation on installation and usage. PycoQC supports 1D and 1D2 runs generated with Minion, Gridion and Promethion devices and basecalled with Albacore 1.2.1+ or Guppy 2.1.3+. The tool we use here for trimming raw reads is NanoFilt, with its [GitHub repository available here](https://github.com/wdecoster/nanofilt), and an associated [NanoFilt tutorial](https://timkahlke.github.io/LongRead_tutorials/FTR_N.html). 

### The hybrid route
Assuming you are starting with trimmed reads from both Illumina and Nanopore, we will be using [Unicycler](https://github.com/rrwick/Unicycler). Unicycler is an assembly pipeline for bacterial genomes. It can assemble Illumina-only read sets where it functions as a SPAdes-optimiser. **It can also assembly long-read-only sets (PacBio or Nanopore) where it runs a miniasm+Racon pipeline**. For the best possible assemblies, give it both Illumina reads and long reads, and it will conduct a hybrid assembly -- it is this last option we are using. These are important notes regarding the use of these tools:

* If you only have short reads, use Unicycler (Trycycler does not do short-read assembly).
* If you only have long reads, Trycycler is a better choice. While Unicycler can do long-read-only assembly, its approach is somewhat out-of-date. Something else to consider is the depth of your long reads, as Trycycler prefers deeper read sets. If your long-read set is particularly shallow (~25× or less), then [Flye](https://github.com/fenderglass/Flye) might be your best option.
* If you have both short and long reads (i.e. are doing a hybrid assembly), then Unicycler and Trycycler+polishing are both viable options. If you have lots of long reads (~100× depth or more), use Trycycler+polishing. If you have sparse long reads (~25× or less), use Unicycler. If your long-read depth falls between those values, it might be worth trying both approaches.




