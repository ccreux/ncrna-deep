.. raw:: html

   <!--- to be converted in rst first in order to add references at the end of this document --->

.. raw:: html

   <!--- pandoc README.md -o README.rst --bibliography=../../document.bib --->

Exploring non-coding RNA functions with deep learning tools
===========================================================

Scripts and datasets to reproduce the experiments reported in the paper:
“Deep learning predicts non-coding RNA functions from only raw sequence
data”

Datasets
========

Two datasets have been adopted in the experiments: *Rfam novel*, a novel
generated dataset of sequences downloaded from Rfam database; and
*RNAGCN/nRC*, the dataset made public available by (Fiannaca et al.
2017) and adopted by the authors of RNAGCN (Rossi et al. 2019). Raw data
are available in `datasets <datasets/>`__. To generate the initial set
of fasta files the *Rfam novel* dataset needs to be prepared first with
an R script available at
`dataset-preparation.R <datasets/Rfam-novel/dataset-preparation.R>`__.
The script must be executed in the same directory as:

.. code:: console

   Rscript dataset-preparation.R

To run this script a working R environment with *Biostrings* and
*ggplot2* packages is needed. The script generates in the same directory
three fasta files, ``x_train.fasta``, ``x_val.fasta``, and
``x_test.fasta`` adopted by the subsequent scripts and the distribution
graph of sequences among Rfam classes ``class-distribution.pdf`` shown
in the paper.

Experiments
===========

Prerequisites
-------------

To run the experiments a working Python 3 environment with the following
libraries is necessary:

-  tensorflow (1.13.1)
-  sklearn (0.21.3)
-  numpy (1.16.2)
-  matplotlib (3.1.1)
-  pandas (0.25.0)

Included functions:

-  `ExpConfiguration.py <ExpConfiguration.py>`__, contains settings for
   the experiments and encoders configurations.
-  `modelUtils.py <modelUtils.py>`__, includes functions to build the
   standard and the improved CNN architectures.
-  `seqEncoders.py <seqEncoders.py>`__, a collection of functions to
   encode sequences into k-mers and spatial-curves representations.

Sequences preparation
---------------------

The Python notebook `datasets.ipynb <datasets.ipynb>`__ generates all
the data, in numpy format, necessary to run the experiments for both
*Rfam novel* and *RNAGCN/nRC* datasets. The notebook is self explained
and is able to create the necessary train, validation, and test splits
for each combination of boundary noise (0, 25, 50, 75, 100), padding
(new, random, constant), and encoder (K-mer, Snake, Morton, Hilbert).

Running the experiments
-----------------------

The Python notebooks
`experiment-Rfam-novel.ipynb <experiment-Rfam-novel.ipynb>`__,
`experiment-dataset-nRC.ipynb <experiment-dataset-nRC.ipynb>`__, and
`experiment-dropout-rejection.ipynb <experiment-dropout-rejection.ipynb>`__
provide all the necessary to execute the experiments described in the
paper respectively on *Rfam novel* and *RNAGCN/nRC* datasets. While, the
Python notebook
`experiment-dataset-nRC-ImprovedModel.ipynb <experiment-dataset-nRC-ImprovedModel.ipynb>`__
provides the necessary to run the experiments with the improved
architecture on *RNAGCN/nRC* dataset.

Results
-------

All experiment results are organized into a Python dictionary and then
stored into a file through pickle library in `results <results/>`__.
Results shown in the paper are provided in this directory for
convenience.

Tables and Figures generation
-----------------------------

The Python notebook `figures-tables.ipynb <figures-tables.ipynb>`__
provides the necessary scripts to generate figures and tables
summarizing results obtained and stored by the experiments scripts.
Supplemental figures and tables can be easly generated by changing
variable parameters at the beginning of each cell.

References
~~~~~~~~~~

.. container:: references hanging-indent
   :name: refs

   .. container::
      :name: ref-fiannaca2017nrc

      Fiannaca, Antonino, Massimo La Rosa, Laura La Paglia, Riccardo
      Rizzo, and Alfonso Urso. 2017. “NRC: Non-Coding Rna Classifier
      Based on Structural Features.” *BioData Mining* 10 (1): 27.

   .. container::
      :name: ref-DBLP:journals/corr/abs-1905-06515

      Rossi, Emanuele, Federico Monti, Michael M. Bronstein, and Pietro
      Liò. 2019. “NcRNA Classification with Graph Convolutional
      Networks.” *CoRR (to Appear in Workshop on Deep Learning on Graphs
      DLG@KDD 2019)* abs/1905.06515. http://arxiv.org/abs/1905.06515.
