# Review of MRE prediction in circRNAs
Before developing the circRNA-miRNA module of the [nextflow pipeline](https://github.com/BarryDigby/circrna), a thorough review of how databases and existing tools annotate circRNA miRNA reponse elements (MREs) must be conducted. This will be done by 'reverse engineering', available annotations will be downloaded and visualised and documentation tracked. Common themes will be noted, if there are major discrepancies then the authors of papers/tools will be contacted. 

My own questions that I intend to address:
* circRNAs are detected via BSJ in sequencing data, providing the span of the circRNA. However due to altenative splicing (AS) and the fact that circRNAs can retain both exons and introns in their sequence, there is no guarantee that the sequence spanning the BSJ sites are included in the final circRNA sequence. Thus the naive approach of using the whole circRNA sequence for MRE prediction seems unsatisfactory. 

* Currently I agree with the notion that using only the BSJ sequence for MRE analysis is the most plausible yet conservative approach. Yet this method omits a large portion of the circRNA sequence. 

* With regards to targetscan, to predict context scores of miRNAs the UTR sequence of the gene must be provided. I am still unsure how to obtain UTR sequences of miRNAs. 
