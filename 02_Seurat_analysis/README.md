# Seurat analysis
## Overview
This repository describes how the scRNAseq data analysis was performed with Seurat. It contains the instructions and material to reproduce the analysis reported in the article.To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.
Source code is directly available in the github repository [https://github.com/ngocchaupham/CITE-seq-analysis_PTEN-project/](https://github.com/ngocchaupham/CITE-seq-analysis_PTEN-project/02_Seurat_analysis/README.md)
Html report produce through the analysis is directly availabe (https://github.com/ngocchaupham/CITE-seq-analysis_PTEN-project/02_Output/Html_report).
The Seurat analysis is divided in two script of each mouse models :
- *merged_preprocessing.rmd* to load our data and obtain our final Seurat object before starting the scRNA seq analysis
- *merged_analysis.rmd* to start the scRNA seq analysis

You can also just generate the plot used in my report :
- *Figure.rmd*

Required data, builded Docker images and Robj are all available in Zenodo. Instructions to reproduce the analysis are provided below.

---

## Setup the experiment
### Prerequisites
Docker container images are available on [zenodo](https://zenodo.org/uploads/10671667).

In order to prepare the environment for analysis execution, it is required to:
- Clone this github repository and set the WORKING_DIR variable
- Download the RStudio / Seurat docker image tar file
- Load the docker image on your system
- Download files to perform the analysis on [zenodo](https://zenodo.org/uploads/10671667).

#### Clone Github repository
Use your favorite method to clone this repository in a chosen folder.This will create a "Pten" folder with all the source code. <br/>
You must set an environment variable called WORKING_DIR with a value set to the path to this Pten folder.
For instance, if I clone the Git repository in "/home/pham/workspace", then the WORKING_DIR variable will be set to :

```bash
export WORKING_DIR=/home/pham/workspace/Pten
```

#### Docker images
> :warning: In order to execute analysis, you must load the provided docker images onto your Docker. Docker must be installed on your system. See https://docs.docker.com/install/ for details on Docker installation.

Docker image file is stored on Zenodo :

```bash
# To download Seurat501
wget -P $WORKING_DIR/Docker https://zenodo.org/uploads/10671667/files/sc_analysis_2.tar
```
Load docker image
```bash
docker load < $WORKING_DIR/Docker/sc_analysis_2.tar
```

#### Data
- merged_preprocessing.rmd
  - Files after Fastq Preprocessing (count matrix) are already in this repository (WORKING_DIR/PTEN/02_Preprocessing/cellranger702/*/*/outs/per_sample_outs/)
  - Preprocessed Seurat objects are stored at PTEN/03_Analysis/Analysis2024/RObject
  - First merged objects : merge_B6_2024.Robj (B6 model) and merge_2023exp.Robj (BC model)
- merged_analysis.rmd
  - Final merged object, produce by merged_preprocessing, to launch the scRNAseq analysis : merge_B6ccregress_2024.Robj (B6 model) and merge_2023exp_reg_cc.Robj (BC model)

> :warning: **Do not move any data.**  When launching B6_merged_analysis.rmd or BC_merged_analysis, it will use our data in WORKING_DIR/PTEN/03_Analysis/Analysis2024/RObject/B6 or WORKING_DIR/PTEN/03_Analysis/Analysis2024/RObject/BC
### Run the R/Seurat analysis

- B6_merged_preprocessing.rmd and BC_merged_preprocessing <br/>
You can either run all the code (starting with count matrix in repository by default) or run only part of the code with our intermediate Robj.
- B6_merged_analysis.rmd and BC_merged_analysis <br/>
When launching B6_merged_analysis.rmd or BC_merged_analysis, it will use our data in WORKING_DIR/PTEN/03_Analysis/Analysis2024/RObject/B6 or WORKING_DIR/PTEN/03_Analysis/Analysis2024/RObject/BC

#### Execution
To get into the RStudio environnement and run the analysis yourself use the following command:

```bash
docker run -d --name sc_analysis -p 8888:8888 -v $WORKING_DIR/PTEN/03_Analysis/Analysis2024/:/home/${USER}/workspace -e USER=$(whoami) -e USERID=$(id -u) -e GROUPID=$(id -g) -e PASSWORD=choose sc_analysis
```
And open the Rmd file that you want.
