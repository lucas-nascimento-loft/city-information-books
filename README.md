# Livros de informação municipal

Bases municipais publicadas como livros. Cada livro tem um notebook de pipeline e um dicionário de variáveis. A chave de junção entre os livros é o código IBGE do município com 7 dígitos (`codigo_ibge`).

Os extratos de origem e os parquets gerados ficam em `data/`. Essa pasta tem cerca de 15 GB, está no `.gitignore` e é distribuída pelo Google Drive.

## Livros

| Livro | Granularidade | Pipeline | Dicionário |
| --- | --- | --- | --- |
| Dados IBGE | Um município. Ano-base 2022. PIB de referência 2023. Valor adicionado setorial de referência 2021. População urbana e rural e indicadores de território são saídas separadas. | `books/01_dados_ibge/01_dados_ibge.ipynb` e `books/01_dados_ibge/02_urbanizacao_territorio.ipynb` | `books/01_dados_ibge/dictionary.csv` |
| Dados IVS/IDH (Atlas/Ipea) | Um município no total municipal do Atlas (Total Cor, Total Sexo, Total Situação de Domicílio). | `books/02_dados_ivs_idh/03_idhm_atlas.ipynb` e `books/02_dados_ivs_idh/04_ivs_atlas.ipynb` | `books/02_dados_ivs_idh/dictionary.csv` |
| RAIS 2022 | Um município em 2022. | `books/03_rais_2022/05_rais_2022.ipynb` | `books/03_rais_2022/dictionary.csv` |
| Base final | Um município. Espinha IBGE, com left join do IVS/IDHM 2010 e da RAIS 2022. | `books/04_base_final/06_base_final.ipynb` | Dicionários dos três livros de origem |
| Comparação | Variáveis em comum entre a ABT juntada e `df_final_abt.parquet`. | `books/04_base_final/07_comparacao_abt.ipynb` | — |

As descrições das variáveis em cada `dictionary.csv` estão em português.

## Dados

Baixe a pasta `data/` no [Google Drive](https://drive.google.com/drive/u/0/folders/19eKt2sJ9IAC4tTJRYX8izW-JHMl3UZ7w) e coloque-a na raiz do repositório, ao lado de `books/`. Os notebooks sobem a partir do diretório de trabalho até encontrar `data/` e `books/`, então os pipelines só rodam com essa pasta no lugar.

## Como executar

Instale as dependências e abra o notebook de um livro a partir da raiz do repositório ou da pasta do próprio livro. O notebook sobe a partir do diretório de trabalho até encontrar `data/` e `books/`.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Insumos locais esperados, incluídos na pasta do Drive:

- IBGE: cadastro de municípios e downloads do SIDRA gerados pelo notebook do IBGE em `data/raw/ibge/` e `data/trusted/ibge/`
- Urbanização e indicadores de território: `data/raw/ibge/Municipios_Defrontantes_com_o_Mar_2024.xlsx` ou `.xls`. As regiões metropolitanas são baixadas quando o arquivo local não existe.
- IVS/IDH: `data/raw/idhm/br_bd_diretorios_brasil_municipio.csv.gz`, `data/raw/idhm/mundo_onu_adh_municipio.csv.gz`, `data/raw/ivs/atlasivs_dadosbrutos_pt_v2.xlsx`
- RAIS: `data/raw/rais/rais_2022.csv`

## O que o Git deve conter

Versione `books/`, este README, `requirements.txt`, `.gitignore` e `data/raw/ibge/Municipios_Defrontantes_com_o_Mar_2024.xls`. O restante de `data/` fica de fora. Baixe essa pasta pelo link do Google Drive acima.

Os notebooks na raiz do repositório (`01.Dados_IBGE_v1.ipynb`, `03.IDHM_Atlas_Intel.ipynb`, `04.IVS_Atlas_Intel.ipynb`, `05.RAIS.ipynb` e os notebooks de clusterização) são as cópias locais de trabalho. As cópias em `books/` são a versão preparada para o Git: saídas das células removidas e caminhos resolvidos a partir deste layout. O livro da RAIS grava `ano`, `sigla_uf_origem` e `nome_municipio_origem` junto com as medidas de emprego.
