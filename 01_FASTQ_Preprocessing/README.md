# FASTQ Preprocessing
## Overview
This folder contain the instructions and material to reproduce fastq pre-processing. Singularity images are respectively available Zenodo. Intructions to reproduce the analysis are provided below.
To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.

If you don't want to redo data pre-processing you can directly go to [02_Seurat_analysis](02_Seurat_analysis/README.md)

---

## Setup the experiment
### Prerequisites
In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKING_DIR variable
- Download reference genome
- Download the Cell ranger/Singularity image tar file
- Load Singularity image on your system

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder. This will create a "Pten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this Pten folder. For instance, if I clone the Git repository in "/home/pham/workspace", then the WORKING_DIR variable will be set to :

```bash
export WORKING_DIR=/home/pham/workspace/Pten
```

#### Reference Genome
Mouse transcriptome reference used is available at 10xGenomics website (https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-mm10-2020-A.tar.gz).
Mouse V(D)J reference (GRCm38) used is available at 10xGenomics website (https://cf.10xgenomics.com/supp/cell-vdj/refdata-cellranger-vdj-GRCm38-alts-ensembl-7.0.0.tar.gz).

#### Singularity Images
Singularity image.tar files are stored on Zenodo.

```bash
#Download the singularity images
# To download CellRanger
wget -P $WORKING_DIR/Images/Singularity/Pten_Cellranger https://zenodo.org/uploads/10671667/

```
#### Launch Singularity images
Singularity must be installed on your system. In order to execute analysis, you must first launch the singularity image you want to use. See https://singularity.lbl.gov/quickstart for details on Singularity installation.


#### RAW Files 

### Run the Fastq preprocessing
#### Cell Ranger multi
Input : Fastq files <br/>
Output : The ouput directory (e.g "../outs/per_sample_outs/") with the pre-processed data that is used later in the Seurat analysis
- mRNA and ADT count per cells
  - barcodes.tsv.gz
  - features.tsv.gz
  - matrix.mtx.gz

- vdj_t
  - filtered_contig.fasta
  - filtered_contig_annotations.csv

and it also produce an html report.

To run cell ranger:
```bash
# Build images
singularity build cellranger720.sif docker-archive:$WORKING_DIR/Images/Singularity/Pten_Cellranger/cellranger720.tar
# Launch singularity image
singularity shell $WORKING_DIR/Images/Singularity/Pten_Cellranger/cellranger720.sif
bash

#Go to the output directory
cd  $WORKING_DIR/01_FASTQ_Preprocessing/02_Output

#Run CellRanger
#replace by good link to file
nohup /usr/local/share/cellranger/cellranger-7.2.0/cellranger multi --id=the_name_of_the_output_file --csv=location_of_config_file.csv --localmem=256
#Replicate 2
nohup /usr/local/share/cellranger/cellranger-2.1.0/cellranger count --id=MycPten_mm10_rep2_mRNA --expect-cells=6000 --transcriptome=$WORKING_DIR/01_FASTQ_Preprocessing/03_Data/Reference/cellranger_mm10-eYFP --fastq=$WORKING_DIR/03_Data/FASTQ/ --sample=rep2_mRNA &
```
Once the analysis is done, you should get result files in the WORKING_DIR/01_FASTQ_Preprocessing/02_Output folder (with the newly created "MycPten_mm10_rep_1_mRNA" and rep2 folder)

#### cite-seq-Count
input : Fastq files are avaible in [SRP311697](https://trace.ncbi.nlm.nih.gov/Traces/sra/?study=SRP311697) <br/>
output : The ouput directory will contain the classical CiteSeqCount output with the pre-processed data that is used later in the Seurat analysis.
- HTO count per cells
  - HTO_barcodes.tsv.gz
  - HTO_features.tsv.gz
  - HTO_matrix.mtx.gz

And only for replicate 2 :
- ADT count per cells
  - ADT_barcodes.tsv.gz
  - ADT_features.tsv.gz
  - ADT_matrix.mtx.gz

Execution :
```bash
# Launch singularity image
singularity shell $WORKING_DIR/Images/Singularity/MycPten_CITE/citeseqcount141_image.tar

bash

#Go to the output directory
cd /MycPten/01_FASTQ_Preprocessing/02_Output

#FOR REPLICATE 1
# HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep1_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep1_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep1.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep1_HTO

#FOR REPLICATE 2
#HTO
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_HTO_S2_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_HTO_S2_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/HTOlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_HTO

#ADT
CITE-seq-Count -R1 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_ADT_S3_R1.fastq.gz -R2 $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/FASTQ/rep2_ADT_S3_R2.fastq.gz -t $WORKING_DIR/01_FASTQ_Preprocessing/03_Data/ADTlist_rep2.csv -cbf 1 -cbl 16 -umif 17 -umil 26 --max-errors 2 -cell 40000 -o MycPten_rep2_ADT
```
