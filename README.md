# 令和8年度大学院講義（臨床障害学実践学）

- **Simple RNA-seq data analysis tutorial**
- by Yilin Du
- 2026.06.02

## What is RNA-seq?

RNA-seq (RNA sequencing) is a powerful technique that uses high-throughput sequencing to profile the transcriptome, i.e., the complete set of RNA molecules in a sample. It allows researchers to measure gene expression levels, identify novel transcripts, and analyze alternative splicing events. The general workflow of RNA-seq includes:

- Sample and RNA extraction: Extracting total RNA from tissues or cells. Often, mRNA (e.g., poly-A RNA) is enriched or rRNA is removed to focus on coding gene expression.
- Library construction (converting RNA into sequencable "pages"): The extracted RNA is typically fragmented into shorter pieces, then converted to cDNA (complementary DNA) via reverse transcription. cDNA is then end-repaired, adapter-ligated, and amplified via limited PCR to generate a sequencing library.
- Sequencing (using Illumina as an example): Libraries are loaded onto flow cells and undergo bridge amplification to form clusters. The "sequencing-by-synthesis" method is used, where fluorescently labeled nucleotides are added in cycles, photographed, and the resulting colors indicate the sequence. This produces many short reads (single-end or paired-end).
- Read types and design considerations: Single-end (SE) or paired-end (PE) sequencing can be chosen based on experimental goals (transcript quantification vs. alternative splicing/fusion gene detection). Read length and sequencing depth affect sensitivity and accuracy for detecting low-expression genes, alternative splicing, and transcript quantification.
- Basic data processing workflow: Quality control and adapter trimming of raw reads; mapping high-quality reads to a reference genome or transcriptome; counting reads per gene or transcript; normalizing counts and building statistical models; performing differential expression analysis and functional enrichment downstream.

**We will focus on how to start from raw data (fastq), perform quality control, mapping, counting, and finally conduct differential expression analysis and result visualization.**

## What you will get from this tutorial?

You will learn how to perform a bulk RNA-seq analysis starting from raw data to obtain a gene expression matrix, a list of differentially expressed genes, and simple visualizations.

## Homework?(Maybe)

1. Please read the reference paper in the repository to learn more: [RNA-seq data science: From raw data to effective interpretation](https://www.frontiersin.org/journals/genetics/articles/10.3389/fgene.2023.997383/full)   or [Local copy](./Papers/RNA-seq%20data%20science%20From%20raw%20data%20to%20effective%20interpretation.pdf).
2. I have prepared a [raw data](https://drive.google.com/drive/folders/10ohrY-cVF5GkT02uwnxkgLWo1bZ0wMna?usp=sharing) that contains fastq files and metadata for two control groups and two experimental groups. Please follow the tutorial in this repository to complete the workflow from raw data to differential expression analysis. At the end, please obtain at least the following:
   1. FastQC reports and interpretation;
   2. Gene expression matrix;
   3. Differentially expressed gene list;
   4. Volcano plot and heatmap of the differentially expressed genes.
3. If you want, you can send the results to me and I can give you some feedback.

## My suggestions:

1. During the tutorial, you may encounter many errors and issues. My recommendation is to:
   - Read the error messages carefully and try to understand what they mean. LLMs can help you interpret error messages and suggest possible solutions, but they may not always be accurate. Always verify the suggestions with official documentation or trusted sources.
   - **Read the official documentation** of the tools you are using to understand the correct usage and options.
   - Search for the error message on GitHub, Google or other forums or search engines to see how others have resolved similar issues.
   - If you are still stuck, you can ask LLMs for help.

## If you finish all above, please think and try:

1. `Salmon` is a popular tool for transcript quantification that uses a lightweight mapping approach compared to traditional aligners. Try using `Salmon` instead of `hisat2` + `featureCounts` to obtain transcript-level quantification, and then use `tximport` to summarize to gene-level counts for DESeq2 analysis. Compare the results with the traditional approach (mapping rate, etc. and think about why they differ).
2. What is TPM/FPKM? Why do we not use them for DE analysis? Try to calculate TPM/FPKM from the raw counts and compare with the normalized counts from DESeq2.
3. Try using `edgeR` or `limma` instead of `DESeq2` for differential expression analysis. What are the differences of these tools and the strengths and weaknesses of each? At what time should we choose one over the others?
4. Learn more about `ggplot2` and try to customize the plot in your own way.
5. Actually, there are many parameters in each main analysis function and only a few of them are used in the tutorial. It would be better if you can figure out other parameters meaning. For example, try to figure out all the parameters in `enrichGO` of `clusterProfiler` and see how they affect the results.  
6. There are many other packages which can replace the ones we used in this tutorial. Please feel free to explore and try them out.
7. Many other visualizations can be done and combined with the DE results, search what others have done and try to make them by yourself.
8. There are many other downstream analyses you can do with the DE results, such as gene set enrichment analysis, pathway analysis, network analysis, etc. Please perform GSEA, WGCNA and PPI network analysis with the DE results and see what you can find.
9. Read more papers and tutorials to learn more about RNA-seq data analysis and the latest tools, algorithms, methods, etc.

---

It is my first time writing a tutorial like this and there may be some mistakes in the code or explanations. Please feel free to point out any issues you find, and I will try to fix them as soon as possible.
