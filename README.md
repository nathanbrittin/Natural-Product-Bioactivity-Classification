# Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics
## Overview
This repository contains the data and Python scripts used in the research project titled "Machine Learning-based Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics". The project focuses on developing a machine learning (ML) framework to characterize the bioactivity of natural products by leveraging LC-MS/MS metabolomics data. This research aims to address the challenge of rediscovery in natural products drug discovery by utilizing in-silico-generated molecular fingerprints (MFPs) to classify compounds based on their core pharmacophores.

****
<!-- Insert Picture -->
<!-- ![Figure 1: Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics Workflow](/figures/Figure_2_project_workflow.png) -->
<img src="/figures/Figure_2_project_workflow.png">
****

This figure outlines the end-to-end workflow used to generate in-silico fragmentation spectra, molecular fingerprints (MFPs), and apply machine learning (ML) models for bioactivity classification of natural products.

### 1. Input Structures:

- The process begins with chemical structures of natural products obtained from public databases, specifically PubChem. 

    - For each drug class, an initial set of compounds containing the pharmacophore of the drug class were compiled from relevant literature.

    - Using the intial set of compounds, additional compounds were identified using PubChem's similarity search to expand the dataset.

        - A tanimoto score of 98% was used as the cutoff for similarity and each structure was manually inspected to ensure it contained the pharmacophore of the drug class.

- The final dataset consists of 23 drug classes with a total of 8,521 compounds across all classes.

