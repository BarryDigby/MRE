# Review of MRE prediction in circRNAs
Before developing the circRNA-miRNA module of the [nextflow pipeline](https://github.com/BarryDigby/circrna), a thorough review of how databases and existing tools annotate circRNA miRNA reponse elements (MREs) must be conducted. This will be done by 'reverse engineering', available annotations will be downloaded and visualised and documentation tracked. Common themes will be noted, if there are major discrepancies then the authors of papers/tools will be contacted. 

My own questions that I intend to address:
* circRNAs are detected via BSJ in sequencing data, providing the span of the circRNA. However due to altenative splicing (AS) and the fact that circRNAs can retain both exons and introns in their sequence (exonic circRNAs (ecircRNAs), circular intronic RNAs (ciRNAs), retained-intron or exon-intron circRNAs (EIciRNAs), and intergenic circRNAs), there is no guarantee that the sequence spanning the circRNA between BSJ sites are included in the final circRNA sequence. Thus the naive approach of using the whole circRNA sequence for MRE prediction seems unsatisfactory. 

* Currently I agree with the notion that using only the BSJ sequence for MRE analysis is the most plausible yet conservative approach. However this method omits a large portion of the circRNA sequence. 

* With regards to targetscan, to predict context scores of miRNAs the UTR sequence of the gene must be provided. I am still unsure how to obtain UTR sequences of miRNAs. 

# Databases
The databases I will interrogate are [CircInteractome](https://circinteractome.nia.nih.gov/) and [CSCD](https://gb.whu.edu.cn/CSCD/) as they provide miRNA sites on a given circRNA. 

I will use `hsa_circ_0022392` as the query circRNA whose parental gene is `FADS2`, as I have Arraystar data correpsonding to this circRNA and its MRE sites calculated from both `miRanda` and `TargetScan`. 

### Circinteractome
* link to paper: [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4829301/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4829301/)

###### miRNA Target ciRNAs  
> Mature sequences of circRNAs were used in the TargetScan Perl Script to predict the miRNAs which have sequence complementarity with circRNA. The complete miRNA list and sequences were taken from the microRNA database (http://www.mirbase.org/)

miRNA data for `hsa_circ_0022392` available [here](https://circinteractome.nia.nih.gov/api/v2/mirnasearch?circular_rna_query=hsa_circ_0022392&mirna_query=&submit=miRNA+Target+Search). 

