# Data folder

## `movie_reviews.csv` (raw, downloaded)

| Property | Value |
|---|---|
| Dataset name | Movie Reviews Dataset |
| Source page | <https://zenodo.org/records/14203180> |
| Direct file URL | <https://zenodo.org/records/14203180/files/movie_reviews.csv?download=1> |
| Licence | CC BY 4.0 (as stated on the Zenodo record) |
| Size | 93,715,558 bytes (~94 MB) |
| SHA-256 | `ff337b14fbd7b6d25278e81d62de71c6d6d346bf61548d918455c666eb7f6559` |
| Rows × columns | 18,862 × 20 |
| Encoding | UTF-8 |

### What it contains

Professional movie reviews from the Cornell movie-review collection (rec.arts.movies.reviews
Usenet archive), enriched with movie metadata from the OMDb API. Each row is one review joined to
its movie's metadata: title, release year, MPAA-style rating, genre, directors, writers, actors,
plot, plus the first-listed genre/actor/director/writer and the recorded gender of those three
first-listed people.

Key columns: `review_id`, `movie_name`, `year`, `reviewer_name`, `review_text`, `rated`,
`year_api`, `genre`, `directors`, `writers`, `actors`, `plot`, `first_genre`, `first_actor`,
`first_director`, `first_writer`, `first_actor_gender`, `first_director_gender`,
`first_writer_gender`, and an unnamed row-index column.

### How the file is obtained

The notebook downloads it automatically on first run:

1. It tries parallel HTTP Range requests (8 workers), falling back to a single streaming
   download if the server or network does not support ranges.
2. Partial downloads go to `data/.download_parts/` and are only moved into place once complete.
3. The file is checked for minimum size and SHA-256 before pandas reads it.
4. If the download fails, the notebook raises a clear `RuntimeError` and stops. **No synthetic
   data is ever generated.**

**Manual download** (offline or blocked network):

```bash
# from the project root
curl -L -o data/movie_reviews.csv "https://zenodo.org/records/14203180/files/movie_reviews.csv?download=1"
```

or open the direct link in a browser and save the file as `data/movie_reviews.csv`.

### Known documentation mismatch

The Zenodo record describes the dataset as 17,165 reviews of 2,544 movies. The file actually
contains 18,862 rows and 2,962 distinct titles. The notebook uses the file as distributed and
reports the observed counts rather than the description.

## `cleaned_movie_reviews.csv` (generated)

Written by `Assignment1_EDA.ipynb` at the end of the cleaning section: 18,719 rows × 33 columns.
It adds cleaned text, flags and pseudonymised identifiers, and drops the raw `reviewer_name` and
`review_text` columns. This file is regenerable and is excluded from version control.

## Privacy

The raw file contains reviewer bylines and, in many reviews, the reviewer's e-mail address and
website. Do not publish the raw CSV or paste raw review text into public issues. The notebook
pseudonymises bylines and redacts contact details before any display.

## Version control

Both CSV files are listed in the project `.gitignore`. Re-download or re-run the notebook instead
of committing them.
