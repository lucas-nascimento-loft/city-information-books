# RAIS 2022

Municipal book of formal employment from RAIS for reference year 2022.

- Grain: one row per municipality in 2022.
- Key: `codigo_ibge` (7 digits).
- Pipeline: `05_rais_2022.ipynb`, prepared from `05.RAIS.ipynb`.
- Input: `data/raw/rais/rais_2022.csv`.
- Output: `data/trusted/ibge/rais_2022_municipio.parquet`.
- Dictionary: `dictionary.csv` (14 variables). Descriptions are in Portuguese.

The saved table keeps `ano`, `sigla_uf_origem` and `nome_municipio_origem` with the employment counts, average pay and sector shares. Sector shares use active jobs on 31 December as the denominator.
