# Transcriptomics-based-models-Promote-study


This R script performs multiple steps of RNA-seq differential gene expression analysis for the PROMOTE study, including data filtering, preprocessing, and visualization. Then feature selection and model building, with a focus on identifying predictors of hormonal treatment response in endometrial cancer.

---

## Input data

The analysis requires the following input files:

- PROMOTE2samplechangeRR60samples.csv
- PROMOTE2.csv
- PROMOTE2.1.csv
- foldchangeJ.csv
- RRfoldchangeJ.csv
- 20260128stagepcacbr.csv
- 97genesCBRYN.csv
- 20251218selectedcbr+5clinic
- 20251212wholeCBR+5clinic
- 1211clinicmerge

- 20251218selectedRR+5clinic.csv
- 103RRYN.csv
- 20251212wholeRR+5clinic
- 20251212mergeRR

- 5clinicRFE_CBR.rds
- 5clinic+wholeDEGSRFE_CBR.rds
- DEGSRFE_CBR.rds
- 202512185clinic+selectedDEGSRFE_CBR.rds

- wholeDEGSRFE_RR.rds
- 5clinicRFE_RR.rds
- wholedegsRR+5clinicRFE_RR.rds
- 20251218selecteddegsRR+5clinicRFE_RR.rds

---

## Requirements

### Software
- R >= 4.2.0

### Key R packages
- tidyverse
- DESeq2
- caret
- glmnet
- ComplexHeatmap
- survival

## How to run the analysis

1.  Open the project root directory in RStudio
    
2.  Ensure all file paths are defined relative to the project root
    
3.  Run the main analysis report
   ```r
    rmarkdown::render("FOR PROMOTE.Rmd")
