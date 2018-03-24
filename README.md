# databases

参考链接：http://annovar.openbioinformatics.org/en/latest/user-guide/filter/#-polyphen-2-annotation


## LJB* (dbNSFP) non-synonymous variants annotation

The LJB* databases (for historical reasons, it is named as ljb rather than dbNSFP in ANNOVAR) include SIFT scores, PolyPhen2 HDIV scores, PolyPhen2 HVAR scores, LRT scores, MutationTaster scores, MutationAssessor score, FATHMM scores, GERP++ scores, PhyloP scores and SiPhy scores. As of October 2015, the lastest ljb database is dbnsfp30a. Previously, this dataset is referred to as ljb26, ljb23, ljb2, ljb, which caused confusions among many users. Starting from version 3.0a, we will adopt the dbnsfp keyword for future updates. Additionally, users should start to use table_annovar.pl to calculate scores for non-synonymous variants, since we no longer provide individual scores for individual algorithms.

The command below takes an input file and generates 20 different scores and predictions for all the non-synonymous variants in the file. You can open the output file by Excel or other spreadsheet programs to examine.

    annotate_variation.pl -downdb -webfrom annovar -buildver hg19 dbnsfp30a humandb/
    table_annovar.pl ex1.avinput humandb/ -protocol dbnsfp30a -operation f -build hg19 -nastring .

The output include various scores in the following columns: SIFT_score SIFT_pred Polyphen2_HDIV_score Polyphen2_HDIV_pred Polyphen2_HVAR_score Polyphen2_HVAR_pred LRT_score LRT_pred MutationTaster_score MutationTaster_pred MutationAssessor_score MutationAssessor_pred FATHMM_score FATHMM_pred PROVEAN_score PROVEAN_pred VEST3_score CADD_raw CADD_phred DANN_score fathmm-MKL_coding_score fathmm-MKL_coding_pred MetaSVM_score MetaSVM_pred MetaLR_score MetaLR_pred integrated_fitCons_score integrated_confidence_value GERP++_RS phyloP7way_vertebrate phyloP20way_mammalian phastCons7way_vertebrate phastCons20way_mammalian SiPhy_29way_logOdds.

Detailed information for all the LJB23 databases are given below:
```html
<table>
<thead>
<tr>
<th>Score (dbtype)</th>
<th># variants in LJB23 build hg19</th>
<th>Categorical Prediction</th>
</tr>
</thead>
<tbody>
<tr>
<td>SIFT (sift)</td>
<td>77593284</td>
<td>D: Deleterious (sift&lt;=0.05); T: tolerated (sift&gt;0.05)</td>
</tr>
<tr>
<td>PolyPhen 2 HDIV (pp2_hdiv)</td>
<td>72533732</td>
<td>D: Probably damaging (&gt;=0.957), P: possibly damaging (0.453&lt;=pp2_hdiv&lt;=0.956); B: benign (pp2_hdiv&lt;=0.452)</td>
</tr>
<tr>
<td>PolyPhen 2 HVar (pp2_hvar)</td>
<td>72533732</td>
<td>D: Probably damaging (&gt;=0.909), P: possibly damaging (0.447&lt;=pp2_hdiv&lt;=0.909); B: benign (pp2_hdiv&lt;=0.446)</td>
</tr>
<tr>
<td>LRT (lrt)</td>
<td>68069321</td>
<td>D: Deleterious; N: Neutral; U: Unknown</td>
</tr>
<tr>
<td>MutationTaster (mt)</td>
<td>88473874</td>
<td>A" ("disease_causing_automatic"); "D" ("disease_causing"); "N" ("polymorphism"); "P" ("polymorphism_automatic"</td>
</tr>
<tr>
<td>MutationAssessor (ma)</td>
<td>74631375</td>
<td>H: high; M: medium; L: low; N: neutral. H/M means functional and L/N means non-functional</td>
</tr>
<tr>
<td>FATHMM (fathmm)</td>
<td>70274896</td>
<td>D: Deleterious; T: Tolerated</td>
</tr>
<tr>
<td>MetaSVM (metasvm)</td>
<td>82098217</td>
<td>D: Deleterious; T: Tolerated</td>
</tr>
<tr>
<td>MetaLR (metalr)</td>
<td>82098217</td>
<td>D: Deleterious; T: Tolerated</td>
</tr>
<tr>
<td>GERP++ (gerp++)</td>
<td>89076718</td>
<td>higher scores are more deleterious</td>
</tr>
<tr>
<td>PhyloP (phylop)</td>
<td>89553090</td>
<td>higher scores are more deleterious</td>
</tr>
<tr>
<td>SiPhy (siphy)</td>
<td>88269630</td>
<td>higher scores are more deleterious</td>
</tr>
</tbody>
</table>
```
