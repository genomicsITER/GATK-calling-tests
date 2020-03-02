# GATK-calling-tests
Statistical tests performed by GATK on the variant calling

As seen by HaplotypeCaller

annotation=[HaplotypeScore, MappingQualityRankSumTest, QualByDepth, ReadPosRankSumTest, RMSMappingQuality, FisherStrand, Coverage, StrandBiasBySample]

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

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# InbreedingCoeff
Likelihood-based test for the consanguinuity among samples
This annotation estimates whether there is evidence of consanguinuity in a population. 
The higher the score, the higher the chance that some samples are related. 
If samples are known to be related, a pedigree file can be provided so that the calculation is only performed on founders 
and offspring are excluded.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036835471-InbreedingCoeff

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# RMSMappingQuality
Root Mean Square of the mapping quality of reads across all samples.
This annotation provides an estimation of the overall mapping quality of reads supporting a variant call, averaged over all samples in a cohort.

Statistical notes
The root mean square is equivalent to the mean of the mapping qualities plus the standard deviation of the mapping qualities.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036454912-RMSMappingQuality

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# FisherStrand
Strand bias estimated using Fisher's Exact Test
Strand bias is a type of sequencing bias in which one DNA strand is favored over the other, which can result in incorrect evaluation of the amount of evidence observed for one allele vs. the other. The FisherStrand annotation is one of several methods that aims to evaluate whether there is strand bias in the data. It uses Fisher's Exact Test to determine if there is strand bias between forward and reverse strands for the reference or alternate allele.

The output is a Phred-scaled p-value. The higher the output value, the more likely there is to be bias. More bias is indicative of false positive calls.

Statistical notes
See the method document on statistical tests for a more detailed explanation of this application of Fisher's Exact Test.

Caveats
- The FisherStrand test may not be calculated for certain complex indel cases or for multi-allelic sites.
- FisherStrand is best suited for low coverage situations. For testing strand bias in higher coverage situations, see the StrandOddsRatio annotation.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036349412-FisherStrand

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# StrandOddsRatio
Allele-specific strand bias estimated by the Symmetric Odds Ratio test
Strand bias is a type of sequencing bias in which one DNA strand is favored over the other, which can result in incorrect evaluation of the amount of evidence observed for one allele vs. the other. The AS_StrandOddsRatio annotation is one of several methods that aims to evaluate whether there is strand bias in the data. It is an updated form of the Fisher Strand Test that is better at taking into account large amounts of data in high coverage situations. It is used to determine if there is strand bias between forward and reverse strands for the reference or alternate allele. It does so separately for each allele. The reported value is ln-scaled.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036714771-AS-StrandOddsRatio

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# StrandBiasBySample
Number of forward and reverse reads that support REF and ALT alleles
Strand bias is a type of sequencing bias in which one DNA strand is favored over the other, which can result in incorrect evaluation of the amount of evidence observed for one allele vs. the other. The StrandBiasBySample annotation produces read counts per allele and per strand that are used by other annotation modules (FisherStrand and StrandOddsRatio) to estimate strand bias using statistical approaches.

This annotation produces 4 values, corresponding to the number of reads that support the following (in that order):
- the reference allele on the forward strand
- the reference allele on the reverse strand
- the alternate allele on the forward strand
- the alternate allele on the reverse strand

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036715611-StrandBiasBySample

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# QualByDepth
Variant confidence normalized by unfiltered depth of variant samples
This annotation puts the variant confidence QUAL score into perspective by normalizing for the amount of coverage available. Because each read contributes a little to the QUAL score, variants in regions with deep coverage can have artificially inflated QUAL scores, giving the impression that the call is supported by more evidence than it really is. To compensate for this, we normalize the variant confidence by depth, which gives us a more objective picture of how well supported the call is.

Statistical notes
The QD is the QUAL score normalized by allele depth (AD) for a variant. For a single sample, the HaplotypeCaller calculates the QD by taking QUAL/AD. For multiple samples, HaplotypeCaller and GenotypeGVCFs calculate the QD by taking QUAL/AD of samples with a non hom-ref genotype call. The reason we leave out the samples with a hom-ref call is to not penalize the QUAL for the other samples with the variant call.

Caveat
This annotation can only be calculated for sites for which at least one sample was genotyped as carrying a variant allele.

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# Coverage
Total depth of coverage per sample and over all samples (DP)
This annotation is used to provide counts of read depth at two different levels, with some important differences. At the sample level (FORMAT), the DP value is the count of reads that passed the caller's internal quality control metrics (such as MAPQ > 17, for example). At the site level (INFO), the DP value is the unfiltered depth over all samples.

See the method documentation on using coverage information for important interpretation details.

Caveats
If downsampling is enabled (as is done by default for some analyses to remove excessive coverage), the depth of coverage effectively seen by the caller may be inferior to the actual depth of coverage in the original file. If using "-dcov D", the maximum depth that can be seen for N samples will be N * D.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036823751-Coverage

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# DepthPerAlleleBySample
Depth of coverage of each allele per sample
Also known as the allele depth, this annotation gives the unfiltered count of reads that support a given allele for an individual sample. The values in the field are ordered to match the order of alleles specified in the REF and ALT fields: REF, ALT1, ALT2 and so on if there are multiple ALT alleles.

See the method documentation on using coverage information for important interpretation details.

Caveats
The AD calculation as performed by HaplotypeCaller may not yield exact results because only reads that statistically favor one allele over the other are counted. Due to this fact, the sum of AD may be different than the individual sample depth, especially when there are many non-informative reads.
Because the AD includes reads and bases that were filtered by the caller (and in case of indels, is based on a statistical computation), it should not be used to make assumptions about the genotype that it is associated with. Ultimately, the phred-scaled genotype likelihoods (PLs) are what determines the genotype calls.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036822131-DepthPerAlleleBySample

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0


# DepthPerSampleHC
Depth of informative coverage for each sample.
This annotation is similar to the sample-level DP annotation, which counts read depth after general filtering, but with an extra layer of stringency. Its purpose is to provide the count of reads that are actually considered informative by HaplotypeCaller (HC), using pre-read likelihoods that are produced internally by HC.

In this context, an informative read is defined as one that allows the allele it carries to be easily distinguished. In contrast, a read might be considered uninformative if, for example, it only partially overlaps a short tandem repeat and it is not clear whether the read contains the reference allele or an extra repeat.

See the method documentation on using coverage information for important interpretation details.

Caveats
- This annotation can only be generated by HaplotypeCaller (it will not work when called from VariantAnnotator).

Related annotations
- DepthPerAlleleBySample calculates depth of coverage for each allele per sample (AD).
- Coverage gives the filtered depth of coverage for each sample and the unfiltered depth across all samples.

URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036454292-DepthPerSampleHC

Example
chr1	1233873	.	T	C,<NON_REF>	0	.	BaseQRankSum=-2.063;ClippingRankSum=0.000;DP=13;ExcessHet=3.0103;MLEAC=0,0;MLEAF=0.00,0.00;MQRankSum=0.000;RAW_MQ=46800.00;ReadPosRankSum=-1.391	GT:AD:DP:GQ:PGT:PID:PL:SB	0/0:11,2,0:13:25:1|0:1233870_A_C:0,25,415,39,420,434:6,5,2,0





URL: https://gatk.broadinstitute.org/hc/en-us/articles/360036821931-QualByDepth

