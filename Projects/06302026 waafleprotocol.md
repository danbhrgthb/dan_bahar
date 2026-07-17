- Source: https://github.com/biobakery/waafle/blob/main/README.md

## Overview

WAAFLE finds horizontal gene transfer events within metagenomes. WAAFLE scans contigs for “unexpected,” or novel, gene sequences that do not fit that taxa’s expected sequence. When a contig contains a sequence of genes that appears to originate from elsewhere, WAAFLE labels that as a possible horizontal gene transfer event.

## Dependency installation

Before running this protocol, make sure your machine is set up:

- [Initial Mac setup](07072026%20Initial%20mac%20setup.md) — install Homebrew, git, and wget
- [Conda](07072026%20conda%20protocol.md) — package and environment manager

### Building the environment

Building the environment (waafle), then installing waafle within it:

```
conda create -n waafle python=3.10
conda activate waafle
```

Now install waafle:

```
conda install -c default -c biobakery -c conda-forge -c bioconda waafle
```

As in the BAQLaVa protocol, the -c flag specifies a channel names, a repository that is online. Conda finds WAAFLE across these channels (listed from least priority to top priority) and downloads it along with its dependencies.

### Testing WAAFLE

```
waafle_search --help
```

If waafle is installed correctly, this prints the help menu.

### Downloading databases

```
mkdir -p ~/databases/waafle
cd ~/databases/waafle
wget <https://huttenhower.sph.harvard.edu/waafle_data/chocophlan.v202210_202403.waafledb.tar.gz>
wget <https://huttenhower.sph.harvard.edu/waafle_data/chocophlan.v202210_202403.taxonomy.tsv>

tar -xzvf chocophlan.v202210_202403.waafledb.tar.gz
```

The wget lines download the WAAFLE BLAST database; the final tar -xzvf line unpacks the BLAST database.

Of note, huttenhower.sph.harvard.edu occasionally goes down. To check, visit downforeveryoneorjustme.com.

### Running WAAFLE

WAAFLE runs in two steps on your assembled contigs:
```
waafle_search A00387_contigs.fna ~/databases/waafle/chocophlan.v202210_202403.waafledb
```
This command blasts the contigs along the WAAFLE database

```
waafle_orgscorer A00387_contigs.fna A00387_contigs.blastout ~/databases/waafle/chocophlan.v202210_202403.taxonomy.tsv A00387
```
This command identifies al the lateral gene transfer events.

Note: Runs would benefit from [multi thread processing](07012026%20multi%20thread%20processing.md). Use a —threads (N) flag (N = number of cores available) for meaningful runs. See multi thread processing.
