![abstract](img\abstract.png)



# Conditional Molecule Generator

This repository contains the source code and data sets for the graph based molecule generator discussed in the article "Multi-Objective De Novo Drug Design with Conditional Graph Generative Model" (https://arxiv.org/abs/1801.07299). 

Briefly speaking, we used conditional graph convolution to structure the generative model. The properties of output molecules can then be controlled using the conditional code.

## Note

We have made several updates compared to the previous version:

- The model is now implemented using MXNet.
- A new graph generative model with molecule level recurrency is added to the repo. See the article for further detail.
- The pre-trained models are now available in `ckpt.tar.gz`, along with the predictive model for GSK-3b and JNK3.
- Samples generated by unconditional model are now available in `samples.tar.gz`
- All datasets are now packed in `datasets.tar.gz`
- We have provided a tutorial (`examples.ipynb`) to demonstrate the usage of our model

## Requirements:

This repo is built using Python 2.7, and utilizes the following packages:

- MXNet == 1.1.0
- RDKit == 2017.03.3
- Numpy == 1.13.3
- Scikit-learn== 0.19.1 (for the predictive model)

To ease to installation process, a docker environment will be added to the repo in future release.

## Quick start

### Project structure

- `train.py`: main training script.
- `mx_mg`: package for the molecule generative model:
  - `data`: packages for data processing workflows:
    - `conditionals.py`: callables used to generate the conditional codes for molecules
    - `data_struct.py`: defines atom types and bond types
    - `dataloaders.py` , `datasets.py` and `samplers.py`: data loading logics
    - `utils.py`: utility functions
  - `models`: library for graph generative models
    - `modules.py`: define modules (or blocks) such as graph convolution
    - `networks.py`: define networks (MolMP, MolRNN and CMolRNN)
    - `functions.py`: autograd.Function objects and operations
  - `builders.py`: utilities for building molecules using generative models
- `rdkit_contrib`: functions used to calculate QED and SAscore (for older version of rdkit)
- `example.ipynb`: tutorial

### Usage

To train the model, first unpack`datasets.tar.gz` to the current directory, and call:
```shell
./train.py {molmp|molrnn|scaffold|prop|kinase} path/to/output
```
Where `{molmp|molrnn|scaffold|prop|kinase}` are model types, and `path/to/output` is the directory where you want to save the model's checkpoint file and log files. The following call:

```shell
./train.py {molmp|molrnn|scaffold|prop|kinase} -h
```

gives help for each model type.

## Todo list

- [ ] Docker environment

## For any questions | problems | criticisms | ...

Please contact me. Email: [1210307427@pku.edu.cn](mailto:1210307427@pku.edu.cn) or [kevinid4g@gmail.com](mailto:kevinid4g@gmail.com)