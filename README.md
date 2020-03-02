# GATK-calling-tests
Statistical tests performed by GATK on the variant calling

# Rank Sum Test of REF versus ALT base quality scores
This variant-level annotation tests compares the base qualities of the data supporting the reference allele with those supporting the alternate allele. 
The ideal result is a value close to zero, which indicates there is little to no difference. 
A negative value indicates that the bases supporting the alternate allele have lower quality scores than those supporting 
the reference allele. 
Conversely, a positive value indicates that the bases supporting the alternate allele have higher quality scores than those 
supporting the reference allele. 
Finding a statistically significant difference either way suggests that the sequencing process may have been biased or 
affected by an artifact.
URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036863231-BaseQualityRankSumTest

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0

# Rank Sum Test for hard-clipped bases on REF versus ALT reads
This variant-level annotation tests whether the data supporting the reference allele shows more or less base clipping 
(hard clips) than those supporting the alternate allele. 
The ideal result is a value close to zero, which indicates there is little to no difference. 
A negative value indicates that the reads supporting the alternate allele have more hard-clipped bases than those 
supporting the reference allele. Conversely, a positive value indicates that the reads supporting the alternate allele 
have fewer hard-clipped bases than those supporting the reference allele. 
Finding a statistically significant difference either way suggests that the sequencing and/or mapping process may have 
been biased or affected by an artifact.
URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036804891-ClippingRankSumTest

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0

# Phred-scaled p-value for exact test of excess heterozygosity.
This annotation estimates the probability of the called samples exhibiting excess heterozygosity with respect to the 
null hypothesis that the samples are unrelated. 
The higher the score, the higher the chance that the variant is a technical artifact or that there is consanguinuity 
among the samples. 
In contrast to Inbreeding Coefficient, there is no minimal number of samples for this annotation. 
If samples are known to be related, a pedigree file can be provided so that the calculation is only performed on founders
and offspring are excluded.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036726851-ExcessHet

# InbreedingCoeff
Likelihood-based test for the consanguinuity among samples
This annotation estimates whether there is evidence of consanguinuity in a population. 
The higher the score, the higher the chance that some samples are related. 
If samples are known to be related, a pedigree file can be provided so that the calculation is only performed on founders 
and offspring are excluded.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036835471-InbreedingCoeff

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0

