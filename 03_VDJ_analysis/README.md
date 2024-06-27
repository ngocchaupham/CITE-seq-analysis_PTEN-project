# VDJ analysis
## Overview
This repository describes how the VDJ data analysis was performed with Immcantation, then with Seurat. It contains the instructions to reproduce the analysis. To reproduce the analysis, you have to first, prepare the environments (see "Prerequisites" section below), then execute the analysis described in the "Run the analysis" section below.
Source code is directly available in the github repository https://github.com/ngocchaupham/CITE-seq-analysis_PTEN-project/03_VDJ_analysis
The VDJ analysis contained two scripts :
- B6_merge_VDJ_analysis.Rmd
- BC_merge_VDJ_analysis.Rmd
---
### Environment Setup

For TCR analysis, we used IgBlast implemented in the Immcantation package, contained in the Docker image: `Immcantation450`.
You will need:
- Cell Ranger VDJ output located in  `$WORKING_DIR/PTEN/03_Analysis/Analysis2024/TCR` or `$WORKING_DIR/02_Preprocessing/cellranger702/*/*/outs/per_sample_outs/*/vdj_t`
- Docker image is available at `$WORKING_DIR/Docker/Immcantation450`,if not you can download on [zenodo](https://zenodo.org/uploads/10671667)
- Load the Docker image
```bash
docker load < $WORKING_DIR/Docker/Immcantation450/immcantationsuite450.tar
```
#### Output:
The output directory (e.g., `/mnt/NASBIOINFO_CP/LALT/BIOINFO/PTEN/03_Analysis/Analysis2024/TCR/BALBC/230303/`) contains the .tsv files used later in the VDJ analysis.
### R/Seurat Analysis:
Open the Rmd file: `/mnt/NASBIOINFO_CP/LALT/BIOINFO/PTEN/03_Analysis/Analysis2024/RMD/BC/merge/*_merged_VDJ_analysis.Rmd`. (replace * by `BC` or `B6)
You can either run all the code starting with the .tsv files or run only part of the code using intermediate R objects. If running part of the code, load the necessary object.
