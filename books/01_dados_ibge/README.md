# Dados IBGE

Municipal book of territory, Census population and GDP from SIDRA/IBGE, including sectoral gross value added and year-over-year transformations.

- Grain: one row per municipality. `ano` is the ABT base year, fixed at 2022. Current GDP uses reference year 2023. Sectoral value added uses reference year 2021.
- Key: `codigo_ibge` (7 digits).
- Pipeline: `01_dados_ibge.ipynb`, prepared from `01.Dados_IBGE_v1.ipynb`.
- Outputs: `data/analytics/abt_municipios_ibge_painel.parquet` and `data/analytics/abt_municipios_ibge_basica.parquet`.
- Dictionary: `dictionary.csv` (127 variables). Descriptions are in Portuguese.

The notebook downloads the municipality dimension and SIDRA tables, then builds lags, growth, CAGR, logs, ranks and sector shares. Those outputs are local and are not committed.
