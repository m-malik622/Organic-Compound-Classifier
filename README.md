# Organic-Compound-Classifier

# Usage
* User interface for interactign with model in `main.ipynb`
  * need to have model file `mlb_classes.pkl` and the `ir_bead_classifier.pth` in model folder 
  * run `pip install -r requirements.txt`
  * select run all in notebook
  * upload jdx file and result of probability of model is produced
    * sample files located in `Sample IR spectroscpoy data files` folder
    * model for gas compounds so state field must be gas 

# How model was built
## Data scrapping
* data scrapped from NIST database from the following repo
  * more details on where scrapped data in extract_jdx notebook
 
## Model preprocessing
1. preprocessing.ipynb file handled 
   * can run using the ir spectra data scrapped from extrac_jdx notebook 
     * https://drive.google.com/file/d/1Ts8AFYkM7r0E82vdLZV6eFwPr4EN8I6U/view?usp=sharing
   * filtering to gas only
   * normalizing x and y to be 1/cm and absorbtion
   * trimming outlying values to maintain a common coordinate for interpolation 

* in train_model.ipynb
2. Load Preproccessed CSV from preprocessing notebook
   1. https://drive.google.com/file/d/1n_qjQ-oJRjKWIFzqqSai7nnsz9z1OqoO/view?usp=sharing 
3. run train_model notebook until you reach labelling 
   * from here Labelling was done using martini 3 mapping algorithm not provided in this notebook for confedentiality reasons. You can find the resulting data with the labeled beads in the following csv  
   1. https://drive.google.com/file/d/1HECTdJJ5_ZupW1E5v0EySNKHrDnPNvt8/view?usp=sharing
4. train model from lableeld dataset 
## Model evaluation

1. load pth file in models folder
2. head to train_model.ipynb notebook and go to section Evaluation where you can load model and run evaluations. 
   1. tune temperature for temp scaling as needed
