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

You can install pixi from the following website:
https://pixi.prefix.dev/latest/installation/

Once you have pixi installed, you can clone this repository and change directory
into the cloned folder, then install the pixi environment with pixi install

# Running instructions

You can run the pipeline with pixi run filter_known_sites. The final output file
will be a file located in known_sites/known_sites.vcf.gz - you can use this in
downstream applications like gatk bqsr.

# Future compatibility

If the sanger institute comes out with a similar list of vcf files that need to
be edited in the future, you may need to make three edits:
 - You will likely want to edit sanger_vcf_file_links.txt to point to new links,
   or create a new text file with new links.
 - filter_bqsr.smk line 16 may need to be edited to point to an alternative text
   file if you created one in the edit above.
 - You will likely need to edit the url_path variable in line 28 to use a
   different url prefix.
