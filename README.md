<!-- filepath: c:\Users\nassi\OneDrive\Bureau\projet_tal\README.md -->
# Natural Language to SQL for Film Database

This project treats language as both a signal and a formal system.  
It combines regular-expression based parsing with machine-learning models to convert French and English natural language queries into SQL statements against a film dataset. Quantitative evaluations of concept extraction and value prediction are also provided.

## Repository Structure

- [.gitignore](.gitignore)  
- [README.md](README.md)  
- [projet_traitement.pdf](projet_traitement.pdf) – Project report  
- [base_films_500.csv](base_films_500.csv) – CSV database of 500 films  
- [main.ipynb](main.ipynb) – Jupyter notebook with all code  
- [queries_french_para.json](queries_french_para.json) – Corpus of French/English queries with paraphrases  
- [queries_french_para_eval.json](queries_french_para_eval.json) – Evaluation set (SQL comparisons)  
- [queries_french_para_eval_values.json](queries_french_para_eval_values.json) – Evaluation set (value extraction)

## Features

1. **Lexicon Builder**  
   Builds a lexicon from [base_films_500.csv](base_films_500.csv) to recognize film titles, directors, genres, actors, and years.

2. **Query Processing**  
   - Regular-expression based tokenization and tagging of lexicon concepts (`<titre>`, `<realisateur>`, `<genre>`, `<actor>`, `<annee>`).  
   - Extraction of concept–value pairs from both SQL and natural-language queries.

3. **Intent Classification**  
   - **SELECT** intent: Perceptron classifier with `CountVectorizer` & `TfidfVectorizer` to predict the SQL `SELECT` clause.  
   - **WHERE** intent: analogous pipeline to predict the SQL `WHERE` clause.

4. **SQL Generation & Execution**  
   - `predict_sql_query(query, SELECT_MODEL, WHERE_MODEL)` builds a parameterized SQL string.  
   - `select_from_csv(BASE_FILMS_URL, natural_query)` applies SQL-equivalent filters on the CSV via pandas.

5. **Evaluation**  
   - **Concept Extraction**: Computes Jaccard similarity, Precision, Recall, F1 against reference SQL (`compute_concepts_similarity`).  
   - **Value Prediction**: Measures accuracy on [queries_french_para_eval_values.json](queries_french_para_eval_values.json).


## Installation

```sh
python -m venv .venv
# Windows
.\.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate
pip install -r requirements.txt
```

## License

MIT License.