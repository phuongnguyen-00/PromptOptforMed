# From Unstructured Clinical Notes to Structured Prompts

Source code and saved prototype representations for the MSc Data Science
and Artificial Intelligence dissertation:

**From Unstructured Clinical Notes to Structured Prompts: A
Patient-Specific Framework for Few-Shot Chest X-ray Classification**

## Overview

This project investigates how clinical text representation affects
vision-language model performance for chest X-ray classification. The
experimental pipeline uses BiomedCLIP with ontology-guided clinical text
processing and few-shot prototype learning.

The project includes OpenI preprocessing and four-class label
construction, a task-specific radiology ontology, a supervised ResNet50
image-only baseline, zero-shot and few-shot prompt experiments,
patient-specific structured prompts, fixed and learnable multimodal
prototypes, ablation experiments, t-SNE visualisation, and external
evaluation on PadChest-GR.

## Repository Structure

``` text
.
├── Hoang_Phuong_Nguyen_Final_Dissertation_Experiment.ipynb
├── README.md
└── prototypes/
    ├── proto_unstruct_20.pt
    ├── proto_struct_20.pt
    └── proto_learnable_20.pt
```

The `.pt` files are saved 20-shot OpenI prototypes used in the external
evaluation stage.

## Datasets

The datasets are **not included in this repository**. They must be
obtained from their original providers and used according to the
applicable access and research-use conditions.

### 1. OpenI / Indiana University Chest X-ray Collection

Official OpenI information and download instructions:

https://openi.nlm.nih.gov/faq

The notebook expects these OpenI resources in the configured project
directory:

``` text
openi_reports.csv
NLMCXR_png.tgz
radiology_vocabulary_final.xlsx
```

`openi_reports.csv` is the report table used by the notebook and
contains the report identifier, Findings, Impression, full note, and
MeSH tags. The OpenI FAQ provides the original reports, images, and
terminology-mapping resources. If starting from the original OpenI
report files, prepare the report table in the format expected by the
notebook before running the experiments.

OpenI asks researchers not to redistribute the dataset outside their
research group or organisation. Therefore, no OpenI images or reports
are included here.

### 2. PadChest-GR

Official PadChest-GR dataset page:

https://bimcv.cipf.es/bimcv-projects/padchest-gr/

PadChest-GR is used for external cross-dataset evaluation. The notebook
currently downloads the 1,000-study working subset through `kagglehub`;
the link above is the **original PadChest-GR source** and should be
consulted for dataset access and its Research Use Agreement.

PadChest-GR is not redistributed in this repository.

## Environment

The experiments were developed and run in Google Colab with GPU
acceleration.

Main dependencies include:

``` text
torch
torchvision
open_clip_torch
transformers
hf_transfer
scikit-learn
pandas
numpy
Pillow
matplotlib
seaborn
openpyxl
kagglehub
```

A CUDA-capable GPU is recommended for the BiomedCLIP and prototype
experiments.

## Running the Notebook

1.  Obtain the required OpenI resources from the official source.
2.  Place the OpenI files in a project directory.
3.  Update `BASE_DIR` near the beginning of the notebook if necessary.
4.  Open the notebook in Google Colab.
5.  Select a GPU runtime.
6.  Run the notebook from top to bottom.
7.  The PadChest-GR section performs external evaluation after the OpenI
    experiments and prototype construction.

The original project configuration uses:

``` python
BASE_DIR = "/content/drive/MyDrive/dissertation"
```

Change this path when reproducing the project elsewhere.

## Saved Prototypes

The repository contains:

-   `proto_unstruct_20.pt` - 20-shot prototype for the unstructured
    clinical-text condition
-   `proto_struct_20.pt` - 20-shot fixed prototype using
    patient-specific structured findings
-   `proto_learnable_20.pt` - optimised 20-shot learnable prototype

The prototypes correspond to the four OpenI classes used in the
dissertation:

``` text
Cardiovascular
Musculoskeletal
No Finding
Respiratory
```

They are model-derived representations and do not contain the original
medical images or radiology reports.

## Reproducibility Notes

The notebook uses a fixed random seed (`seed = 42`) for data splitting
and support sampling. The main patient-specific multimodal configuration
uses image/text fusion weights of 0.4/0.6.

Dataset paths and access requirements may need to be updated before
execution. Because the source datasets are not redistributed,
reproduction requires obtaining the corresponding data from the original
providers.

## Intended Use

This repository accompanies an MSc dissertation and is provided for
academic research and evaluation. The framework and outputs are **not
intended for clinical diagnosis or patient care**.
