# 📊 Datos

## Estructura
data/
├── raw/                                      # Datos originales sin procesar
│   └── oecd_city_economy.csv                 # Datos económicos urbanos (OECD)
├── processed/                                # Datos procesados y limpios
│   └── ladb_mobility_economy_2024_clean.csv  # Dataset integrado
└── README.md                                 # Este archivo

## Descripción de archivos

### raw/ (Datos crudos)
- **oecd_city_economy.csv**: Datos directos de OECD Cities
  - Contiene: PIB per cápita, desempleo, contaminación (PM2.5), población
  - Ciudades de América Latina (Brasil, Argentina, etc.)
  - Año: 2023-2024

### processed/ (Datos procesados)
- **ladb_mobility_economy_2024_clean.csv**: 
  - Resultado de combinar datos de movilidad (TomTom) con datos económicos (OECD)
  - Sin valores faltantes (NaN)
  - Datos normalizados y limpios
  - Listo para análisis directo en Jupyter

## Cómo usar

**Para análisis exploratorio:** Usa `processed/ladb_mobility_economy_2024_clean.csv`

**Para reproducir procesamiento:** Usa archivos en `raw/`

## Variables principales

- **City**: Nombre de la ciudad
- **Country**: País
- **GDP_per_capita**: PIB per cápita (USD)
- **Unemployment**: Tasa de desempleo (%)
- **PM25**: Contaminación del aire (μg/m³)
- Listo para análisis directo en Jupyter

## Cómo usar

**Para análisis exploratorio:** Usa `processed/ladb_mobility_economy_2024_clean.csv`

**Para reproducir procesamiento:** Usa archivos en `raw/`

## Variables principales

- **City**: Nombre de la ciudad
- **Country**: País
- **GDP_per_capita**: PIB per cápita (USD)
- **Unemployment**: Tasa de desempleo (%)
- **PM25**: Contaminación del aire (μg/m³)
- **Population**: Población urbana (millones)
- **Traffic_Index**: Índice de congestión vehicular (TomTom, 0-100)
- **Travel_Time_10km**: Tiempo de viaje promedio por 10 km (minutos)

