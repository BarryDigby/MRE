# Review of MRE prediction in circRNAs
Before developing the circRNA-miRNA module of the [nextflow pipeline](https://github.com/BarryDigby/circrna), a thorough review of how databases and existing tools annotate circRNA miRNA reponse elements (MREs) must be conducted. This will be done by 'reverse engineering', available annotations will be downloaded and visualised and documentation tracked. Common themes will be noted, if there are major discrepancies then the authors of papers/tools will be contacted. 

My own questions that I intend to address:
* circRNAs are detected via BSJ in sequencing data, providing the span of the circRNA. However due to altenative splicing (AS) and the fact that circRNAs can retain both exons and introns in their sequence (exonic circRNAs (ecircRNAs), circular intronic RNAs (ciRNAs), retained-intron or exon-intron circRNAs (EIciRNAs), and intergenic circRNAs), there is no guarantee that the sequence spanning the circRNA between BSJ sites are included in the final circRNA sequence. Thus the naive approach of using the whole circRNA sequence for MRE prediction seems unsatisfactory. 

* Currently I agree with the notion that using only the BSJ sequence for MRE analysis is the most plausible yet conservative approach. However this method omits a large portion of the circRNA sequence. 

* With regards to targetscan, to predict context scores of miRNAs the UTR sequence of the gene must be provided. I am still unsure how to obtain UTR sequences of miRNAs. 

# Databases
The databases I will interrogate are [CircInteractome](https://circinteractome.nia.nih.gov/) and [CSCD](https://gb.whu.edu.cn/CSCD/) as they provide miRNA sites on a given circRNA. 


## hsa_circ_0022392
miRNA data for `hsa_circ_0022392` pulled from `CircInteractome` search query [here](https://circinteractome.nia.nih.gov/api/v2/mirnasearch?circular_rna_query=hsa_circ_0022392&mirna_query=&submit=miRNA+Target+Search) and miRNA table copied from `CSCD` results page (search PLCL2, cancer,normal, chr3:17051165|17109557) and reformatted locally. The corresponding bed files used to generate the IGV image can be found under the master branch in `test/circinteractome`. 

#### Results in IGV:
![](https://github.com/BarryDigby/MRE/blob/main/test/CSCD/CSCD_hsa_circ_0022392.png)

*CircInteractome miR sites given in red, CSCD miR sites given in purple*

###### Comments
For `CircInteractome` the miRNA sites span the first exon of the circRNA and interestingly, also span the intronic space between exon 1 and exon 2. The total length of sequence where miRNAs appear is 272nt in length, suggesting that predefined sequence length for Targetscan analysis was not adopted. Ultimately I still question why miRNA sites are not appearing along the entire circRNA sequence. 

`CSCD` however only uses a short ~100nt sequence for miRNA prediction.


## hsa_circ_0122696
miRNA data was copied and reformatted from the `CircInteractome` table at [this link](https://circinteractome.nia.nih.gov/api/v2/mirnasearch?circular_rna_query=hsa_circ_0122696&mirna_query=&submit=miRNA+Target+Search) and miRNA table copied from `CSCD` results page (search PLCL2, cancer,normal, chr3:17051165|17109557) and reformatted locally. 

#### Results in IGV:
![](https://github.com/BarryDigby/MRE/blob/main/test/CSCD/CSCD_hsa_circ_0122696.png)

*CircInteractome miR sites given in red, CSCD miR sites given in purple*

###### Comments
Yet again the miR sites span the first exon and into the intronic sequence of `hsa_circ_0122696`. 
***

### CSCD
### hsa_circ_0022392
miRNA table was copied from the results page (search FADS2, common circRNA, chr11:61630443|61631258) and reformatted locally. The start site of the circRNA was added to each miRNA start site to get its context within the circRNA `awk -v s=61630443 -v OFS="\t" '{print $1, $2+s, $3+s, $4, $5}' miR_sites.bed`. 

#### Results in IGV:
![](https://github.com/BarryDigby/MRE/blob/main/test/CSCD/CSCD_hsa_circ_0022392.png)

*CircInteractome miR sites given in red, CSCD miR sites given in purple*

###### Comments
`CSCD` seems to use only the 100nt in its MRE prediction, however there are far more miRNAs provided with this analysis. `CircInteractome` provides much richer annotation spanning the first exon and into the intronic space yet again.

