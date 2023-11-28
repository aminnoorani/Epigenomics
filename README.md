# Useful tools and command for epigenomic data analysis 


# 1. ATAC-Seq data (ENCODE)
Starting with fastq files, first thing to do is preparing Samplesheet in json format for ENCODE pipeline input, which should include name of the fastqs, directory of genome annotation and a few more details which could be found in [here](https://github.com/ENCODE-DCC/atac-seq-pipeline/blob/master/example_input_json/template.json).

These files cromwell-47.jar, womtool-47.ja and atac.wtl are necessary for running the pipline and usually they could be found in the directory where the pipeline is installed. 

For more detail about intstallation, click [here](https://github.com/ENCODE-DCC/atac-seq-pipeline)

module load atac-seq-pipeline/1.5.4\

caper run /path/to/atac.wtl -i /path/to/Samplesheet.json --womtool /path/to/womtool-47.jar --cromwell /path/to/cromwell-47.jar


When the job is finished, you could have access to ouput files with another tool called croo. 

There will be a METADATA_JSON_FILE, in where the job was submited in the first place. croo /path/to/METADATA_JSON_FILE shows you what file is in which directory. 

# 2. Cut&Run (nf-core)
There are few steps to make nf-core productive, otherwise you will face many errors along the way.

I assumed conda is installed already. First, we create conda environment with nextflow and python, and install neccassary modules. Commands below will do them all for you, it might takes a bit long to have them all ready.

conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

conda create --name nf-core nextflow
conda activate nf-core
#test
nextflow run hello

#conda install prettier
#conda install python=3.9
#conda install -c bioconda seacr
#conda install bioconda::picard=3.0.0=hdfd78af_1
#conda install deeptools

conda install prettier python=3.9 deeptools -c bioconda seacr bioconda::picard=3.0.0=hdfd78af_1


module load bowtie2
module load bamtools/2.4.2
module load ucsctools/378
module load trim_galore/0.6.6
module load bedtools
module load samtools
module load java



Preparing samplesheet like below and if there is no igg or control, at the end of scripts --use_control 'false' should be written.

group,replicate,fastq_1,fastq_2,control
H3K27ac_CCR2,1,CCR2_S11_R1_001.fastq.gz,CCR2_S11_R2_001.fastq.gz,igg_ctrl
igg_ctrl,1,Negative_S15_R1_001.fastq.gz,Negative_S15_R2_001.fastq.gz,

Script for submitting job:

~/nextflow run nf-core/cutandrun --input ~/path/to/samplesheet.csv --igenome_base ~/Bowtie2Index --fasta ~/hg38_genome.fa --gtf ~/h38_genes.gtf --spikein_fasta ~/Lambda_genome.fa
