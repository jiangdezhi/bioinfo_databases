# databases

参考链接：http://annovar.openbioinformatics.org/en/latest/user-guide/filter/#-polyphen-2-annotation


##1.LJB* (dbNSFP) non-synonymous variants annotation

The LJB* databases (for historical reasons, it is named as ljb rather than dbNSFP in ANNOVAR) include SIFT scores, PolyPhen2 HDIV scores, PolyPhen2 HVAR scores, LRT scores, MutationTaster scores, MutationAssessor score, FATHMM scores, GERP++ scores, PhyloP scores and SiPhy scores. As of October 2015, the lastest ljb database is dbnsfp30a. Previously, this dataset is referred to as ljb26, ljb23, ljb2, ljb, which caused confusions among many users. Starting from version 3.0a, we will adopt the dbnsfp keyword for future updates. Additionally, users should start to use table_annovar.pl to calculate scores for non-synonymous variants, since we no longer provide individual scores for individual algorithms.

The command below takes an input file and generates 20 different scores and predictions for all the non-synonymous variants in the file. You can open the output file by Excel or other spreadsheet programs to examine.

    annotate_variation.pl -downdb -webfrom annovar -buildver hg19 dbnsfp30a humandb/
    table_annovar.pl ex1.avinput humandb/ -protocol dbnsfp30a -operation f -build hg19 -nastring .

The output include various scores in the following columns: SIFT_score SIFT_pred Polyphen2_HDIV_score Polyphen2_HDIV_pred Polyphen2_HVAR_score Polyphen2_HVAR_pred LRT_score LRT_pred MutationTaster_score MutationTaster_pred MutationAssessor_score MutationAssessor_pred FATHMM_score FATHMM_pred PROVEAN_score PROVEAN_pred VEST3_score CADD_raw CADD_phred DANN_score fathmm-MKL_coding_score fathmm-MKL_coding_pred MetaSVM_score MetaSVM_pred MetaLR_score MetaLR_pred integrated_fitCons_score integrated_confidence_value GERP++_RS phyloP7way_vertebrate phyloP20way_mammalian phastCons7way_vertebrate phastCons20way_mammalian SiPhy_29way_logOdds.

Detailed information for all the LJB23 databases are given below:

![](https://github.com/jiangdezhi/bioinfo_databases/blob/master/ljb23_dbtype.png)

## 2.ljb23数据库中，常见预测变异致病性的算法为SIFT和polyphen2-hdiv,polyphen2-hvar
### 1.LJB23_SIFG_score：初始打分值； LJB23_SIFT_score_converted：转换后的打分制，等于1-LJB23_SIFG_score；LJB23_SIFT_pred：突变类型预测，D表示Deleterious（LJB23_SIFG_score<0.05）,T表示Torelated。
### 2.LJB23_Polyphen2_HDIV_score：打分值；LJB23_Polyphen2_HDIV_pred：突变类型预测，分三种类型：probably damaging(D),possible  damaging(P)，benign（B）。其中LJB23_Polyphen2_HDIV_score=>0.957,表示D类型；LJB23_Polyphen2_HDIV_score<=0.452,表示B类型；介于两者之间表示P类型。
### 3.LJB23_Polyphen2_HVAR_score：打分值；LJB23_Polyphen2_HVAR_pred：突变类型预测，分三种类型：probably damaging(D),possible  damaging(P)，benign（B）。其中LJB23_Polyphen2_HVAR_score=>0.909,表示D类型；LJB23_Polyphen2_HVAR_score<=0.447,表示B类型；介于两者之间表示P类型。
### 4.其他就不一一介绍了。LJB23_LRT_score LJB23_LRT_score_converted LJB23_LRT_pred LJB23_MutationTaster_score LJB23_MutationTaster_score_converted LJB23_MutationTaster_pred LJB23_MutationAssessor_score LJB23_MutationAssessor_score_converted LJB23_MutationAssessor_pred LJB23_FATHMM_score LJB23_FATHMM_score_converted LJB23_FATHMM_pred LJB23_RadialSVM_score LJB23_RadialSVM_score_converted LJB23_RadialSVM_pred LJB23_LR_score LJB23_LR_pred LJB23_GERP++ LJB23_PhyloP LJB23_SiPhy.


## 3.特殊情况




MetaSVMs不适用单基因病变异致病性评估

