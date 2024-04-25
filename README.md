# Adaptyv @ Lemanic Life Sciences Hackathon 2024
Welcome to the Adaptyv Bio project at the Lemanic Life Sciences Hackathon 2024! Here you will find all the information you need to get started with our project.

## Introduction
Your goal in this project is to train classifiers that can predict protein-protein interactions for proteins binding to specific targets. We provide you with two datasets that we sourced from [CoV-AbDab](https://opig.stats.ox.ac.uk/webapps/covabdab/), a database of antibodies and nanobodies binding to different coronaviruses. We split these datasets to simulate two typical real-world scenarios. One is learning from literature, where typically there are many positive examples and few negative. The other is learning from experimental data, where there are few positive examples and many negative. The test subsets for both scenarios have several times more negative samples than positive. The antigens are SARS-CoV1 and HCoV-HKU1, respectively.
Since the source data is publicly available, we provide you with the test labels. However, you should not use these labels to train your models or tune hyperparameters. Only reserve them for the final evaluation.

## Data
The data is provided in the `data` directory. The `experiment_train.csv` and `experiment_test.csv` files contain the experimental data, while the `literature_train.csv` and `literature_test.csv` files contain the literature data. Each file contains the following columns: 
- `Binds`: `True` if the protein binds to the target, `False` otherwise,
- `Ab or Nb`: `Ab` if the protein is an antibody, `Nb` if it is a nanobody,
- `VHorVHH`: the heavy chain of the protein,
- `VL`: the light chain of the protein,
- `CDRH3`: the third complementarity-determining region of the heavy chain,
- `CDRL3`: the third complementarity-determining region of the light chain.

The heavy chain is present for all the proteins, while the other information may be missing.

You might want to use additional data to improve your models. For that, we provide a table of protein-protein interactions with other coronaviruses that do not concern the target proteins in either of the datasets. This data is in the `interactions.csv` file. It has one additional column:
- `Antigen`: the antigen the protein binds to.

In this table most antibodies and nanobodies are repeated multiple times, as they bind or do not bind to multiple antigens.

## Evaluation
Since the datasets are imbalanced, the evaluation metric for this task is F1 score. Please provide an average of five random seeds in your final solution.

## Baseline
In order to provide you with a baseline, we trained a simple random forest model with SMOTE resampling on ESM-2 embeddings of the heavy chain data. You can find the code in the [baseline notebook](baseline.ipynb).

In order to run the baseline, you will need to install some dependencies. Run this code to create a new conda environment and install them.
```bash
conda create --name lemanic_adaptyv python=3.9
conda activate lemanic_adaptyv
python -m pip install -r requirements.txt
```

## Directions
See the [intro presentation](intro.pdf) for some initial directions and references (on the last slide). Feel free to reach out to us if you have any questions or need help with the data. Good luck!
