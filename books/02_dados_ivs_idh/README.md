# Dados IVS/IDH (Atlas/Ipea)

Municipal book of the Social Vulnerability Index (IVS/Ipea) and the Municipal Human Development Index (IDHM).

- Grain: one municipality on the Atlas municipal total.
- Key: `codigo_ibge` (7 digits). `codigo_ibge_6` is kept for older auxiliary bases.
- Published filters: `label_cor_origem` = Total Cor, `label_sexo_origem` = Total Sexo, `label_sit_dom_origem` = Total Situação de Domicílio.
- Pipelines:
  - `03_idhm_atlas.ipynb` prepares IDHM from Base dos Dados.
  - `04_ivs_atlas.ipynb` standardizes the IVS/Ipea extract to municipality-year.
- Inputs:
  - `data/raw/idhm/br_bd_diretorios_brasil_municipio.csv.gz`
  - `data/raw/idhm/mundo_onu_adh_municipio.csv.gz`
  - `data/raw/ivs/atlasivs_dadosbrutos_pt_v2.xlsx`
- Outputs: `data/trusted/ibge/ivs_municipio_ano.parquet` and `data/trusted/ibge/abt_ivs_2010_var.parquet`.
- Dictionary: `dictionary.csv` (101 variables). Descriptions are in Portuguese.

`04_ivs_atlas.ipynb` also builds 2000–2010 variation columns. Those engineered columns are outside `dictionary.csv`.
