# RNASeq

# RNASeq

RNA sequencing (RNASeq) is a powerful and widely used technique for studying gene expression and transcriptome profiling. It involves sequencing the RNA molecules present in a biological sample, allowing researchers to identify and quantify the RNA transcripts that are present. RNASeq can be used to investigate a range of biological questions, including identifying differentially expressed genes, characterizing alternative splicing events, and detecting novel transcripts.

One of the major advantages of RNASeq is its ability to detect lowly expressed genes and quantify transcript abundance with high accuracy. This makes it a valuable tool for studying rare cell populations or subtle changes in gene expression. RNASeq can also be used to study non-coding RNAs, such as microRNAs and long non-coding RNAs, which have been implicated in a range of biological processes.

RNASeq has become increasingly accessible and affordable in recent years, with a range of commercial and open-source software tools available for analysis. However, RNASeq data analysis can be complex, and requires careful consideration of experimental design, normalization methods, and statistical analysis. Multiple factors affect the tools chosen to carry out analysis, and the workings of these tools have to be well understood to select the best one to carry out analysis. This tool hub will focus on the steps of RNASeq analysis, focusing on the tools available for each step, and the commands to run the steps.

## Datasets

We will use a public dataset from the Galaxy RNASeq tutorial. We use the subsampled data for our steps, but the large datasets are also available for use. The datasets are in fastqsanger format, which is similar to fastq format

```bash
## You can use wget or curl to get the datasets. Or a for loop
https://zenodo.org/record/6457007/files/GSM461177_1_subsampled.fastqsanger
https://zenodo.org/record/6457007/files/GSM461177_2_subsampled.fastqsanger
https://zenodo.org/record/6457007/files/GSM461180_1_subsampled.fastqsanger
https://zenodo.org/record/6457007/files/GSM461180_2_subsampled.fastqsanger
```

## Steps

### 1. Quality control and Trimming

This step involves removing errors introduced during the sequencing process. Different sequence platforms may cause different errors. Trimming is also necessary where adapters are present, and the reads are longer than the fragments sequenced. 

Your input at this point is fastq or fasta reads, and in most cases paired-end reads (_1.fastq and _2 .fastq in our case). The output of the fastqc or multiqc steps are reports that guide on the type of trimming to be done. These two tools are relatively ‘lightweight’ in terms of computational resources, and can run on a local PC.  

- FastQC - Check out the documentation here:  https://github.com/s-andrews/FastQC
- MultiQC - MultiQC can aggregate reports of multiple samples: https://github.com/ewels/MultiQC

The adapter trimming comes after checking the quality of the sequences. 

- Cutadapt - [https://cutadapt.readthedocs.io/en/stable/](https://cutadapt.readthedocs.io/en/stable/)
- TrimGalore - https://github.com/FelixKrueger/TrimGalore

Another quality check is conducted using FastQC or multiQC tools to check if the quality has improved. 

Each of these tools have man pages to guide their installation and use. Here are the basic commands of the tools:

```bash
## Fastqc
fastqc input.fastq

## Multiqc
multiqc input.fastq

## Cutadapt
cutadapt -a AACCGGTT -o output.fastq input.fastq

## TrimGalore
trim_galore input.fastq
```

### 2. Mapping

We need to find the position of each gene on the organisms genome. To do this we ‘map’ or align the reads to the reference genome, if the genome exists. Multiple tools have been designed to do mapping and can be sample specific. These step is usually computationally intensive and in most cases fails on local computers. Cloud computing or running the analysis in a cluster might be a solution if analysis fails on a local PC. 

The input of these tools are FASTA/Q reads and the output is SAM/BAM files. Some common tools include: 

- Bowtie2 - https://github.com/BenLangmead/bowtie2
- SOAP - [http://gaow.github.io/genetic-analysis-software/s/soap/](http://gaow.github.io/genetic-analysis-software/s/soap/)
- STAR - https://github.com/alexdobin/STAR
- HISAT - https://github.com/DaehwanKimLab/hisat2
- TopHat -https://github.com/infphilo/tophat

```bash
## Bowtie2

## SOAP

## STAR

## HISAT2

## TopHat
```

### 3. Analysis of the deferentially expressed genes
