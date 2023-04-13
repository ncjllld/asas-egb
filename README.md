# ASAS-EGB

ASAS-EGB is a library for estimating allele-specific
alternative splicing events using transcriptome data.

## Installation

ASAS-EGB is released as a Python package which requires **Python 3.7** 
or higher to be installed on the computer.

To install ASAS-EGB, some Python packages that ASAS-EGB depends on 
should be installed first. In order to successfully compile 
some of the packages, several system libraries should be 
pre-installed. For example, on **Ubuntu**, these libraries 
may need to be installed:

```shell
sudo apt install zlib1g-dev libbz2-dev liblzma-dev
```

Then, use `pip` to install dependent packages:
```shell
pip install --user numpy scipy pandas cython
pip install --user pymc3 pyarrow
pip install --user pysam htseq
```

Then, use `pip` to install ASAS-EGB:
```shell
pip install --user asas-egb
```

*After the installation, if you cannot run `asas-egb` from the terminal, 
this is caused by the executable binary file `asas-egb` not being found 
in the system path, you may need to run:*
```shell
export PATH=~/.local/bin:$PATH
``` 

To use the **plot module**, `matplotlib` should also be 
installed:
```shell
pip install --user matplotlib
```

# Example

To demonstrate the use of ASAS-EGB, an example is provided, it can be downloaded at: [asas-egb_example.zip](https://github.com/ncjllld/asas-egb/blob/main/asas-egb_example.zip?raw=true).

Unzip the file and enter the directory `asas-egb_example`.

**Build database**
```shell
asas-egb build-database -e inputs/as_events.gff3 -f inputs/genes.gff3 -a "gene_name" -v inputs/snps.vcf -C -s "NA12878" -o db
```

**Inference**
```shell
asas-egb inference -n 2 -d db -b inputs/alignments.bam -L 54 -P -M 103.46 -S 19.25 -o results
```

**Stats**
```shell
asas-egb stats -d results
```

**Plotting**

Plot in event isoform view: 

```shell
asas-egb plot -d results -i "SE.1083-PHASED"
```

Plot in gene isoform view:

```shell
asas-egb plot -d results -i "SE.1083-PHASED" -g
```
