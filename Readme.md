# Veterinary Medicine Search

A lightweight veterinary medicine search and recommendation engine built with
TF-IDF and cosine similarity. It searches medicine metadata and indications,
corrects close spelling variations, and returns related medicines from a
precomputed similarity matrix.

## Features

- Text search across medicine names, categories, dosage forms, strengths, and indications
- Basic query correction using close string matching
- Ranked results with similarity scores
- Recommendations for medicines with similar profiles
- Notebook workflow for cleaning data and rebuilding the model artifacts

## Project Structure

```text
.
├── Data/
│   └── cleaned_veterinary_medicine.csv
├── models/
│   ├── cosine_sim.pkl
│   ├── medicine_dataset.pkl
│   ├── tfidf_matrix.pkl
│   └── tfidf_vectorizer.pkl
├── search_TF_IDF/
│   ├── Med_search.ipynb
│   └── recommender.py
├── requirements.txt
└── Readme.md
```

## Requirements

- Python 3.9 or newer
- pandas 2.2.2
- scikit-learn 1.6.1
- scipy 1.16.3

## Installation

From the repository root, create and activate a virtual environment, then
install the dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Prepare the Model Files

`recommender.py` loads its pickle files from `search_TF_IDF/models`. The
committed artifacts currently live in the repository-level `models` directory,
so copy them into the location expected by the module before searching:

```powershell
New-Item -ItemType Directory -Force search_TF_IDF\models
Copy-Item models\*.pkl search_TF_IDF\models\
```

## Usage

Run the following from the repository root:

```python
from search_TF_IDF.recommender import recommend_medicine, smart_search

results = smart_search("rabies", top_n=5)
for result in results:
		print(result)

recommendations = recommend_medicine("ketamine", top_n=5)
for recommendation in recommendations:
		print(recommendation)
```

Each search result includes the medicine name, category, dosage form,
strength, indications, and a percentage-based similarity score. Each
recommendation includes the medicine, category, and similarity score.

You can also run the module directly for a small smoke test:

```powershell
python search_TF_IDF\recommender.py
```

## Rebuilding the Artifacts

The notebook `search_TF_IDF/Med_search.ipynb` contains the exploratory data
cleaning, feature preparation, TF-IDF training, and similarity calculations.
Use it when the source data changes or the model needs to be rebuilt. The
resulting files should be placed in `search_TF_IDF/models` using these names:

```text
tfidf_vectorizer.pkl
tfidf_matrix.pkl
cosine_sim.pkl
medicine_dataset.pkl
```

The training block preserved in `search_TF_IDF/recommender.py` is commented out
to prevent accidental overwriting of the saved artifacts. Review its paths
before using it for a rebuild.

## Data

The cleaned dataset is stored in
`Data/cleaned_veterinary_medicine.csv`. The search engine expects the trained
dataset artifact to contain these columns:

- `generic_name`
- `category`
- `dosage_form`
- `strength`
- `indications`

## Notes

- This repository provides a Python search module and notebook; it does not
	include a web interface or HTTP API.
- The similarity scores indicate textual relevance, not clinical efficacy or
	treatment suitability. Consult a qualified veterinary professional before
	making treatment decisions.
