# MIA_C3_AANS_Corte_03_Bitacora_05

## Detección de Anomalías con DBSCAN

**Alumno:** Víctor Manuel Santos Martínez — Matrícula 253220020
**Materia:** Aprendizaje Automático No Supervisado
**Nombre de la actividad:** Asignación 5 — DBSCAN para Anomalías
**Cuatrimestre:** Tercero — Parcial 3

---

### Descripción de la actividad

Se aplica el algoritmo **DBSCAN** (*Density-Based Spatial Clustering of Applications with Noise*) al dataset `tripadvisor_reviews.csv` (980 turistas, 4 categorías de valoración) para **confirmar de forma independiente** las anomalías detectadas previamente con Isolation Forest en la Actividad 4. Los puntos de ruido (`-1`) de DBSCAN se interpretan como las valoraciones atípicas.

#### Pasos realizados

1. Carga del dataset y eliminación de la columna `user_id`.
2. Exploración de rangos → decisión de **estandarizar** (DBSCAN es sensible a la escala).
3. Reutilización de la función `tune_dbscan` del cuaderno de demostración.
4. Búsqueda en rejilla de `eps` y `min_samples`; la estandarización eleva la mejor silueta de 0.44 a 0.64.
5. Selección de la mejor silueta útil: **eps = 1.6, min_samples = 3** → silueta **0.6359**, **10 anomalías**.
6. Ajuste de un único modelo DBSCAN y visualización de las anomalías en un pair plot.
7. Confirmación cruzada con Isolation Forest: ambos detectan 10 anomalías, 5 en común.

---

### Estructura del proyecto

```
Actividad 5/
├── dbscan_analisis.ipynb                 # Notebook principal (ejecutado)
├── tripadvisor_reviews.csv               # Dataset fuente
├── fig1_pairplot_base.png                # Pair plot inicial
├── fig2_silhouette_heatmap.png           # Silueta según eps y min_samples
├── fig3_kdistance.png                    # Curva de k-distancias (validación de eps)
├── fig4_pairplot_dbscan_anomalias.png    # Anomalías detectadas por DBSCAN
├── fig5_comparacion_iso_dbscan.png       # Concordancia DBSCAN vs Isolation Forest
└── README.md
```

El informe completo (introducción, desarrollo y conclusión) se redactó en la nota de Obsidian
*Asignación 5 — DBSCAN para Anomalías*.

---

### Resultados principales

| Método | Anomalías | Silueta | Coincidencias |
|---|---|---|---|
| DBSCAN (eps=1.6, min_samples=3) | 10 (1.02 %) | 0.6359 | 5 |
| Isolation Forest (contamination=0.01) | 10 (1.02 %) | — | 5 |

---

### Tecnologías utilizadas

- Python 3.12.6 (pyenv)
- scikit-learn 1.7.2 — `DBSCAN`, `StandardScaler`, `silhouette_score`, `NearestNeighbors`
- pandas 2.3.3 · numpy 1.26.4
- seaborn 0.13.2 / matplotlib 3.10.7
- Jupyter / nbconvert 7.16.6
