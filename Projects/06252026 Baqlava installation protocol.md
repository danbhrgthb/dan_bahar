Sources:
- [https://github.com/biobakery/baqlava/blob/master/readme.md#requirements](https://github.com/biobakery/baqlava/blob/master/readme.md#requirements)
- [https://github.com/biobakery/humann/blob/master/readme.md](https://github.com/biobakery/humann/blob/master/readme.md)
- [https://github.com/biobakery/anadama2/blob/master/readme.rst](https://github.com/biobakery/anadama2/blob/master/readme.rst) 
    
## Dependency installation

Before running this protocol, make sure your machine is set up:

- [Initial Mac setup](07072026%20Initial%20mac%20setup.md) — installs Homebrew and git
- [Conda](07072026%20conda%20protocol.md) — package and environment manager

### Building the environment
Building the environment (baqlava_env), then installing baqlava within the environment
```
conda create -n baqlava_env python=3.10
conda activate baqlava_env
conda install -c bioconda -c conda-forge pandas scipy biopython humann=3.9 anadama2=0.10.0 baqlava
```

In the above command, the -c flag represents a channel. In this case, we are looking to install the packages from two separate channels, bioconda and conda-forge.

### Testing HUMAnN and BAQLaVa on sample demo data

Testing humann:
```
humann_test
```

Testing BAQLaVa, in a separate delete-able folder “baqlava_test,” using demo data:
```
mkdir -p ~/baqlava_test
cd ~/baqlava_test
git clone https://github.com/biobakery/baqlava.git
mkdir -p ~/baqlava_test/demo_output
    
baqlava -i ~/baqlava_test/baqlava/examples/demo.fq  -o ~/baqlava_test/demo_output --nucdb ~/baqlava_test/baqlava/examples/BAQLaVa.V0.5.nucleotide/  --protdb ~/baqlava_test/baqlava/examples/BAQLaVa.V0.5.protein/  --bypass-bacterial-depletion
```

For the line of code above, baqlava is the command that we previously installed itself. The -i flag is the input, in this case the /baqlava_test/baqlava/examples/BAQLaVa_demo.fq. The -o flag is the output directory, in this case ~/baqlava_test/demo_output. The next two flags reference a demo nucleotide and a protein database, respectively, within the examples directory. The final flag --bypass tells baqlava to ignore bacteria within the sample, as the example dataset do not contain those (Probably the only time bypassing will be needed).

```
pwd 
	- Ensure that you are in demo_output
ls
cat <filename shown on ls>
```

### Installing the Chocophlan database
```
mkdir -p ~/databases
humann_databases --download chocophlan full ~/databases 
baqlava_database --download database baqlava-db ~/databases 
```
What is chocophlan? It is a reference database of species-level microbial nucleotide sequences within HUMAnN, allowing for functional profiling of microbes.
  
Of note, it is possible that the following website is down: huttenhower.sph.harvard.edu. To check if the website is down, go here: [https://downforeveryoneorjustme.com](https://downforeveryoneorjustme.com/)



------------------------------------------------------------------------
After installing baqlava, here is a sample of how it can be run on files within "kneaddata" folder within the Desktop
```
mkdir -p ~/Desktop/baqlava_runs/A00062
baqlava -i ~/Desktop/kneaddata/A00062_combined.fastq.gz -o ~/Desktop/baqlava_runs/A00062
```

Note: unlike the demo, real runs would benefit from [multi thread processing](07012026%20multi%20thread%20processing.md). baqlava defaults to a single thread, which is very slow — add a `--threads <N>` , where N = number of cores available.
