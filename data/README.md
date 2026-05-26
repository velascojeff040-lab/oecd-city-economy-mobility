# Análisis de Movilidad Urbana y Economía en América Latina 🚗📊

**Proyecto:** Relación entre Congestión Vehicular y Productividad Económica en Ciudades Latinoamericanas (2024)

**Autor:** Jefferson Velasco  
**Repositorio:** [oecd-city-economy-mobility](https://github.com/velascojeff040-lab/oecd-city-economy-mobility)

---

## 📋 Descripción del Proyecto

Este análisis examina la relación entre **movilidad urbana** (congestión vehicular, tiempos de viaje) y **productividad económica** (PIB per cápita) en 15 ciudades de América Latina durante 2024.

### Pregunta Central
¿Existe una relación significativa entre altos niveles de congestión vehicular y menores indicadores de productividad económica? ¿Qué ciudades son prioritarias para inversión en infraestructura de transporte?

### Objetivo
Proporcionar evidencia cuantitativa para decisiones de inversión en movilidad urbana y planificación de transporte público.

---

## 📁 Estructura del Repositorio

```
oecd-city-economy-mobility/
├── data/
│   ├── raw/
│   │   └── oecd_city_economy.csv          # Datos OECD (PIB, desempleo, población)
│   ├── processed/
│   │   └── ladb_mobility_economy_2024_clean.csv  # Dataset integrado y limpio
│   └── README.md                           # Descripción de carpetas de datos
├── notebooks/
│   └── OECD_City_Economy_and_Mobility_Analysis (2).ipynb  # Análisis principal
├── .gitignore
├── README.md                               # Este archivo
└── requirements.txt                        # Dependencias del proyecto
```

---

## 📊 Datos Utilizados

### Fuentes Primarias

| Fuente | Cobertura | Variables | Ubicación |
|--------|-----------|-----------|-----------|
| **OECD Cities** | 15 ciudades, 7 países | PIB per cápita, Desempleo, PM2.5, Población | `data/raw/oecd_city_economy.csv` ✅ En GitHub |
| **TomTom Traffic Index** | 15 ciudades (2024) | Congestión, Tiempos de viaje, Demoras, Índice de tráfico | [Google Drive Link](#-datos-de-tomtom-traffic) |

### Ciudades Analizadas
- 🇦🇷 **Argentina:** Buenos Aires
- 🇧🇷 **Brasil:** São Paulo, Rio de Janeiro, Brasília, Salvador, Belo Horizonte, Curitiba, Porto Alegre
- 🇨🇴 **Colombia:** Bogotá
- 🇵🇪 **Perú:** Lima
- 🇨🇱 **Chile:** Santiago
- 🇺🇾 **Uruguay:** Montevideo

---

## 🗂️ Datos de TomTom Traffic

⚠️ **Nota sobre el dataset de TomTom Traffic:**

El archivo `tomtom_traffic.csv` contiene datos de tráfico de **1,004,464 registros diarios** (aproximadamente **240 MB**). 

### ❌ NO está en GitHub porque:
- Excede límites de repositorio (GitHub: máx. 100 MB por archivo)
- Sería ineficiente para clonar/actualizar el repo
- Es un dataset "pesado" más apropiado para almacenamiento en la nube

### ✅ Archivo alojado en Google Drive:

🔗 **[Descargar tomtom_traffic.csv](https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link)**

**Instrucciones para descargar:**
1. Abre el [enlace de Google Drive](https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link)
2. Haz clic en el ícono de **descargar** (esquina superior derecha)
3. Coloca el archivo en la **carpeta raíz** del proyecto

**Alternativa: Descarga automática en el notebook**

El notebook descargar el archivo automáticamente usando `gdown`:
```python
import gdown

file_id = "1GKKkybzladDfkA5O5YgitFVXvA5RHb-R"
url = f"https://drive.google.com/uc?id={file_id}"
gdown.download(url, 'tomtom_traffic.csv', quiet=False)
traffic = pd.read_csv('tomtom_traffic.csv')
```

---

## 🔧 Instalación y Configuración

### Requisitos
- Python 3.8+
- pandas, numpy, matplotlib, seaborn
- gdown (para descargar datos de Google Drive)

### Pasos de Instalación

```bash
# 1. Clonar el repositorio
git clone https://github.com/velascojeff040-lab/oecd-city-economy-mobility.git
cd oecd-city-economy-mobility

# 2. (Opcional) Crear entorno virtual
python3 -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Descargar datos de TomTom Traffic
# Opción A: Descargar manualmente desde Google Drive (arriba)
# Opción B: El notebook descarga automáticamente si gdown está instalado
```

---

## 📈 Análisis Principal

### Notebook: `OECD_City_Economy_and_Mobility_Analysis (2).ipynb`

El notebook contiene **9 secciones principales**:

1. **Ingesta de Datos**
   - Importación de librerías necesarias
   - Descarga automática de `tomtom_traffic.csv` desde Google Drive
   - Carga de `oecd_city_economy.csv`

2. **Evaluación de Estructura y Calidad**
   - Diagnóstico de tipos de datos
   - Identificación de valores faltantes
   - Análisis de completitud

3. **Estandarización de Nomenclatura**
   - Conversión a formato `snake_case`
   - Normalización de nombres de columnas
   - Consistencia de tipos de datos

4. **Conversión de Tipos de Datos**
   - Conversión de fechas a datetime
   - Limpieza de valores numéricos
   - Manejo de delimitadores locales

5. **Extracción de Período Temporal**
   - Extracción de año de timestamps
   - Filtrado para 2024

6. **Agregación de Indicadores de Movilidad**
   - Agregación a nivel ciudad-año
   - Cálculo de promedios de congestión, tiempos de viaje

7. **Integración de Datos: Movilidad + Economía**
   - INNER JOIN entre datasets de tráfico y OECD
   - Dataset final unificado

8. **Análisis Exploratorio Visual**
   - Distribuciones de tráfico y PIB
   - Comparativas entre ciudades
   - Identificación de patrones

9. **Exportación**
   - Generación de `data/processed/ladb_mobility_economy_2024_clean.csv`
   - Dataset listo para análisis estadístico

---

## 🎯 Hallazgos Principales

### Ciudad Prioritaria: Bogotá 🔴

Bogotá se destaca como la ciudad con **mayor necesidad de inversión en movilidad**:

| Indicador | Valor |
|-----------|-------|
| **Traffic Index** | ≈ 37.6 (muy alto) |
| **Jams Delay (minutos)** | ≈ 1,141.55 |
| **PIB per cápita (USD)** | ≈ $11,442 (moderado) |
| **Población** | ≈ 11.3M |

**Interpretación:** Alta congestión con productividad económica moderada sugiere que **mejoras en movilidad podrían generar impactos positivos significativos** en competitividad urbana.

### Comparación Regional Estimada

| Ciudad | Traffic Index | PIB per cápita | Prioridad |
|--------|---------------|----------------|-----------|
| Bogotá | 37.6 | $11,442 | 🔴 Crítico |
| Lima | ~35 | $9,500+ | 🟠 Alto |
| São Paulo | ~40 | ~$13,000 | 🟠 Alto |
| Buenos Aires | ~25 | $18,117 | 🟢 Mejor |
| Montevideo | ~18 | $21,111+ | 🟢 Óptimo |

---

## 💡 Recomendaciones de Inversión

### Para Bogotá (Prioridad 1)

1. **Expansión de Metro:** Aumentar cobertura de transporte masivo
2. **Infraestructura de Ciclorrutas:** Movilidad sostenible y alternativa
3. **Gestión Inteligente de Tráfico:** Semáforos adaptativos, IoT urbano
4. **Flexibilidad Laboral:** Teletrabajo y horarios escalonados
5. **Integración Multimodal:** Conectividad BRT-Metro-Cicloruta-TransMilenio

### Para Lima y São Paulo (Prioridad 2)

- Mejora y ampliación de transporte público existente
- Nuevas líneas de metro/BRT
- Estacionamientos park-and-ride

### Para Buenos Aires y Montevideo (Mantenimiento)

- Modernización de sistemas existentes
- Mantenimiento preventivo
- Innovación en movilidad (e-scooters, bikesharing)

---

## 📊 Próximos Pasos (Análisis Adicional)

- [ ] Análisis de correlación Pearson/Spearman entre congestión y PIB
- [ ] Modelado predictivo (regresión lineal)
- [ ] Análisis de elasticidad (% cambio en PIB por % reducción de congestión)
- [ ] Expansión temporal (2023-2025)
- [ ] Integración de costos de congestión (económicos, ambientales)
- [ ] Proyecciones de impacto de inversión en movilidad

---

## 📋 Dependencias

Ver `requirements.txt`:

```
pandas>=1.3.0
numpy>=1.20.0
matplotlib>=3.3.0
seaborn>=0.11.0
gdown>=4.4.0
jupyter>=1.0.0
```

Para instalar:
```bash
pip install -r requirements.txt
```

---

## 📝 Notas sobre los Archivos de Datos

### `data/raw/oecd_city_economy.csv` ✅
- **Incluido en GitHub:** Sí
- **Tamaño:** ~5 KB (pequeño y manejable)
- **Contenido:** Año, Ciudad, País, PIB per cápita, Desempleo, PM2.5, Población
- **Registros:** 30 (15 ciudades × 2 años: 2023-2024)

### `tomtom_traffic.csv` ❌
- **Incluido en GitHub:** No (muy pesado)
- **Tamaño:** ~240 MB
- **Contenido:** País, Ciudad, Timestamp, Índice de tráfico, Tiempos de viaje, Demoras
- **Registros:** 1,004,464 (datos diarios)
- **Ubicación:** [Google Drive](https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link)
- **Razón de no incluirlo:** Límite de GitHub (100 MB/archivo), eficiencia de repo, almacenamiento en nube

### `data/processed/ladb_mobility_economy_2024_clean.csv` ✅
- **Generado por el notebook:** Sí (se crea al ejecutar)
- **Tamaño:** ~2 KB
- **Contenido:** Dataset final integrado y limpio
- **Uso:** Análisis estadístico y visualizaciones
- **Incluido en GitHub:** No (generado localmente)

---

## 🔐 Acceso a Datos

El notebook utiliza `gdown` para descargar automáticamente `tomtom_traffic.csv` desde Google Drive. 

**No requiere autenticación** si el enlace es público.

Si tienes problemas:
1. Verifica que el [archivo sea accesible](https://drive.google.com/file/d/1GKKkybzladDfkA5O5YgitFVXvA5RHb-R/view?usp=drive_link)
2. Descárgalo manualmente y colócalo en la raíz del proyecto
3. Actualiza la ruta en el notebook si es necesario

---

## 🤝 Contribuciones

Este proyecto es académico/de investigación. Para sugerencias o mejoras:
- Abre un **Issue** en GitHub
- Propón cambios vía **Pull Request**

---

## 📧 Contacto

**Autor:** Jefferson Velasco  
**GitHub:** [@velascojeff040-lab](https://github.com/velascojeff040-lab)

---

## 📄 Licencia y Datos

Este proyecto utiliza datos públicos:
- **OECD:** Datos públicos con atribución
- **TomTom Traffic Index:** Datos públicos disponibles

Consulta los términos de uso de cada fuente antes de redistribuir.

---

## 📚 Referencias

- [OECD Cities Programme](https://www.oecd.org/cfe/leed/cities/)
- [TomTom Traffic Index](https://www.tomtom.com/traffic-index/)
- [Movilidad Urbana - CEPAL](https://www.cepal.org/)
- [Congestión y Productividad - BID](https://www.iadb.org/)

---

**Última actualización:** Mayo 2026  
**Versión del notebook:** 2.0 (JSON validado ✅)  
**Estado del proyecto:** Análisis principal completado
