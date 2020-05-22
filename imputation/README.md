# Workflow for genotype imputation against reference panel

The following workflow takes genotypes in plink binary format (.bed/.bim/.fam),
phases them via PhaseIt, followed by imputation against a reference panel via
impute2.

The workflow is organised via snakemake, with rules in the rules directory
and accompanying scripts in the scripts subdirectory. Parameters are specified
in the config/config.yaml file, with example parameters in the provided
config.yaml. config/cluster.json is an example json file for running the
workflow on a UGE high-performance computing cluster.

After running this analysis, phased and imputed genotypes, as well as quality
control plots will be returned in the following results directory structure:

```
dir
│   README.md
│
└───unphased
│   │   name.chr1.bed name.chr1.bim name.chr1.fam
│   │   name.chr2.bed name.chr2.bim name.chr2.fam
│   │   ...
│   │   name.chr22.bed name.chr22.bim name.chr22.fam
│
└───phased
│   │   name.chr1.hap.gz name.chr1.sample
│   │   name.chr2.hap.gz name.chr2.sample
│   │   ...
│   │   name.chr22.hap.gz name.chr22.sample
│
└───imputed
│      └───chr1
│      │    │   name.chr1.1.gen name.chr1.1.gen_samples name.chr1.1.gen_info ...
│      │    │   name.chr1.2.gen name.chr1.2.gen_samples name.chr1.2.gen_info ...
│      │    │   ...
│      │    │   name.chr1.lastchunk.gen name.chr1.lastchunk.gen_samples name.chr1.lastchunk.gen_info ...
│      │
│      └───
│      │
│      └───chr22
│           │   name.chr22.1.gen name.chr22.1.gen_samples name.chr22.1.gen_info ...
│           │   name.chr22.2.gen name.chr22.2.gen_samples name.chr1.2.gen_info ...
│           │   ...
│           │   name.chr22.lastchunk.gen name.chr22.lastchunk.gen_samples name.chr22.lastchunk.gen_info ...
│
└───genotypes
│   │   name.chr1.gen.gz name.chr1.qc.gen.gz name.chr1.sample ...
│   │   name.chr2.gen.gz name.chr2.qc.gen.gz name.chr2.sample ...
│   │   ...
│   │   name.chr22.gen.gz name.chr22.qc.gen.gz name.chr22.sample ...
│
└───counts
│   │   chr1.SNPsPerChunk.txt chr1.numbers.txt chr1.data.txt
│   │   chr2.SNPsPerChunk.txt chr2.numbers.txt chr2.data.txt
│   │   ...
│   │   chr22.SNPsPerChunk.txt chr22.numbers.txt chr22.data.txt
│
└───bgen (optional)
│
└───bimbam (optional)

```