# Movie Review Data Profiling and EDA — Entertainment Streaming Services

**Course:** Data Engineering — Assignment 1: Data Profiling (EDA) Report

## Team members

| Name | Matric number |
|---|---|
| LU JUNMING | A214112 |
| LIN MINGXU | A214110 |
| ZHAO YIHAN | A207334 |
| BAI XINRAN | A223106 |

## Business scenario

A movie streaming service wants to improve user retention and reduce choice paralysis through a
*Guess You Like* feature. The plan is an automated data pipeline that feeds the service's batch
movie data into pre-trained language models, analyses review text, and uses the enriched data to
recommend similar movies.

Before any of that can be trusted, the review data and the movie metadata behind it have to be
profiled: how complete, duplicated, consistent and representative are they, and what would break
a similarity model built on top of them? This assignment answers that question with a data
profiling and exploratory data analysis (EDA) report. The recommender itself, model training, and
any retention claim are out of scope.

## Data source

- **Dataset:** Movie Reviews Dataset (Cornell movie-review corpus enriched with OMDb metadata)
- **Source page:** <https://zenodo.org/records/14203180>
- **Direct download:** <https://zenodo.org/records/14203180/files/movie_reviews.csv?download=1>
- **Local file:** `data/movie_reviews.csv` (18,862 rows × 20 columns, ~94 MB, SHA-256
  `ff337b14fbd7b6d25278e81d62de71c6d6d346bf61548d918455c666eb7f6559`)
- **Licence:** CC BY 4.0, as stated on the Zenodo record

The notebook downloads the file automatically on first run. If the download fails or the file's
SHA-256 does not match the reference copy, it stops with a clear error; it never generates or
substitutes synthetic data. See `data/README.md` for provenance, integrity checks and
manual-download instructions.

## Project files

| File | Description |
|---|---|
| `Assignment1_EDA.ipynb` | The main deliverable: 17-section notebook covering the business scenario, data source, research questions, inspection, profiling, missing values, duplicates, outliers, other quality issues, diagnostic charts, PII, bias, cleaned-data summary, conclusions and run instructions. Executed end-to-end with outputs and charts embedded. |
| `README.md` | This file. |
| `requirements.txt` | Python packages needed to run the notebook. |
| `.gitignore` | Keeps the downloaded/regenerated CSV files, temporary download files and local settings out of version control. |
| `.devcontainer/devcontainer.json` | Optional Codespaces/dev-container setup: Python 3.13 image with the Python and Jupyter extensions and the requirements pre-installed. |
| `data/README.md` | Dataset provenance, licence, size, checksum, download methods and data limitations. |
| `data/movie_reviews.csv` | Raw dataset (downloaded, not committed — see `.gitignore`). |
| `data/cleaned_movie_reviews.csv` | Cleaned dataset written by the notebook (regenerable, not committed). |

## Installation

Requires Python 3.10 or newer. Tested with Python 3.13 and pandas 2.2.3 / 2.3.3,
NumPy 2.1.3 / 2.4.3 and Matplotlib 3.10.0 / 3.11.2. Also run successfully in GitHub Codespaces
(Python 3.13).

```bash
git clone https://github.com/a207334-cmyk/data-engineering-group-project.git
cd data-engineering-group-project

python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
```

The notebook itself imports only `pandas`, `numpy`, `matplotlib` and `IPython.display`. The other
packages in `requirements.txt` (`ipykernel`, `jupyterlab`, `notebook`, `nbconvert`, `nbclient`)
are the Jupyter front-end and execution stack used to run it.

## How to run

The notebook downloads `data/movie_reviews.csv` (about 94 MB) from Zenodo on its first run, checks
its size and SHA-256, and stops with an explicit error if either check fails. It finishes by
writing `data/cleaned_movie_reviews.csv`. The data is fetched automatically; it does not need to
be uploaded by hand.

### GitHub Codespaces

1. On the repository page choose **Code → Codespaces → Create codespace on main**.
2. If the Codespace was created without the included dev container, install the VS Code extensions
   **Python** and **Jupyter**, then run **Developer: Reload Window**.
3. In the terminal run `pip install -r requirements.txt` (the dev container does this
   automatically).
4. Open `Assignment1_EDA.ipynb`, choose **Select Kernel → Python Environments → Python**, then
   **Run All**.

The first run downloads the CSV, which takes a few minutes; later runs reuse the cached file.

### Google Colab

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/a207334-cmyk/data-engineering-group-project/blob/main/Assignment1_EDA.ipynb)

Colab's filesystem is temporary: when the session ends, the downloaded CSV and the cleaned output
are discarded. Nothing is lost — the next session downloads the dataset again automatically, so
there is no need to re-upload it.

### Local

1. Open a terminal in the project folder and activate the environment above.
2. Start Jupyter: `jupyter notebook`
3. Open `Assignment1_EDA.ipynb`.
4. Choose **Kernel → Restart & Run All**.

**If the automatic download fails** (blocked network, proxy, offline machine), download the CSV
manually from the direct link above, save it as `data/movie_reviews.csv`, and run the notebook
again. The notebook checks the file's size and checksum and reports an explicit error rather than
continuing with bad data.

## Important limitations

- The dataset contains **professional movie-critic reviews** from a 1990s/early-2000s Usenet
  archive, **not streaming-platform user reviews**. Treating it as a stand-in for subscriber
  behaviour is a simulation of the data-quality work a streaming service would do, not evidence
  about its users.
- The corpus is **English-only**, concentrated in 1990s releases, and over-represents popular
  films and a small number of prolific critics. A *Guess You Like* model built on it would inherit
  these biases.
- The Zenodo description states 17,165 reviews across 2,544 movies, but the distributed file
  actually contains 18,862 rows and 2,962 distinct titles. The notebook uses the file as shipped
  and reports both figures.
- Some movie metadata is wrong: 315 titles carry implausible release years (after 2001), and five
  review texts appear under more than one movie. These are flagged, not silently repaired.
- This notebook performs **data profiling, EDA and cleaning only**. It does not build a
  recommender, train or evaluate a pre-trained model, or show any effect on user retention.

## Privacy

The notebook does not print raw reviewer bylines or contact details. Reviewer names are
pseudonymised with SHA-256 and e-mail addresses, URLs, phone-like numbers and IP addresses found
in review text are redacted. No API keys, passwords or personal data are stored in this
repository.

## Data and privacy notes for this repository

The raw and cleaned CSV files are not stored here (see `.gitignore`). They are downloaded or
regenerated by the notebook, so no personal data from the dataset is committed.

## Reference

Zenodo record 14203180, *Movie Reviews Dataset*: <https://zenodo.org/records/14203180>
