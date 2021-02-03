# HTE-MA-Project
this is used for the publication of stability reversal paper
This documentation is prepared as the workflow to accompany the following study:

"How machine learning can help select capping layers to suppress perovskite degradation"

Noor Titan Putri Hartono (1), Janak Thapa (1), Armi Tiihonen (1), Felipe Oviedo (1), Clio Batali (1), Jason J. Yoo (1), Zhe Liu (1), Ruipeng Li (2), David Fuertes Marrón (1,3), Moungi G. Bawendi(1), Tonio Buonassisi (1), Shijing Sun (1)

Affiliations:

Massachusetts Institute of Technology, 77 Massachusetts Avenue, Cambridge, MA 02139
National Synchrotron Light Source II, Brookhaven National Laboratory, Upton, NY 11973
Instituto de Energía Solar-ETSIT, Universidad Politécnica de Madrid, 28040, Madrid, Spain
Installation
To run the Jupyter Notebook, please install the following:

Anaconda (https://www.anaconda.com/distribution/), which already consists of Jupyter Notebook, NumPy, pandas, seaborn, matplotlib, SciPy, scikit-learn.
Jupyter Notebook (https://jupyter.org/install.html)
There are several packages and/or libraries that need to be installed to run the notebook:

Pandas (https://pandas.pydata.org/pandas-docs/stable/getting_started/install.html)
NumPy (https://docs.scipy.org/doc/numpy/user/install.html)
Seaborn (https://seaborn.pydata.org/installing.html)
Matplotlib (https://matplotlib.org/users/installing.html)
SciPy (https://www.scipy.org/install.html)
Scikit-learn (https://scikit-learn.org/stable/install.html)
SHAP (https://github.com/slundberg/shap)
OR clone the following repository: pip install -r requirements.txt

Datasets
There are several datasets we need:

The ML input (X), which consists of the processing conditions and the molecular properties from the PubChem 2019 database (Kim, S. et al. PubChem 2019 update: improved access to chemical data. Nucleic Acids Res. 47, D1102–D1109 (2019)). One dataset includes phenyltriethylammonium iodide (PTEAI), while another one excludes PTEAI. PTEAI is the most stable capping layer in our study.
The ML output (y), which consists of the degradation parameters: red degradation onset, along with red degradation slope, green degradation onset, and greeen degradation slope. For this study, we focus on red degradation onset, but it is possible to try the other parameters, such as slope. As the films degrade, the color changes from black perovskite phase to yellow lead (II) iodide phase, therefore, the red and green (RG) values from the RGB values of the images increase. The degradation parameters are hence extracted by going through each sample, and fitting a line that goes through the most significant change of the RG values. The ML output dataset consists of the parameters from this line fitting.
The molecule prediction dataset, which consists of the PubChem 2019 database values for the molecules that we would like to predict, using the trained ML models. To add more capping layer materials to predict, you can add the PubChem 2019 values of the composition to the .csv file.
ML algorithms
There are 6 ML algorithms trained, which are available on scikit-learn:

Linear regression
K-nearest neighbors regression
Random forest regression
Gradient boosting with decision trees regression
Support vector machine regression
Multi-layer perceptron regression (MLP, neural network/ NN)
We evaluate the algorithms using a 5-fold cross-validation RMSE.

Workflow
There are 3 Jupyter notebook files: the normalized input (SHAP_std.ipynb), the non-normalized input (SHAP_nonstd.ipynb), and the non-normalized input and excluding PTEAI (SHAP_nonstd_excPTEAI.ipynb). The workflow is the following:

We start by loading the data, both the input (X) and the output (y).
We split the train and test data in 80% : 20% ratio (using scikit-learn).
For the normalized input, we pre-process the data (using scikit-learn).
We use GridSearchCV to find the optimum parameters for each algorithm, and train the model based on that (using scikit-learn).
We compare the cross-validated RMSE of various models.
We run SHAP for trained model, to look at how the processing conditions and the molecular properties contribute to the result. We can also look at the most important contributors, which govern the stability result.
After the models are trained, we can load the dataset that consists of the input (X) for the molecules we want to predict. Then, we can predict what the degradation onset for these molecules be.
Authors
The ML workflow for capping layer study ver 4, 2020/04/09

Titan Hartono (MIT), with the help from Felipe Oviedo (MIT), Armi Tiihonen (MIT), Siyu Isaac P. Tian (SMART), Zekun Danny Ren (SMART)
