# Datos - Movilidad Urbana y Economía en América Latina

Esta carpeta contiene todos los archivos de datos utilizados en el análisis.

---

## 📁 Estructura

```
data/
├── raw/
│   └── oecd_city_economy.csv          # Datos económicos OECD (original)
├── processed/
│   └── ladb_mobility_economy_2024_clean.csv  # Dataset integrado y limpio
└── README.md                           # Este archivo
```

---

## 📊 Descripción de Archivos

### `raw/oecd_city_economy.csv` ✅

**Estado:** Incluido en GitHub

**Tamaño:** ~5 KB

**Descripción:** Datos económicos de 15 ciudades latinoamericanas obtenidos de OECD Cities Programme

**Estructura:**
```
Columnas: año, ciudad, país, pib_per_capita, desempleo, pm25, población
Filas: 30 registros (15 ciudades × 2 años: 2023-2024)
```

**Ejemplo:**
```
año,ciudad,país,pib_per_capita,desempleo,pm25,población
2024,Bogotá,Colombia,11442.50,10.5,25.3,11300000
2024,Lima,Perú,9542.30,8.2,35.7,9500000
```

**Variables:**
- `año`: Año del registro (2023, 2024)
- `ciudad`: Nombre de la ciudad
- `país`: País donde se ubica
- `pib_per_capita`: PIB per cápita en USD
- `desempleo`: Tasa de desempleo (%)
- `pm25`: Contaminación PM2.5 (µg/m³)
- `población`: Población urbana (habitantes)

**Origen:** [OECD Cities Database](https://www.oecd.org/cfe/leed/cities/)

---

### `tomtom_traffic.csv` 📥

**Estado:** NO incluido en GitHub (muy pesado)

**Tamaño:** ~140 MB

**Descripción:** Datos diarios de tráfico y congestión de 15 ciudades latinoamericanas en 2024

**Estructura:**
```
Columnas: país, ciudad, timestamp, traffic_index_live, avg_speed_relative, jams_delay
Filas: 1,004,464 registros (datos diarios por ciudad)
```

**Ejemplo:**
```
país,ciudad,timestamp,traffic_index_live,avg_speed_relative,jams_delay
Colombia,Bogotá,2024-01-15,37.6,42.3,1141.55
Perú,Lima,2024-01-15,35.2,45.1,987.30
```

**Variables:**
- `país`: País de la ciudad
- `ciudad`: Nombre de la ciudad
- `timestamp`: Fecha y hora del registro
- `traffic_index_live`: Índice de tráfico en vivo (0-100, donde 100 es congestión máxima)
- `avg_speed_relative`: Velocidad promedio relativa (% de velocidad libre)
- `jams_delay`: Demora acumulada en congestión (minutos)

**Descarga:**
- 🔗 [Google Drive Link](https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link)
- Alternativa automática: El notebook descarga usando `gdown` si ejecutas la primera celda

**Por qué no está en GitHub:**
- Excede límite de GitHub (100 MB máx por archivo)
- Es más eficiente almacenar en nube para grandes datasets
- Reduce tamaño de clonación del repositorio

**Origen:** [TomTom Traffic Index](https://www.tomtom.com/traffic-index/)

---

### `processed/ladb_mobility_economy_2024_clean.csv` 🔧

**Estado:** Generado por el notebook (no en GitHub)

**Tamaño:** ~2 KB

**Descripción:** Dataset final integrado y limpio, resultado de combinar datos de OECD y TomTom

**Estructura:**
```
Columnas: ciudad, país, año, pib_per_capita, desempleo, pm25, población, 
          traffic_index_live, avg_speed_relative, jams_delay
Filas: 15 registros (15 ciudades, solo 2024)
```

**Ejemplo:**
```
ciudad,país,año,pib_per_capita,desempleo,pm25,población,traffic_index_live,avg_speed_relative,jams_delay
Bogotá,Colombia,2024,11442.50,10.5,25.3,11300000,37.6,42.3,1141.55
Lima,Perú,2024,9542.30,8.2,35.7,9500000,35.2,45.1,987.30
```

**Cómo se genera:**
1. Se carga `tomtom_traffic.csv` y se agrega por ciudad-año
2. Se carga `oecd_city_economy.csv`
3. Se realiza INNER JOIN por ciudad + país
4. Se filtran solo registros de 2024
5. Se exporta a CSV

**Código (en el notebook):**
```python
# Agregación de tráfico
traffic_city_year = traffic[traffic['year'] == 2024].groupby('city').agg({
    'traffic_index_live': 'mean',
    'avg_speed_relative': 'mean',
    'jams_delay': 'mean'
}).reset_index()

# Merge con OECD
merged = traffic_city_year.merge(
    eco[eco['year'] == 2024],
    on='city',
    how='inner'
)

# Exportar
merged.to_csv('data/processed/ladb_mobility_economy_2024_clean.csv', index=False)
```

**Uso:** Este es el archivo que usas para análisis estadístico, visualizaciones y conclusiones

---

## 🔄 Flujo de Datos

```
Google Drive                        Local Repository
(tomtom_traffic.csv)               
        ↓                          
    gdown.download()               
        ↓                          
    /tomtom_traffic.csv            
        ↓                          
    ┌──────────────┐               
    │   Notebook   │               
    │ (limpieza)   │               
    └──────────────┘               
        ↓                          
    data/raw/oecd_city_economy.csv   (desde GitHub)
        ↓                          
    ┌──────────────────┐           
    │  Integración &   │           
    │  Agregación      │           
    └──────────────────┘           
        ↓                          
    data/processed/
    ladb_mobility_economy_2024_clean.csv
        ↓                          
    Análisis Estadístico
    Visualizaciones
    Reportes
```

---

## 📥 Cómo Obtener los Datos

### Para `raw/oecd_city_economy.csv`
✅ Ya está en el repositorio. No necesitas hacer nada.

### Para `tomtom_traffic.csv`

**Opción 1: Descarga manual**
1. Ve a: https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link
2. Haz clic en "Descargar"
3. Coloca el archivo en la **raíz del proyecto** (mismo nivel que `README.md`)

**Opción 2: Descarga automática en el notebook**
```python
import gdown

file_id = "1GKKkybzladDfkA5O5YgitFVXvA5RHb-R"
url = f"https://drive.google.com/uc?id={file_id}"
gdown.download(url, 'tomtom_traffic.csv', quiet=False)
```

### Para `processed/ladb_mobility_economy_2024_clean.csv`
✅ Se genera automáticamente al ejecutar el notebook. No necesitas descargarlo.

---

## 🔐 Acceso a los Datos

**Licencias y Uso:**
- **OECD:** Datos públicos con atribución requerida
- **TomTom:** Datos públicos del Traffic Index

Consulta los términos de uso de cada fuente antes de redistribuir los datos.

---

## ✅ Validación de Datos

Al ejecutar el notebook, se generan validaciones automáticas:
- Valores faltantes
- Tipos de datos
- Rangos de valores (ej: tráfico 0-100)
- Completitud temporal (2024 completo)

---

## 📝 Notas

- Los datos de 2023 están disponibles en `oecd_city_economy.csv` pero el análisis se enfoca en 2024
- TomTom Traffic Index se actualiza diariamente; el archivo descargado es un snapshot de 2024
- Los datos de PM2.5 son promedios anuales de OECD
- El PIB per cápita está expresado en USD PPA (Paridad de Poder Adquisitivo)

---

**Última actualización:** Mayo 2026
