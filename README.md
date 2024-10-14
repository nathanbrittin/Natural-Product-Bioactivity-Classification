# Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics
## Overview
This repository contains the data and Python scripts used in the research project titled "Machine Learning-based Bioactivity Classification of Natural Products Using LC-MS/MS Metabolomics". The project focuses on developing a machine learning (ML) framework to characterize the bioactivity of natural products by leveraging LC-MS/MS metabolomics data. This research aims to address the challenge of rediscovery in natural products drug discovery by utilizing in-silico-generated molecular fingerprints (MFPs) to classify compounds based on their core pharmacophores.

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
### https://zenodo.org/records/13921667?token=eyJhbGciOiJIUzUxMiJ9.eyJpZCI6Ijc3YjJhNDZlLTU4MTctNDYwNy04OTBlLTk2MDUwOGRlMDlmOCIsImRhdGEiOnt9LCJyYW5kb20iOiJiNjBiNGI4YjUzMTczZGY2MzVhMmEzZWQzYmEyYTI1ZSJ9.dKQYziE9NPrsFYz-QheLp4GrjW2k7e6O1_D_3H3MHD9o4JFhlO11ynL_dKhXcqM7YKVWGIh9Gp_EyDfN8y2tbg

Installation

### 1. Download

****

Usage
To train and test the models, run the following command:

****

Dataset
The dataset used for training and testing consists of in-silico generated molecular fingerprints for 23 bioactive drug classes and GNPS spectra from real-world experimental data. These fingerprints were processed using SIRIUS 5 from Mass Frontier generated MS/MS spectra.

Citation
If you use this repository in your research, please cite:

****

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
We acknowledge the support of the National Institutes of Health and the University of Wisconsin-Madison for providing the facilities to acquire the necessary mass spectrometry data.