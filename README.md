# Segmentación de inmuebles en arriendo – ML no supervisado

**Universidad de Cundinamarca · Especialización en Inteligencia Artificial**
CADI – Introducción a Machine Learning · Periodo 2026-2 · Docente: Ing. Wilson Rojas Reales, PhD(c)

Segmentación de un portafolio de 1 000 inmuebles en arriendo (Suba, Chapinero y Usaquén) con **K-Means**, **clustering jerárquico (Ward)**, **PCA** y **SVD truncado**, desarrollada en Google Colab.

## Contenido

| Ruta | Descripción |
|---|---|
| `notebooks/01_KMeans_Segmentacion_Inmuebles.ipynb` | Carga y calidad de datos, EDA, preprocesamiento, codo y silueta, K-Means con k = 2, 3 y 4, dendrograma de Ward y segmentación propuesta |
| `notebooks/02_PCA_Inmuebles.ipynb` | Varianza explicada, cargas, clusters en el plano PC1–PC2, K-Means sobre componentes vs. variables preprocesadas, comparación con SVD |
| `data/DATASET_INmuebles.xlsx` | Dataset original entregado |
| `figures/` | Figuras generadas por los notebooks |
| `resultados/inmuebles_segmentados.csv` | ID de cada inmueble con su cluster en cada modelo |
| `resultados/perfil_segmentos.csv` | Perfil de los segmentos propuestos |

## Cómo ejecutar en Google Colab

1. Abra el notebook desde GitHub en Colab (`File → Open notebook → GitHub`, o reemplace `github.com` por `colab.research.google.com/github` en la URL del notebook).
2. En la primera celda de código, cambie `URL_GITHUB` por la URL *raw* del dataset en este repositorio:
   `https://raw.githubusercontent.com/<usuario>/<repositorio>/main/data/DATASET_INmuebles.xlsx`
   (alternativa: suba el archivo con el panel de archivos de Colab; si no lo encuentra, el notebook abre un diálogo para subirlo).
3. `Runtime → Run all`.

Localmente: `pip install -r requirements.txt` y ejecute los notebooks desde la raíz del repositorio.

## Principales resultados

- **Calidad de datos:** el Excel trae dos columnas `Estrato`; la segunda (rango 1–4, r ≈ 0,03 con el precio) se descarta como error de captura. `Localidad` y `Tipo_inmueble` tienen una relación 1 a 1.
- **Dimensiones:** 10 columnas originales → 8 características → 12 tras preprocesar (rango efectivo 8) → 2 con PCA.
- **PCA:** PC1 = 46,54 %, PC2 = 13,75 % (60,29 % acumulado); 5 componentes superan el 90 %.
- **K-Means (todas las variables):** k = 2 tiene la mejor silueta (0,350) y separa estrato 2–4 de 5–6. Con k = 3 y 4 los grupos extra se forman por número de baños.
- **K-Means sobre PCA-2:** idéntico con k = 2 (ARI = 1); distinto con k = 3 (ARI = 0,68) y k = 4 (ARI = 0,48).
- **Segmentación recomendada:** K-Means k = 3 sobre precio, área, habitaciones y estrato (silueta = 0,482):

| Segmento | n | Estrato | Área media | Precio medio |
|---|---|---|---|---|
| Económico | 419 | 2–3 | 49,7 m² | $1,47 M |
| Intermedio | 209 | 4 | 85,4 m² | $3,13 M |
| Premium | 372 | 5–6 | 156,1 m² | $6,35 M |

## Tecnologías
Python 3 · pandas · NumPy · scikit-learn · SciPy · Matplotlib · Google Colab
