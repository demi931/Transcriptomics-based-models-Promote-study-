# Transcriptomics-based-models-Promote-study


This R script performs multiple steps of RNA-seq differential gene expression analysis for the PROMOTE study, including data filtering, preprocessing, and visualization. Then, feature selection and model building, with a focus on identifying predictors of hormonal treatment response in endometrial cancer.

---
## Requirements

### Software
- R >= 4.2.0

### Key R packages version
- tidyverse 2.0.0
- ggplot 3.4.4
- ggforce 0.4.1
- DESeq2 1.42.0
- caret 6.0.94
- glmnet 4.1.8
- ComplexHeatmap 2.18.0
- pheatmap 1.0.12
- readr 2.1.4
- pROC 1.18.5

## Installation
git clone https://github.com/your-username/Transcriptomics-based-models-Promote-study-.git

cd Transcriptomics-based-models-Promote-study-

## Overview of the Analysis Workflow

The workflow follows these main steps:

1.  **Data preprocessing**
    
2.  **PCA for assessment of regional effects**
    
3.  **Differential expression analysis (DESeq2)**
    
4.  **Heatmap visualization of response-associated genes**

5.  **Exploratory PCA of transcriptomic profiles**
    
6.  **Feature selection using logistic regression + RFE**
    
7.  **Model evaluation (AUC, sensitivity, specificity)**
    
8.  **Visualization of selected predictors**



## Example Usage
1.**Principal Component Analysis (PCA)**

PCA is used to explore sample clustering based on gene expression profiles and clinical variables.
```
pcdat <- prcomp(expr_matrix, scale. = TRUE)

ggplot(pca_scores, aes(PC1, PC2, colour = Response, shape = Stage)) +
  geom_point(size = 3) +
  theme_classic()
```
This allows visual inspection of the separation between responders and non-responders.

2. **Differential Expression Analysis (DESeq2)**
DESeq2 is applied to identify genes differentially expressed between response groups.
```dds <- DESeqDataSetFromMatrix(
  countData = round(count_matrix),
  colData   = metadata,
  design    = ~ CBR
)

dds <- DESeq(dds)
res <- results(dds)
```
Genes are classified as UP, DOWN, or NOT CHANGE based on log2 fold change and adjusted p-value.
3. ** Heatmap Visualization**
Differentially expressed genes are visualized using heatmaps to compare response groups:
```
pheatmap(
  expr_matrix,
  scale = "row",
  annotation_col = annotation_col,
  show_rownames = FALSE
)
```
This is performed separately for clinical benefit and response.
4. **Feature Selection with Logistic Regression + RFE, and Model Evaluation**
Recursive Feature Elimination (RFE) is used to identify optimal gene and clinical feature subsets.
```
RFE_CBR <- performLogitRfe(
  data_sample,
  condition_sample,
  sizesPerIteration = 2:25
)
createROCCurve(glmProfileIndividual, condition_test, data_test)
```
Model performance is evaluated using sensitivity, specificity, and overall accuracy.
Final models are saved as `.rds` objects for reuse and validation.

5. **Visualization of Selected Predictors**
Dot plots are used to visualize distributions of selected predictors between response groups:
```
ggplot(plot_df_long, aes(x = group_label, y = value)) +
  geom_jitter(width = 0.15) +
  facet_wrap(~ variable, scales = "free_y")
  ```

## Key Functions

`performLogitRfe()` Performs logistic regression with RFE

`calculateVariableImportance()` Computes mean/median importance scores

`reduceVariablesLogit()` Iteratively reduces features and evaluates models

`createROCCurve()` Generates ROC curves and AUC

`calculateAccuracy()` Computes sensitivity, specificity, and accuracy


## Reproducibility Notes

-   Random seeds are fixed where applicable (`set.seed(1)`)
    
-   Train/test splits are explicitly defined
    
-   Models are saved as `.rds` files for reproducibility （Feature selection is based on resampling-based RFE; therefore,
  selected features may vary slightly between runs, while overall
  model performance remains stable）

##  License

MIT License

© PROMOTE Study / Maastricht University  
    rmarkdown::render("FOR PROMOTE.Rmd")
