# Dados IBGE

Municipal book of territory, Census population and GDP from SIDRA/IBGE, including sectoral gross value added and year-over-year transformations.

- Grain: one row per municipality. `ano` is the ABT base year, fixed at 2022. Current GDP uses reference year 2023. Sectoral value added uses reference year 2021.
- Key: `codigo_ibge` (7 digits).
- Pipeline: `01_dados_ibge.ipynb`, prepared from `01.Dados_IBGE_v1.ipynb`. Urban and rural population and territory flags are in `02_urbanizacao_territorio.ipynb`, prepared from `01.Dados_IBGE_v2.ipynb` and `01.Dados_IBGE_v3.ipynb`.
- Outputs: `data/analytics/abt_municipios_ibge_painel.parquet`, `data/analytics/abt_municipios_ibge_basica.parquet`, `data/trusted/ibge/urbanizacao_municipio_censo_2022.parquet` and `data/trusted/ibge/municipio_litoral_rm.parquet`.
- Dictionary: `dictionary.csv` (140 variables). Descriptions are in Portuguese.
- Extra local input for the territory notebook: `data/raw/ibge/Municipios_Defrontantes_com_o_Mar_2024.xlsx` or `.xls`. Metropolitan regions are downloaded from the IBGE localidades API when `data/raw/ibge/ibge_rm_cidades.json` is absent.

The notebook downloads the municipality dimension and SIDRA tables, then builds lags, growth, CAGR, logs, ranks and sector shares. Those outputs are local and are not committed.
