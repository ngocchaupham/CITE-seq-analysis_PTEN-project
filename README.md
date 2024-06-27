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
#### Seurat analysis
- Seurat rmd script to reproduce the preprocessing and analysis can be found [here](02_Seurat_analysis/01_Script/)
#### VDJ analysis
- VDJ analysis rmd script [here](03_VDJ_analysis/01_Script)

#### Docker and Singularity images
Singularity/Docker images and Robj are all availabe in [Zenodo](https://zenodo.org/uploads/10671667)
