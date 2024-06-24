# CITE-seq-analysis_PTEN-project
Deciphering the impact of PTEN-loss in T-cell Leukemogenesis:  A multimodal single-cell analysis

If you have any questions on this analysis, please contact [Ngoc Chau Pham](ngoc-chau.pham@univ-amu.fr)

---

### Overview
This repository contains instructions and material to reproduce the analysis. Source code is available in this github repository. Required data and builded Docker/singularity images are available in Zenodo. Instructions to reproduce the analysis are provided in the different subdirectories:

- Fastq preprocessing is discribed in the 01_FASTQ_Preprocessing folder <br/>
In order to re do Fastq preprocessing you can follow guidelines and script here : [01_FASTQ_Preprocessing](01_FASTQ_Preprocessing/README.md)
- Seurat analysis is discribed in the 02_Seurat_analysis folder <br/>
In order to re do Seurat Analysis you can follow guidelines and script here : [02_Seurat_analysis ](02_Seurat_analysis/README.md)
- VDJ analysis is discribed in the 03_VDJ_analysis folder <br/>
In order to re do VDJ Analysis you can follow guidelines and script here : [03_VDJ_analysis ](03_VDJ_analysis/README.md)
---

### Data Availability
#### Fastq preprocessing
- All Cell Ranger Html report can be [found here](01_FASTQ_Preprocessing/Html_report/) :
#### Seurat analysis
- All Seurat Html report containing figures and analysis that we generated with R can be [found here](02_Seurat_analysis/02_Output/Html_report/) :
- Seurat rmd script to reproduce the preprocessing can be found [here](02_Seurat_analysis/01_Script/Experiment_preprocessing.Rmd), analysis rmd script [here](02_Seurat_analysis/01_Script/Experiment_analysis.Rmd) and the script to only generate figures [here](02_Seurat_analysis/01_Script/Figures.Rmd)

#### VDJ analysis
- All Seurat Html report containing figures and analysis that we generated with R can be [found here](02_Seurat_analysis/02_Output/Html_report/) :
- VDJ analysis rmd script [here](03_VDJ_analysis/01_Script/Experiment_analysis.Rmd) and the script to only generate figures [here](03_VDJ_analysis/01_Script/Figures.Rmd)

#### Docker and Singularity images
Singularity/Docker images and Robj are all availabe in [Zenodo](https://zenodo.org/uploads/10671667)
