# Useful tools and command for epigenomic data analysis 


# 1. ATAC-Seq data
Starting with fastq files, first thing to do is preparing Samplesheet in json format for ENCODE pipeline input, which should include name of the fastqs, directory of genome annotation and a few more details which could be found in [here](https://github.com/ENCODE-DCC/atac-seq-pipeline/blob/master/example_input_json/template.json).

These files cromwell-47.jar, womtool-47.ja and atac.wtl are necessary for running the pipline and usually they could be found in the directory where the pipeline is installed. 

For more detail about intstallation, click [here](https://github.com/ENCODE-DCC/atac-seq-pipeline)

module load atac-seq-pipeline/1.5.4\

caper run /path/to/atac.wtl -i /path/to/Samplesheet.json --womtool /path/to/womtool-47.jar --cromwell /path/to/cromwell-47.jar


When the job is finished, you could have access to ouput files with another tool called croo. 



