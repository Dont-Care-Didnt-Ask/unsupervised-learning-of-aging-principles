# Unsupervised learning of aging principles from longitudinal data

Think about the report as a research paper. Only text, references and pictures demonstrating the logic of your research. All code is placed in a separate notebook.

The report should contain three sections: Introduction, Results, Discussion. Feel free to use any additional style blocks from [jupyter_book](https://jupyterbook.org/en/stable/intro.html) API for making your report more beautiful.

Use single # for project title, ## for sections and ### for subsections of your report.

## Introduction

Describe your task and its background. Imagine that your potential employer will read this report. Try to use simple language for explaining your task and hypothesis but be precise in terms.

Create a separate bibtex file (`.bib` extension) to store the references. Any bibtex reference can be obtained from google scholar by clicking on `cite` button and choosing `bibtex` option. Use the following directive to cite something inside the text of your report {cite}`bibtex_citekey`. A useful bibtex guide is here [guide](https://www.bibtex.com/g/bibtex-format/).

1.  Train AE-AR model on mouse phenome database. Explain what is dFI.
2.  Check different correlations of dFI with known aging biomarkers.

{cite}`avchaciov2022unsupervised`

## Results

This section is for presenting and describing your results. Put pictures, text, references, formulae and all that you need here. You are free to put code here also but it is quite redundant because you are also preparing the notebook with code and comments. 

Put mathematical formulae in the report if needed. Use, for example, the following directive for that

$$ y = wx + b$$

Put figures in your report. If some of the pictures were produced with python code, save them in a separate folder within the folder of your project. Use the following directive to put a figure inside the text:

```{figure} figs/hallmarks_taxonomy.png
:name: hallmarks_taxonomy
Hallmarks taxonomy.
```

Use the following directive to refer to a particular picture in the text {numref}`hallmarks_taxonomy`.

## Discussion

Discuss your results here and answer additional questions from questions/tasks section of **project proposal**. 

Project tasks/questions:


3.  What paradigm of aging do authors follow (program/quasi-program/stochastic)?

what is program

what is quai-program

what is stochastic

There are two major paradigms around ageing: the first one is seeing ageing as a consequence of developmental process, for example, some mutations can provide with some advantages early in live, but become pathological later in life [Vijg and Dong, 2020]. The second paradigm is ageing resulting from a stochastic process of damage accumulation [Seale et al., 2022]. 

Если в гугле ввести quasi-program aging, то будет статья, где написано 
Aging is not and cannot be programmed. Instead, aging is a continuation of developmental growth, driven by genetic pathways such as mTOR. Ironically, this is often misunderstood as a sort of programmed aging. In contrast, aging is a purposeless quasi-program or, figuratively, a shadow of actual programs.
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3905065/



4.  Describe some weak points of the paper (if any).

the authors use linear auto-regressor

5.  Could you suggest improvements to the approach?


6.  Why do authors call their approach unsupervised? 
They do not fit any labels


## Credits
This text prepared by

Mikhail Seleznyov
Mikhail Zybin
Nikolay Kotoyants


## References

```{bibliography}
:style: plain
:filter: docname in docnames
```

====

# Mice dFI

## AI for unsupervised learning of aging principles from longitudinal data

This repository contains the proposed model in the paper
[https://www.biorxiv.org/content/10.1101/2020.01.23.917286v1](https://www.biorxiv.org/content/10.1101/2020.01.23.917286v1).
It also contains notebooks and data to reproduce the results from the paper.


## Abstract
We proposed and characterized a novel biomarker of aging and frailty in mice trained 
from the large set of the most conventional, easily measured blood parameters such as 
Complete Blood Counts (CBC) from the open-access Mouse Phenome Database (MPD).
Instead of postulating the existence of an aging clock associated with any particular 
subsystem of an aging organism, we assumed that aging arises cooperatively from positive
feedback loops spanning across physiological compartments and leading to an organism-level
instability of the underlying regulatory network. To analyze the data, we employed a 
deep artificial neural network including auto-encoder (AE) and auto-regression (AR) 
components. The AE was used for dimensionality reduction and denoising the data.
The AR was used to describe the dynamics of an individual mouse’s health state by means
of stochastic evolution of a single organism state variable, the “dynamic frailty index”
(dFI), that is the linear combination of the latent AE features and has the meaning of 
the total number of regulatory abnormalities developed up to the point of the measurement
or, more formally, the order parameter associated with the instability. 
We used neither the chronological age nor the remaining lifespan of the animals while 
training the model. Nevertheless, dFI fully described aging on the organism level, 
that is it increased exponentially with age and predicted remaining lifespan. 
Notably, dFI correlated strongly with multiple hallmarks of aging such as physiological 
frailty index, indications of physical decline, molecular markers of inflammation and
accumulation of senescent cells. The dynamic nature of dFI was demonstrated in mice 
subjected to aging acceleration by placement on a high-fat diet and aging deceleration 
by treatment with rapamycin.

## Requirements
1. Python >= 3.8, pip => 20.0
2. Required python packages are listed in [setup.py](setup.py). Will be installed automatically.
3. To run jupyter notebooks, you should be able to connect to a running [jupyter server](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)


## Installation
Use `pip` install to install a package. 
```bash
git clone https://github.com/gero-science/mice_dfi
cd mice_dfi
pip install .
```

## Obtaining MPD datasets
This study is mostly based on data from the [Mouse Phenome Database](https://phenome.jax.org/). 
To download the dataset used for training a model simply run the following command.
```bash
python -m mice_dfi.dataset.download
```
The other datasets used in this study are stored in [this repository](notebooks/generated).

## Training model

Start a model training with the command. Note, that datasets should be downloaded in prior
```bash
python -m mice_dfi.model.train -o dump -c ./src/mice_dfi/model/config/model_resnet.yaml --tb
```
or display command-line argument help.
```bash
python -m mice_dfi.model.train --help
```
File `model_resnet.yaml` could be modified for tuning neural network parameters, 
such as depth, activation and dropouts. 

## Notebooks

Notebooks are stored in the [notebooks](notebooks/) folder. Note, you have to install and run jupyter
server by yourself. 

## TODOs
 - Write missing documentation
 - Add learning rate scheduler and loss weights scheduler 

## License
The `mice_dfi` package is licensed under the [GNU GENERAL PUBLIC LICENSE Version 3 (GPLv3)](LICENSE)

