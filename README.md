

# Chemical Effect Prediction Using Chemical Fingerprints.
This repository aims at predicting chemical effects using the T.E.S.T dataset ([U.S. EPA](https://www.epa.gov/chemical-research/toxicity-estimation-software-tool-test)).

## Problem
Each dataset contains training and testing data. Where each sample is a CAS number and a chemical concentration. 

### Methods
We use three models:
1. Simiarity model. Prediction is the average of the k closest (most similar) chemicals in the training set. Hyperparameters: k
2. FDA model. The training data is clustered into k clusters. During prediction a model is fitted to the cluster, which is used for prediction. Hyperparameters: k, clustering model, prediction model, model parameters. 
3. Ensemble model ([auto-sklearn](https://automl.github.io/auto-sklearn/master/)). This library finds the optimal ensemble model for the given problem. Hyperparameters: optimization time (total and per model). 

We report R2 scores. See table at bottom for a excerpt of full results. 

## Usage 
```
usage: fingerprint_learning.py [-h] [-d DATASETS [DATASETS ...]] [-c CONFIG]
                               [--cv] [--fp] [--sd] [--p]

Chemical Effect Prediction Using Chemical Fingerprints.

optional arguments:
  -h, --help            show this help message and exit
  -d DATASETS [DATASETS ...], --datasets DATASETS [DATASETS ...]
                        Datasets (if empty: all datasets)
  -c CONFIG, --config CONFIG
                        Config file. See LC50_config.txt for example
  --cv                  Run Cross Validation
  --fp                  Fetch fingerprints from PubChem, and save to txt for
                        faster execution later.
  --sd                  Scale labels.
  --p                   Predict mode, will output file dataset_prediction.txt.
                        Provide test file with fingerprints/CIDs and labels
                        (these are ignored).
```

See data folder for dataset options. See config folder for example configurations. A new optimal configuration will be created from the cross validation process. The labels for regression can be scaled between 0 and 1, this can be favourable for certain model. 
During prediction, the program will gather training and test data in the way as before, but test labels will be ignored. 
If the training and testing files has columns (CID,label), then use the '--fp' flag to gather fingerprints from the PubChem API.


## Results
The table below show the results for each dataset.

