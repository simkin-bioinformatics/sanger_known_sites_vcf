# sanger_known_sites_vcf
filters sanger Pf8 data from 33,325 samples to high quality "PASS" genotypes
that then serve as known mutations for other pipelines.

Our main pipelines that use such a file of "known" mutations are GATK pipelines
that use base quality score recalibration (BQSR) - GATK bqsr uses known
mutations and a bam file as input and uses the known mutations to recalibrate
estimates of the base quality scores of the original reads.

The Pf8 project is described here:
https://www.malariagen.net/data_package/open-dataset-plasmodium-falciparum-v80/

and also here:
https://wellcomeopenresearch.org/articles/10-325/v1

This pipeline gathers data primarily from this web-hosted list of short variant
genotypes:
https://pf8-release.cog.sanger.ac.uk/vcf/index.html

Our pipeline downloads each file, filters for PASS variants, and removes the
individual genotypes associated with each of the 33,325 samples, before deleting
the original file to avoid filling the hard drive.

The resulting (much smaller sized) PASS variants are then concatenated to form a
VCF of known variable sites in the genome.

# Installation

# Running instructions