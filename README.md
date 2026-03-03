# Telecom X — Churn de Clientes (ETL + EDA)

Proyecto de análisis exploratorio orientado a entender los factores asociados a la evasión de clientes (**churn**) en Telecom X.  
Se realiza un flujo completo de **Extracción → Transformación (ETL) → Análisis Exploratorio (EDA)**, dejando el dataset listo para una etapa posterior de modelado predictivo.

---

## Objetivo

- Medir y visualizar la distribución de **churn**.
- Detectar patrones de churn según:
  - Variables categóricas (género, tipo de contrato, método de pago, servicio de internet, etc.)
  - Variables numéricas (antigüedad, cargo mensual, cargo total, etc.)
- Estandarizar datos (renombrar, traducir, normalizar categorías y binarizar variables) para habilitar análisis y modelos.

---

## Fuente de datos

Los datos se obtienen desde un JSON publicado en GitHub (API/RAW):

- TelecomX_Data.json: (raw)  
  > Se consume directamente desde el notebook mediante `pandas.read_json`.

---

## Contenido del proyecto

- **Notebook principal**: contiene todo el flujo de trabajo:
  - Extracción desde API
  - Flatten del JSON
  - Limpieza y tratamiento de inconsistencias
  - Estandarización y transformación (incluye creación de `churn_bin`)
  - EDA (descriptivo + gráficos)
  - Informe final
  - Correlaciones y relaciones entre variables

> Nota: Todo está en español excepto **churn**.

---

## Flujo de trabajo (resumen)

### A) Extracción
- Importación del JSON desde la fuente (API/RAW).

### B) Calidad de datos
- Revisión de tipos, nulos y duplicados (por `customerID`).

### C) Correcciones
- Conversión de variables numéricas (`cargo_total`, `cargo_mensual`, `antigüedad_meses`).
- Regla de coherencia: si `antigüedad_meses == 0` y `cargo_total` es nulo, se asigna `0`.

### D) Estandarización / Transformación
- Renombrado de columnas al español.
- Normalización de categorías:
  - `"No internet service"` → `"No"`
  - `"No phone service"` → `"No"`
- Traducción de categorías (internet/contrato/pago).
- Creación de `churn_bin` (Yes=1, No=0).
- Binarización de variables Yes/No.

### E–H) EDA
- Estadísticas descriptivas.
- Distribución de churn.
- churn por variables categóricas (barras 100% apiladas).
- Variables numéricas por churn (histogramas y comparación de medias).

### Informe final + correlación
- Resumen ejecutivo de hallazgos y recomendaciones.
- Heatmap de correlaciones y ranking de correlación con `churn_bin`.

---

## Visualización (estilo)
Se utiliza una paleta consistente para los gráficos:

- **Clientes fieles (churn=No)**: Turquesa
- **Clientes que evaden (churn=Yes)**: Violáceo

---

## Requisitos

- Python 3.10+ (recomendado)
- Librerías:
  - pandas
  - numpy
  - matplotlib
  - seaborn (solo si se usa en correlaciones)
  
Instalación rápida:
```bash
pip install pandas numpy matplotlib seaborn
