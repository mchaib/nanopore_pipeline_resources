# nanopore_pipeline_resources

Here's a set of resources for sequence processing and assembly starting from long reads generated with Nanopore. 

There are two pipelines that we explore using long-read data:

1. Hybrid assembly of short reads generated with Illumina MiSeq? V2? and long Nanopore reads using UniCycler.
2. Assembly of long Nanopore reads alone, where we explore two routes:
2.1. Minimap2 + Miniasm + Racon
2.2. Flye

These pipelines assume you have already performed the base-calling step with your data, and have fastq (rather than fast5) files available for the analyses.


The quality checks and filtering steps are common to the two approaches. To visualize the quality of the long-read data, we use pycoQC. This is the [GitHub repository to pycoQC](https://tleonardi.github.io/pycoQC/), which includes extensive documentation on installation and usage. PycoQC supports 1D and 1D2 runs generated with Minion, Gridion and Promethion devices and basecalled with Albacore 1.2.1+ or Guppy 2.1.3+. The tool for trimming raw reads is NanoFilt 