- The negative dataset was generated by a subselection of 2,778 diverse natural products from the RIKEN NP Depository. (https://coconut.naturalproducts.net/search?type=tags&q=NPEdia&tagType=dataSource)



### 2. In-Silico MS Fragmentation:

- Structures are fragmented using Mass Frontier 8.1 to simulate LC-MS/MS fragmentation spectra.

- This step replicates the experimental breakdown of molecules to generate realistic fragmentation.

    - Mass Frontier is run with a maximum of 60 fragments being generated per compound, which is the maximum input for SIRIUS 5.

- The fragments generated from Mass Frontier are then converted to mass spectra using python.

    - The intensity of each fragment is simply a descending integer beginning at 100 for the smallest fragment and decreasing by 1 for each subsequent fragment. This does not impact the molecular fingerprint prediction done by SIRIUS 5 as shown in Supplemental Figure 1. Molecular fingerprints are generated irrespective of the intensity of the fragments, or so we have observed.

****
<!-- ![Figure 2: Spectra intensity](/figures/supp_fig_1_spectral_intensity_impact.png) -->
<img src="/figures/supp_fig_1_spectral_intensity_impact.png" width="800">
****
### 3. Molecular Fingerprint Generation:

- The fragmented spectra are processed using SIRIUS 5, which converts the spectral data into molecular fingerprints (MFPs) by generating a fragmentation tree and analyzing the pattern to predict the presence of 3,778 different substructures or properties. These fingerprints act as condensed representations of the compounds' structural features.

    - For all fingerprint sets, only the known molecular formulae were used to generate the MFPs. This is to avoid the variation in structural data that can be introduced by predicting incorrect molecular formulae.

- The generated MFPs are compiled into a dataset for training and testing machine learning models.

### 4. Training Machine Learning Models:

- The generated MFPs are used as training data for several ML classifiers (e.g., Support Vector Classifier, Logistic Regression, etc.) from the sklearn python package.

- Training data consists of both positive examples (bioactive compounds) and negative examples (non-bioactive or unrelated compounds).

    - The sets are split into training and testing data using an 80/20 split.

<!-- Figure of class distributions -->
****
<!-- ![Figure: Class Distribution](/figures/figure_class_distribution.png|width=500) -->
<img src="/figures/figure_class_distribution.png" width="500">
****

- The class distribution of the dataset is shown in Figure 2. The dataset is imbalanced, with some classes having significantly fewer examples than others. This imbalance is addressed using class weights in the ML model training.

- A variety of ML models are trained and evaluated using cross-validation to determine the best-performing model for bioactivity classification.

### 5. Testing and Evaluation:

- The trained models are evaluated on held-out test sets to ensure generalizability.

- Additional testing is conducted on experimental spectra from the GNPS repository to confirm the models' performance on real-world data.

### 6. Classification and Application:

- The trained models are applied to identify bioactive compounds, particularly in complex bacterial extracts, focusing on biologically relevant pharmacophore-based classification.

## Key Features
Machine Learning Framework: Developed to classify compounds into 23 diverse bioactive drug classes, achieving >93% accuracy on experimental spectra.
Molecular Fingerprints (MFPs): Created using SIRIUS 5 and in-silico generated fragmentation spectra to enable classification of natural products even without reference experimental spectra.
Tools Used: Utilizes computational tools such as SIRIUS, Mass Frontier, and scikit-learn for generating and analyzing metabolomics data.
Bioactivity Classification: Demonstrates the utility of pharmacophore-based classification, outperforming existing methods such as CANOPUS in identifying known bioactive compounds.

## Project Workflow
### 1. Data Generation:

- In-silico MS/MS spectra are generated using Mass Frontier for a diverse set of natural product structures.
- SIRIUS 5 is used to generate molecular fingerprints (MFPs) from the in-silico data.

### 2. Machine Learning Model:

- Multiple machine learning models are trained using scikit-learn, including Support Vector Classifiers (SVC), Ridge Classifiers, and more.
- Models are evaluated on both in-silico generated and experimental GNPS spectra to classify bioactive compounds into 23 drug classes.

### 3. Performance Metrics:

- Classification models achieve over 93% accuracy, with low false-positive rates across all drug classes.
- The models outperformed traditional classification tools, especially in predicting polyene macrolides and other antifungal drug classes.

## Zenodo Repository for all training and evaluation datasets.
https://zenodo.org/records/13921667?token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6Ijc3YjJhNDZlLTU4MTctNDYwNy04OTBlLTk2MDUwOGRlMDlmOCIsImRhdGEiOnt9LCJyYW5kb20iOiJiNjBiNGI4YjUzMTczZGY2MzVhMmEzZWQzYmEyYTI1ZSJ9.dKQYziE9NPrsFYz-QheLp4GrjW2k7e6O1_D_3H3MHD9o4JFhlO11ynL_dKhXcqM7YKVWGIh9Gp_EyDfN8y2tbg


## Installation

### Option 1: Replicate the results of the paper within this Google Colab environment.

- https://colab.research.google.com/drive/14VnBaJrp-LIpIyPne_DUE_PxeRlGYaB-?usp=sharing

- Open Collab notebook and run all cells to generate model results from the data available on the Zenodo repository.

### Option 2: Execute the code locally (Windows).

1. Prerequisites

    Before you begin, ensure you have the following installed:

    Python 3.9.13 (Other versions may cause compatibility issues.)
    pip (Python package installer)
    If you don’t have Python installed, you can download it here.

2. Installation
```
git clone https://github.com/nathanbrittin/Natural-Product-Bioactivity-Classification.git
cd Natural-Product-Bioactivity-Classification
```

3. Initiate virtual environment (Optional, but recommended for managing dependencies)
```
python3.9 -m venv venv
```

4. Activate the virtual environment
```
source venv/bin/activate
```

5. Install the required packages
```
pip install -r requirements.txt
```

6. Download the data from the Zenodo repository and place it in the same directory as the Jupyter notebook.

7. Change the file paths in the Jupyter notebook to match the location of the data files on your system.

8. Start the Jupyter notebook
```
jupyter notebook
```

9. Run the Jupyter notebook to replicate the results of the paper.

***

Dataset

The dataset used for training and testing consists of in-silico generated molecular fingerprints for 23 bioactive drug classes and GNPS spectra from real-world experimental data. These fingerprints were processed using SIRIUS 5 from Mass Frontier generated MS/MS spectra.

Citation

If you use this repository in your research, please cite:
Brittin, N., et al. (2024). Machine Learning-based Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics.

****

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
We acknowledge the support of the National Institutes of Health and the University of Wisconsin-Madison for providing the facilities to acquire the necessary mass spectrometry data. Additionally, we thank the developers of SIRIUS, and scikit-learn for their contributions to the field of metabolomics and machine learning.