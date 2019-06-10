# FOLD
This is the First Implementation of FOLD (First Order Learner of Default) algorithm. FOLD is an ILP algorithm that learns a hypothesis from a background knowledge represented as normal logic program, with two disjoint sets of Positive and Negative examples. Learning hypotheses in terms of default theories (i.e., default and exceptions) outperforms Horn based ILP algorithms in terms of classification evaluation measures. It also significantly decreases the number of induced clauses. For more information about the original FOLD algorithm and learning default theories kindly refer to the [FOLD paper](https://arxiv.org/pdf/1707.02693.pdf "FOLD paper").

### SHAP_FOLD
This algorothm replaces the heuristic based search for best clause in ILP, with a technique from datamining known as High-Utility Itemset Mining. The idea is to use [SHAP](https://github.com/slundberg/shap "SHAP") to generate relevant features for each training data. Then our FOLD algorithm learns a set of Non-Monotonic clauses, that would capture the underlying logic of the Statistical Model from which SHAP features were extracted. For more details refer to our [arXiv paper](https://arxiv.org/pdf/1905.11226.pdf). 

## Install 
### Prerequisites
We only support Windows at the moment.
* SHAP <pre> pip install shap </pre>
* XGBoost <pre> pip3 install xgboost </pre>
* [SWI-Prolog](http://www.swi-prolog.org/)  x64-win64, version 7.4.0-rc2
* [JPL Library](https://github.com/SWI-Prolog/packages-jpl) and [here](https://jpl7.org/DeploymentWindows.html) for JPL installation troubleshooting
### Compile Sources (Create Jar file)
1. Download src folder and its contents
2. Change directory to the "src" and compile the sources using the following command:
<pre> javac -cp jpl.jar *.java </pre>
3. Create the Jar file using the following command:
<pre> jar -cmvf META-INF/MANIFEST.MF fold.jar * </pre>
4. Upon Successful execution the fold.jar file will be created.

## Instructions
1. Data preparation
    + Create a dataset as ".csv" file.
    + Add a header row so that each column has a name. The class column should be named "label". Order is not important
    + Add a new column named "id" and use MS Excel to assign a unique integer to each data row.
2. Training a Statistical Model
    + Modify the "training.py" according the provided examples to work with your dataset.
    + Remember the dataset_name variable. It will be used later to run FOLD algorithm.
    + Run the Python sccript as follows:<pre> python training.py </pre>.
    + Upon sucessful execution it will produce 6 files including 2 Prolog files with ".pl" extension. Make sure that all files are put in the same folder that the jar file "UFOLD.java" is located.  
3. Run the FOLD algorithm as follows: <pre> java -jar fold.jar -mode shapfold <dataset_name> </pre>
4. Upon successful execution, the file "hypothesis.txt" will be created. It contains a logic program that would explain the underlying logic of the statistical model trained using "training.py" script.
