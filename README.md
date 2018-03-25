# dbNSFP

参考链接：http://annovar.openbioinformatics.org/en/latest/user-guide/filter/#-polyphen-2-annotation


## 1.LJB* (dbNSFP) non-synonymous variants annotation

>The LJB* databases (for historical reasons, it is named as ljb rather than dbNSFP in ANNOVAR) include SIFT scores, PolyPhen2 HDIV scores, PolyPhen2 HVAR scores, LRT scores, MutationTaster scores, MutationAssessor score, FATHMM scores, GERP++ scores, PhyloP scores and SiPhy scores. As of October 2015, the lastest ljb database is dbnsfp30a. Previously, this dataset is referred to as ljb26, ljb23, ljb2, ljb, which caused confusions among many users. Starting from version 3.0a, we will adopt the dbnsfp keyword for future updates. Additionally, users should start to use table_annovar.pl to calculate scores for non-synonymous variants, since we no longer provide individual scores for individual algorithms.

>The command below takes an input file and generates 20 different scores and predictions for all the non-synonymous variants in the file. You can open the output file by Excel or other spreadsheet programs to examine.

    annotate_variation.pl -downdb -webfrom annovar -buildver hg19 dbnsfp30a humandb/
    table_annovar.pl ex1.avinput humandb/ -protocol dbnsfp30a -operation f -build hg19 -nastring .

>The output include various scores in the following columns: SIFT_score SIFT_pred Polyphen2_HDIV_score Polyphen2_HDIV_pred Polyphen2_HVAR_score Polyphen2_HVAR_pred LRT_score LRT_pred MutationTaster_score MutationTaster_pred MutationAssessor_score MutationAssessor_pred FATHMM_score FATHMM_pred PROVEAN_score PROVEAN_pred VEST3_score CADD_raw CADD_phred DANN_score fathmm-MKL_coding_score fathmm-MKL_coding_pred MetaSVM_score MetaSVM_pred MetaLR_score MetaLR_pred integrated_fitCons_score integrated_confidence_value GERP++_RS phyloP7way_vertebrate phyloP20way_mammalian phastCons7way_vertebrate phastCons20way_mammalian SiPhy_29way_logOdds.

>Detailed information for all the LJB23 databases are given below:

![](https://github.com/jiangdezhi/bioinfo_databases/blob/master/ljb23_dbtype.png)

## 2.ljb23数据库中，常见预测变异致病性的算法为SIFT和polyphen2-hdiv,polyphen2-hvar
>1.LJB23_SIFG_score：初始打分值； LJB23_SIFT_score_converted：转换后的打分制，等于1-LJB23_SIFG_score；LJB23_SIFT_pred：突变类型预测，D表示Deleterious（LJB23_SIFG_score<0.05）,T表示Torelated。

>2.LJB23_Polyphen2_HDIV_score：打分值；LJB23_Polyphen2_HDIV_pred：突变类型预测，分三种类型：probably damaging(D),possible  damaging(P)，benign（B）。其中LJB23_Polyphen2_HDIV_score=>0.957,表示D类型；LJB23_Polyphen2_HDIV_score<=0.452,表示B类型；介于两者之间表示P类型。

>3.LJB23_Polyphen2_HVAR_score：打分值；LJB23_Polyphen2_HVAR_pred：突变类型预测，分三种类型：probably damaging(D),possible  damaging(P)，benign（B）。其中LJB23_Polyphen2_HVAR_score=>0.909,表示D类型；LJB23_Polyphen2_HVAR_score<=0.447,表示B类型；介于两者之间表示P类型。

>4.其他就不一一介绍了。LJB23_LRT_score LJB23_LRT_score_converted LJB23_LRT_pred LJB23_MutationTaster_score LJB23_MutationTaster_score_converted LJB23_MutationTaster_pred LJB23_MutationAssessor_score LJB23_MutationAssessor_score_converted LJB23_MutationAssessor_pred LJB23_FATHMM_score LJB23_FATHMM_score_converted LJB23_FATHMM_pred LJB23_RadialSVM_score LJB23_RadialSVM_score_converted LJB23_RadialSVM_pred LJB23_LR_score LJB23_LR_pred LJB23_GERP++ LJB23_PhyloP LJB23_SiPhy.


## 3.特殊情况
>1.ljb2_pp2hvar should be used for diagnostics of Mendelian diseases, which requires distinguishing mutations with drastic effects from all the remaining human variation, including abundant mildly deleterious alleles.The authors recommend calling "probably damaging" if the score is between 0.909 and 1, and "possibly damaging" if the score is between 0.447 and 0.908, and "benign" is the score is between 0 and 0.446.(**polyphen2_hvar被用来诊断孟德尔疾病，要求从剩余的人类所有变异中区分有重大影响的变异，包括高丰度的温和有害性等位基因。**）

>2.ljb2_pp2hdiv should be used when evaluating rare alleles at loci potentially involved in complex phenotypes, dense mapping of regions identified by genome-wide association studies, and analysis of natural selection from sequence data. The authors recommend calling "probably damaging" if the score is between 0.957 and 1, and "possibly damaging" if the score is between 0.453 and 0.956, and "benign" is the score is between 0 and 0.452.（**polyphen2_hdiv被用来在复杂表型位点评估罕见等位基因**)

>3.FATHMMT is less well known compared to SIFT and PolyPhen, but in our experience it works really well and better than SIFT/PolyPhen

>4.MetaSVM（又称 radialSVM），类似SIFT包括2个打分值和1个突变类型预测
LJB23_RadialSVM_score：raw score
LJB23_RadialSVM_score_converted：converted score（转换分值)，0-1 range, higher score denoting more deleterious variants
LJB23_RadialSVM_pred：predictions

>It has clear advantage over other competing approaches such as SIFT/PolyPhen/CADD/Condel: (1) better performance (2) less missing values than SIFT/PolyPhen/Condel.

>the model building used variants that are known to cause Mendelian diseases so the method is specifically designed to work for Mendelian diseases but not complex diseases(**MetaSVM模型是使用导致孟德尔疾病的变异构建的，所以该方法是为孟德尔疾病特别设计的，并不适用复杂疾病变异**)

>**5.GERP++只对编码区变异进行注释。**
Both are similar to GERP++ and these three can be considered as competitors of each other (just like SIFT and PolyPhen are competitors of each other).

>PhyloP score is based on multiple alignments of 46 genomes. Similarly, SiPhy score is based on 29 mammals genomes. The larger the score, the more conserved the site.

    注意：(1) these types of "conservation scores" only considers conservation level at the current base, and they do not care       about the actual nucleotide identity so synonymous and non-synonymous variants at the same site will be scored as the same       (2) these scores are not designed specifically for finding causal variants for Mendelian diseases, but for finding       
    functionally important sites, so variants that confer increased susceptibility may be scored well(1.GERP++，PhyloP，siPhy三种     方法的保守性打分只考虑当前碱基的保守性水平，不考虑实际碱基的一致性，所以相同位置的同义和非同义突变的保守性是一样的。2.这些打分值不是专门设计用来     寻找导致孟德尔遗传病的变异，而是用来发现功能性的重要位点，所以只要变异被证明是增加了疾病易感性打分值都会比较高）
   











