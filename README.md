
# Predicting Drug Response from Clinical + Molecular Biomarkers using Logistic Regression

🎯 # Goal
Predict response to an EGFR inhibitor in lung cancer cell lines using clinical-like and molecular biomarkers.

Build an interpretable logistic regression model that predicts drug response using as features *clinical variables* and *molecular biomarkers*(in this case we will use mutations).

🧪 Specifically we will model:
* Response to an EGFR inhibitor in lung cancer

📌 Prediction Task
Binary classification:
* 1	Drug-sensitive
* 0	Drug-resistant

We WILL use:
✅ Mutation status (binary)
✅ Simple clinical variables
✅ Small number of features (≤15)

🧠 ML Model
Logistic Regression
With L1 / Elastic Net regularization

🎯 What Data We Need

To predict drug response, we need three things:

Drug response labels

Clinical metadata

Molecular biomarkers (mutations)

### Raw Data Sources

This project uses publicly available cell line data from DepMap (CCLE):

- Drug response (Erlotinib sensitivity)
- Somatic mutation calls
- Cell line metadata

Due to file size, raw datasets are not stored in this repository.

Download instructions:
https://depmap.org/portal/download/


📦 Dataset Source 

Raw data for cell lines were downloaded from [DepMap / CCLE](https://depmap.org/portal/download/). DepMap integrates CCLE cell line metadata, mutations, and drug response. This page contains versioned, CSV files used by industry and academia.

Public, reproducible, industry-standard

# Drug Response Data
Drug Response Data were downloaded from DepMap download page:

*File set "Sanger GDSC1 and GDSC2 Files"*, file name "sanger-dose-response.csv"

The Genomics of Drug Sensitivity in Cancer Project dataset (Release 8.1, Oct 2019) reprocessed to obtain dose-response parameters.
GDSC represents results from large scale viability screens across hundreds of cell lines. This data was downloaded from the Genomics of Drug Sensitivity in Cancer Project website. Starting from raw data, fold change viabilities are computed using the R package gdscIC50. Standard four-parameter monotonic log-logistic dose-response curves are then fit using R package dr4pl (Ritz et al., 2015). Recomputed dose-response parameters are available for download with harmonized cell line and drug names.

*File set "Pharmacological Profiling Files"*, file name [CCLE_NP24.2009_Drug_data_2015.02.24.csv](https://depmap.org/portal/data_page/?tab=allData&releasename=Pharmacological%20Profiling&filename=CCLE_NP24.2009_Drug_data_2015.02.24.csv)


A file contains:

Cell line identifier

Drug name

Drug response metric (AUC or IC50)

# Mutation Data
“Is gene X mutated in this cell line?”

*File set "DepMap Public 25Q3 Files"*, file name "OmicsSomaticMutations.csv"

Expanded characterizations of CCLE cancer cell lines. This includes RNA sequencing, whole-exome sequencing, whole-genome sequencing, reverse-phase protein array, reduced representation bisulfite sequencing, microRNA expression profiling, global histone modification profiling, and metabolomics.

Processed data downloads are available here. Raw sequencing data is available through the Sequence Read Archive under accession number PRJNA523380.

A file contains:

Cell line identifier (DepMap_ID)

Hugo_Symbol (gene name)

Mutation annotation

From this file we will derive:

EGFR_mut (0/1)

KRAS_mut (0/1)

# Cell Line Metadata
*File set "CCLE 2019 Files"*, file name [Cell_lines_annotations_20181226.txt](https://depmap.org/portal/data_page/?tab=allData&releasename=CCLE%202019&filename=Cell_lines_annotations_20181226.txt)

*Cell Line Annotations Files"*, file name "CCLE_sample_info_file_2012-10-18.txt"


A file that tells you:

Cancer type

Tissue

Lineage

What columns you should see

DepMap_ID

primary_disease or lineage

subtype

tissue

This is how we filter to lung cancer.

✅ Recommended Primary Dataset
Cancer Cell Line Encyclopedia (CCLE / DepMap)

Why this is ideal:

Real industry-standard dataset

Clean, well-documented

Contains drug response + mutation + basic metadata

Widely used in pharma & biotech

🧬 Cancer Type (Locked)

*Lung cancer*

Specifically:

Lung adenocarcinoma (LUAD)

Lung cancer (broader category, depending on metadata)

🧪 Drug Selection (Pick ONE)


Drug: *Erlotinib* (classic EGFR inhibitor)

*Features*:

EGFR mutation

KRAS mutation

Limited metadata features



🧠 Feature Set (Small & Interpretable)

We will intentionally limit features to ≤10 total.

Molecular Biomarkers (Binary)
Feature	Why
EGFR_mut	Known sensitivity marker
KRAS_mut	Known resistance marker
Clinical / Metadata Features
Feature	Type	Rationale
Cancer subtype	Categorical	Biological context
Tissue	Categorical	Context
Cell line lineage	Categorical	Batch proxy
Growth medium (if available)	Categorical	Technical confounder

We will drop any feature that is unclear or noisy.

🎯 Target Variable (Drug Response)
*Binary drug response target*

From drug response file:

AUC or IC50

We will:

Convert to binary response

Sensitive vs Resistant

Thresholding strategy will be:

Median split
OR

Top/bottom quantiles (e.g., top 30% sensitive)

We will justify this choice later.

📊 Expected Sample Size

After filtering:

~40–80 lung cancer cell lines

Clean, defensible dataset

This is acceptable for:

Logistic regression

5–8 features

Cross-validation


Predicting Drug Response from Gene Expression. where to get the data for this project?

README.md with
Description of the problem
Instructions on how to run the project
Data
You should either commit the dataset you used or have clear instructions how to download the dataset

1️⃣ Predicting Drug Response from Clinical + Molecular Biomarkers (TOP CHOICE)
Why this is excellent

This mirrors real precision-medicine products:

Companion diagnostics

Clinical decision support

Trial stratification

Problem

Predict whether a patient responds to a cancer drug using a small set of clinically interpretable biomarkers.

Data

Use:

Clinical drug response datasets (e.g., TCGA clinical + mutation status)

Or curated datasets from publications

Examples of features:

KRAS mutation (binary)

EGFR mutation (binary)

Tumor type (encoded)

Expression score of a pathway (1–2 features)

Age, sex

Total: ~10–20 features

ML Model

Logistic Regression

L1 or Elastic Net regularization

Why this signals expertise

You intentionally avoid “omics overload”

You model how real diagnostics work

Coefficients are interpretable for clinicians

Example framing

“This project demonstrates how logistic regression can be used to integrate clinical variables and a small number of molecular biomarkers for drug response prediction, reflecting real-world companion diagnostic design.”
