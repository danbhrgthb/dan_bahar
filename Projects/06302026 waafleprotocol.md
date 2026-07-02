WAAFLE (a Workflow to Annotate Assemblies and Find LGT Events) is a program for finding lateral gene transfers in assembled metagenomes, just like the ones in the KneadData folder.

Source: https://github.com/biobakery/waafle/blob/main/README.md


Step 1: Creating a new conda environment
```
conda create -n waafle python=3
conda activate waafle
```

Step 2: Setting up channel priorities

Conda downloads packages from online repositories called channels. Each conda config --add channels command puts adds a channel to a "priority" list, and the last one added has the highest priority. Therefore, it is important that you type out the following in order:
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --add channels biobakery
```

Step 3: Installing waafle, then making sure it was properly installed
```
conda install waafle -c biobakery
waafle_search --help
```

Step 4: Downloading the reference databases
```
brew install wget

wget https://huttenhower.sph.harvard.edu/waafle_data/chocophlan.v202210_202403.waafledb.tar.gz

wget https://huttenhower.sph.harvard.edu/waafle_data/chocophlan.v202210_202403.taxonomy.tsv

tar -xzvf chocophlan.v202210_202403.waafledb.tar.gz

```
The last line unpacks the the BLAST database.

Note to self: link to multi threading protocol
