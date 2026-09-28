# City-level information books

Municipal datasets published as books. Each book has a pipeline notebook and a variable dictionary. The join key across books is the 7-digit IBGE municipality code (`codigo_ibge`).

Source extracts and parquet outputs live under `data/`. That folder is about 15 GB, is listed in `.gitignore`, and is distributed on Google Drive.

## Books

| Book | Grain | Pipeline | Dictionary |
| --- | --- | --- | --- |
| Dados IBGE | One municipality. Base year 2022. GDP reference 2023. Sectoral value added reference 2021. Urban and rural population and territory flags are separate outputs. | `books/01_dados_ibge/01_dados_ibge.ipynb` and `books/01_dados_ibge/02_urbanizacao_territorio.ipynb` | `books/01_dados_ibge/dictionary.csv` |
| Dados IVS/IDH (Atlas/Ipea) | One municipality on the Atlas municipal total (Total Cor, Total Sexo, Total Situação de Domicílio). | `books/02_dados_ivs_idh/03_idhm_atlas.ipynb` and `books/02_dados_ivs_idh/04_ivs_atlas.ipynb` | `books/02_dados_ivs_idh/dictionary.csv` |
| RAIS 2022 | One municipality in 2022. | `books/03_rais_2022/05_rais_2022.ipynb` | `books/03_rais_2022/dictionary.csv` |
| Base final | One municipality. IBGE spine, left join of IVS/IDHM 2010 and RAIS 2022. | `books/04_base_final/06_base_final.ipynb` | Dictionaries of the three source books |
| Comparação | Shared variables between the joined ABT and `df_final_abt.parquet`. | `books/04_base_final/07_comparacao_abt.ipynb` | — |

Variable descriptions in each `dictionary.csv` are in Portuguese.

## Data

Download the `data/` folder from [Google Drive](https://drive.google.com/drive/u/0/folders/19eKt2sJ9IAC4tTJRYX8izW-JHMl3UZ7w) and place it at the repository root, next to `books/`. Notebooks walk up from the working directory until they find `data/` and `books/`, so the pipelines do not run until that folder is in place.

## How to run

Install dependencies and open a book notebook from the repository root or from its own folder. The notebook walks up from the working directory until it finds `data/` and `books/`.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Expected local inputs, included in the Drive folder:

- IBGE: municipality registry and SIDRA downloads created by the IBGE notebook under `data/raw/ibge/` and `data/trusted/ibge/`
- Urbanization and territory flags: `data/raw/ibge/Municipios_Defrontantes_com_o_Mar_2024.xlsx` or `.xls`. Metropolitan regions are downloaded when the local file is absent.
- IVS/IDH: `data/raw/idhm/br_bd_diretorios_brasil_municipio.csv.gz`, `data/raw/idhm/mundo_onu_adh_municipio.csv.gz`, `data/raw/ivs/atlasivs_dadosbrutos_pt_v2.xlsx`
- RAIS: `data/raw/rais/rais_2022.csv`

## What Git should contain

Track `books/`, this README, `requirements.txt`, `.gitignore` and `data/raw/ibge/Municipios_Defrontantes_com_o_Mar_2024.xls`. Do not add the rest of `data/`. Download that folder from the Google Drive link above.

Notebooks at the repository root (`01.Dados_IBGE_v1.ipynb`, `03.IDHM_Atlas_Intel.ipynb`, `04.IVS_Atlas_Intel.ipynb`, `05.RAIS.ipynb` and the clustering notebooks) are the local working copies. The copies under `books/` are the version prepared for Git: cell outputs removed, and paths resolved from this repository layout. The RAIS book saves `ano`, `sigla_uf_origem` and `nome_municipio_origem` together with the employment measures.
