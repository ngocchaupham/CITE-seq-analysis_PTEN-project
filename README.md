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
- 10 Fastq are availabe in [SRA](https://trace.ncbi.nlm.nih.gov/Traces/sra/?study=SRP311697) under the accession ID *SRP311697*
  - 4 Fastq files containing paired-end reads sequenced from the mRNA library of replicate 1 and 2
  - 4 Fastq files containing paired-end reads sequenced from the HTO library of replicate 1 and 2
  - 2 Fastq files containing paired-end reads sequenced from the ADT library of replicate 2
- Cellranger output that can be load in Seurat are available in [GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE169374) (*GSE169374*), under accession number :
  - Replicate 1
    - [Cellranger mRNA](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM5198190) (*GSM5198190*)
    - [Cite-seq-count HTO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM5198191) *GSM5198191*)
  - Replicate 2
    - [CellRanger mRNA](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM5198192) (*GSM5198192*)
    - [Cite-seq-count HTO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM5198193) (*GSM5198193*)
    - [Cite-seq-count ADT](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM5198194) (*GSM5198194*)

#### Seurat analysis
- All Seurat Html report containing figures and analysis that we generated with R can be [found here](02_Seurat_analysis/02_Output/Html_report/) :
- Seurat rmd script to reproduce the preprocessing can be found [here](02_Seurat_analysis/01_Script/Experiment_preprocessing.Rmd), analysis rmd script [here](02_Seurat_analysis/01_Script/Experiment_analysis.Rmd) and the script to only generate figures [here](02_Seurat_analysis/01_Script/Figures.Rmd)

#### Docker and Singularity images
Singularity/Docker images and Robj are all availabe in [Zenodo](https://zenodo.org/uploads/10671667)
