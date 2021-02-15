<divalign = "center"><h1> Interaction Prediction between Molecules and Metabolic Pathways with ANNs</h1></div>
<hr />
#<h3>Overview</h3>
In this project, the interaction of a set of molecules with specifications
Metabolic pathways is predicted using two types of Artificial Neural
Networks (ANNs): Convolutional Neural Network 1-Dimensional or
Long Short Term Memory Units, which receive processing as inputof the SMILES 
notation that identifies each molecule. Such no-tation is made unique for each molecule 
and detects  structural and physico-chemical information. Convolutional filters, as well as units LSTM, are able to recognize textual patterns, which in turn
they represent precise substructures responsible for the interactions between
molecules of the dataset and reagents in the target metabolic pathways.
<p></p>
This work was inspired by <a href ="https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2523-5"> this paper </a>, while the data used are available <a href="https://tripod.nih.gov/tox21/challenge/data.jsp">here</a>.
<p></p>
All the notebooks are has been ran on Colab.

<h3>1) Metabolic pathways</h3>

In the work presented here, the interference between molecules of interest was analyzed
toxicological and metabolic pathways of two types: Nuclear Receptor (NR) signaling,
Stress Response (SR) pathways. In the first case we are dealing with proteins, that is
macromolecules consisting of chains of amino acids (20 specific molecules),located in the cell, capable of recognizing the presence of specific hormones and
consequently improve cellular activity and development. In the second case, it deals with a wide variety of adaptive responses of the cell to maintain the own physiological state despite external stresses (mechanical, physical, chemical,
environmental, et alia). In both, the interaction between molecules, when known,
it can be traced back to the quality, quantity and organization of the chemical elements in the molecular structures of the cell and of the reagents; yet not this inter-
action is not directly and universally predictable.

<h3>2) Datasets - Tox21 10k</h3>
Tox21 is an initiative of the US government, aimed at developing the drug
cologia in the 21st century, thanks to both experimental and new technologies
analytical. Human beings are exposed to enormous amounts and varieties of
chemical agents of little known toxicity, simultaneously about 30% of
Promising experimental drugs in animal tests prove toxic to the human being. This highlights the need to analyze quickly and effectively
ciently large amounts of data different in origin and format (exactly the 3 V of Big Data, Velocity, Variety, Volume). In 2014 it was therefore launched
created a Tox21 Data Challenge, a set of sub-problems whose objective generic was to predict exactly the outcome of 12 tests for about 10 000 molecules, 6 NR type assays and 6 SR type assays, the outcome of which may be would end if each molecule interfered with the 12 metabolic pathways or not.
<p></p>
The 12 original datasets, divided into train, validation and score set, differ
as the same molecule may or may not be independently active on different ways, and why not all assays for molecule-metabolic pair ica give unique or clear results. They are made publicly available in SMILES format <a href="https://tripod.nih.gov/tox21/challenge/data.jsp">here</a>.

<h3>3) From SMILES strings to ANNs Input</h3>

Following the approach and algorithm presented in <a href ="https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-018-2523-5">(Maya et al. 2018)</a>, the SMILES strings were transformed into 42-column Feature Matrices. 21 Columns needed for one-hot-encoding of SMILES native symbols, althree 21 columns to collect features of the atoms, such as the type of element (categories H, C, O, N, or Other), the charge and the electronic valence, the number
of bonds with Hydrogen atoms, the chirality (right, left, or other), the saturation and hybridization of orbitals. Being the longest molecule of the dataset identified by 400 SMILES characters, each matrix has been to zero-padding to equalize the dimensions. The Feature Matrices constructed in this way have been used as inputs of the 1-Dimensiona Convolutional Neural Networks (1-D CNNs), while for Long Short Term Memory units (LSTMs) we preferred to avoid approaching the problem as multivaried (42 possibly unrelated features), reducing the matrices to one-hot-SMILES string encodings: in particular, columns have been removed with the additional atomic characteristics in addition to the element type, each row has been replaced with a "flag" of its index with element
non-null in order to learn effective embedding at the same time
to LSTM training.

<h3>4) Methodology</h3>
Two different methodologies were followed for the two methaboloc pathways, SR and NR, in oder to assess the effectiveness of both CNN and LSTM models and Bayesian optimized models. 
<h4>SR</h4>
Several CNN and LSTMS models were used, in order to find a benchmark model for each of the approaches, finally applying them on the test data. Here, unbalanced data are managed by testing the effect on results of both oversampling and weighted classes techniques are applied.
<h4>NR</h4>
Here, only CNN models are applied, after undergoing a Bayesian Optimizations oftthe hyperparameters. First, a reduction of the search-space was was carried out, by trying different architectures evaluated on a 3-fold cross validation. Following, the resulting best architecture was optimized using bayesian Optimization. Here, unbalanced data were managed assessing the effectiveness of oversampling, weighted classes and SMOTE techqniques.
