# Organic Compound Classifier

## Overview

IR spectroscopy is a core analytical tool in organic chemistry, but manual interpretation is slow, expertise-dependent, and doesn't scale. This project applies machine learning to IR spectral data, generating probabilistic predictions of functional groups present in a compound.
Key contribution: A machine learning pipeline that maps IR spectral data to probabilistic functional group predictions.**Key contribution:** A machine learning pipeline that maps IR spectral data to probabilistic functional group predictions.


## Installation + Usage

The primary way to interact with the classifier is through the `main.ipynb` notebook.

### Prerequisites

Before running the notebook, ensure you have the following files in the `model/` folder:
- `mlb_classes.pkl`
- `ir_bead_classifier.pth`

Install dependencies:

```bash
pip install -r requirements.txt
```

### Running the Interface

1. Open `main.ipynb`
2. Select **Run All** to launch the interface
3. Upload a `.jdx` file when prompted
   - Sample `.jdx` files are provided in the `Sample IR Spectroscopy data files/` folder
4. The model will output the predicted probability for each bead class
   - Beads are representation of chemical group and can be used to lookup formal functional group. Further explanation in paper and video demo  

**Notes:**
- The model was trained on gas-phase compounds — the **State** field in your input file must be set to `gas`
- The `yunit` field of the `.jdx` file must be absorbance or transmittance 

---

## How the Model Was Built

### 1. Data Scraping

IR spectral data was scraped from the [NIST database](https://webbook.nist.gov/). See `extract_jdx.ipynb` for details on where to find and download jdx collection. And how the data was structured.

### 2. Preprocessing (`preprocessing.ipynb`)
* To run you will need the output of the data scrapping notebook [Here](https://drive.google.com/file/d/1Ts8AFYkM7r0E82vdLZV6eFwPr4EN8I6U/view?usp=sharing)
   * Make sure its in the correct path specified in notebook

* The preprocessing notebook takes the formated scraped data and:
  - Filters compounds to gas-phase only
  - Normalizes x-axis to wavenumber (1/cm) and y-axis to absorbance
  - Trims outlying values to a common coordinate range for interpolation


### 3. Labeling (`train_model.ipynb`)

* To run you will need the output of the data preprocessing notebook [Here](https://drive.google.com/file/d/1n_qjQ-oJRjKWIFzqqSai7nnsz9z1OqoO/view?usp=sharing)
1. Run the notebook until the `### Create Labels ` section
2. Functional group labels were assigned using the **Martini 3 mapping algorithm** (not included in this repository for confidentiality reasons)
3. The labeled dataset is available here:
[labeled_ir_data.csv](https://drive.google.com/file/d/1HECTdJJ5_ZupW1E5v0EySNKHrDnPNvt8/view?usp=sharing)
   - labels found in `bead_summary` column

### 4. Training (`train_model.ipynb`)
* Ensure you have the labeled dataset downloaded which can be found in the point above 
* Continue running `train_model.ipynb` from the labeled dataset to train the classifier. The trained model weights are saved in the `model/` folder.

### 5. Evaluation (`train_model.ipynb`)

1. Load the `.pth` file from the `models/` folder
2. Navigate to the **Evaluation** section of `train_model.ipynb`
3. Run evaluation metrics