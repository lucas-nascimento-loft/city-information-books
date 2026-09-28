# Municipal ABT

One row per municipality, joining the tables written by the IBGE, IVS/IDHM and RAIS books.

- Key: `codigo_ibge` (7 digits).
- Spine: `data/analytics/abt_municipios_ibge_basica.parquet` (falls back to `abt_municipios_ibge_painel.parquet`).
- IVS/IDHM: `data/trusted/ibge/abt_ivs_2010_var.parquet`, plus 2010 indicators from `data/trusted/ibge/ivs_municipio_ano.parquet` that are not already in the variation table.
- Urbanization: `data/trusted/ibge/urbanizacao_municipio_censo_2022.parquet`, dropping `municipio_sidra` and `populacao_total_censo_2022`.
- Territory flags: `data/trusted/ibge/municipio_litoral_rm.parquet`.
- RAIS: `data/trusted/ibge/rais_2022_municipio.parquet`.
- Output: `data/analytics/abt_municipios_final.parquet`.
- Pipelines:
  - `06_base_final.ipynb` builds the join.
  - `07_comparacao_abt.ipynb` compares shared variables with `df_final_abt.parquet` at the repository root.

`ano` is kept from the IBGE book (base year 2022). IVS/IDHM measures are 2010 levels and 2000–2010 variations. RAIS measures are for 2022. Level and absolute-change columns of GDP, sectoral value added, net taxes and approximate GDP per capita are stored with `log1p`. The output stays on disk under `data/` and is not committed.
