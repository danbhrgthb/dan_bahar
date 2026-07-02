Sources:
- [https://github.com/biobakery/baqlava/blob/master/readme.md#requirements](https://github.com/biobakery/baqlava/blob/master/readme.md#requirements)
- [https://github.com/biobakery/humann/blob/master/readme.md](https://github.com/biobakery/humann/blob/master/readme.md)
- [https://github.com/biobakery/anadama2/blob/master/readme.rst](https://github.com/biobakery/anadama2/blob/master/readme.rst) 
    

Part 1: Installing Homebrew and system-level packages:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"*
brew install git bowtie2 diamond
```
	git: the control system
	bowtie2: short-read aligner used by HUMAnN
	diamond: fast protein aligner used by HUMAnN

Part 2: Installing Conda and creating a BAQLaVa environment.
```
brew install miniconda
conda init zsh
source ~/.zshrc
conda create -n baqlava_env python=3.10
conda activate baqlava_env
```

'conda activate' moves into the new baqlave_env environment, labeled (baqlava_env). Ensure that you stay in it for the remainder of the protocol. In order to move out of it back to “(base)”, type *conda deactivate*
    
Conda is a tool that creates isolated environments within your computer. Now, we created and activated the (baqlava_env). Make sure you are in this environment when installing local packages.


Part 3: Building the environment (baqlava_env), then installing baqlava within the environment
```
pip install --upgrade pip setuptools wheel
pip install pandas scipy biopython
pip install humann==3.9
pip install anadama2==0.10.0
pip install baqlava
```  

Part 4: Testing the humann, then testing baqlava on demo data

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

Part 5: Installing the databases (chocophlan) for real runs within baqlava_env
​
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

Note, no flags are needed as it will assume standard for all.