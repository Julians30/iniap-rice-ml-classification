# Clasificación de variedades de arroz INIAP con aprendizaje automático

[![Publicado](https://img.shields.io/badge/Publicado-AgriEngineering%202026-2F855A?style=flat-square)](https://www.mdpi.com/2624-7402/8/3/100)
[![DOI](https://img.shields.io/badge/DOI-10.3390%2Fagriengineering8030100-1F3A5F?style=flat-square)](https://doi.org/10.3390/agriengineering8030100)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)

Código del artículo:

**Coronel-Reyes, J.; Haro-Sarango, A.; Delgado-Vera, C.; Triviño-Sánchez, J. (2026). Comparative Evaluation of Machine Learning Algorithms for the Identification and Morphological Classification of Rice Grains. *AgriEngineering*, 8(3), 100.** https://doi.org/10.3390/agriengineering8030100

Clasificación multiclase de granos de arroz de tres variedades certificadas del INIAP (Ecuador) a partir de descriptores morfométricos. Compara modelos clásicos de aprendizaje automático y una red neuronal multicapa.

> Este fue el primer trabajo de mi línea sobre morfometría de granos. El trabajo posterior, con validación anidada y análisis de suficiencia de la representación, está en [geometric-invariance-bean-rice](https://github.com/Julians30/geometric-invariance-bean-rice).

## Datos

### Conjunto analizado en el artículo

El estudio publicado analizó **2.400 granos**, balanceados entre las tres variedades:

| Variedad | Granos |
|---|---:|
| INIAP-11 | 800 |
| INIAP-12 | 800 |
| INIAP-20 | 800 |
| **Total** | **2.400** |

Descriptores morfométricos (7): `AREA`, `PERIMETER`, `MAJOR_AXIS`, `MINOR_AXIS`, `ECCENTRICITY`, `CONVEX_AREA`, `EXTENT`.

El conjunto completo **no se distribuye en este repositorio**. Según la declaración de disponibilidad de datos del artículo, puede solicitarse al autor de correspondencia.

### Muestra de demostración incluida

> **Importante:** `Granos de Arroz.xlsx` **no es el conjunto del artículo**. Es una muestra de demostración de **500 registros**, incluida a pedido de la revisión por pares para que el código pueda ejecutarse de principio a fin. Tiene las mismas 7 variables y la columna `CLASS` con la variedad.

| Variedad | Registros en la muestra |
|---|---:|
| INIAP-11 | 171 |
| INIAP-12 | 172 |
| INIAP-20 | 157 |
| **Total** | **500** |

Las métricas que se obtienen al ejecutar `ml_rice.py` con esta muestra **no reproducen las cifras publicadas**, que provienen de los 2.400 granos. La muestra sirve para verificar el flujo de análisis, no los resultados.

## Qué hace el script

`ml_rice.py` (exportado desde Google Colab) realiza, en orden:

1. Estadísticos descriptivos, cuartiles y tablas de frecuencia por variedad.
2. Matriz de correlación y factor de inflación de la varianza (VIF) para detectar colinealidad.
3. Entrenamiento y evaluación en partición entrenamiento/prueba de regresión logística, Random Forest, KNN, árbol de decisión, SVM y Naive Bayes.
4. Validación cruzada de 5 pliegues.
5. Búsqueda de hiperparámetros con `GridSearchCV` y curva de aprendizaje para SVC.
6. Red neuronal multicapa (`MLPClassifier`) y comparación con y sin PCA.

## Cómo ejecutarlo

El script está pensado para Google Colab: al inicio pide subir `Granos de Arroz.xlsx` con `files.upload()`. Para ejecutarlo localmente, elimina esa línea y deja el archivo Excel en la misma carpeta.

Dependencias principales: `pandas`, `numpy`, `scikit-learn`, `statsmodels`, `matplotlib`, `seaborn` y `openpyxl`.

## Limitaciones

El escalado se ajusta sobre todos los datos antes de dividir en entrenamiento y prueba, por lo que las métricas pueden ser algo optimistas. Los resultados deben leerse como un ejercicio exploratorio, no como una evaluación definitiva.

## Autores

Julián Coronel-Reyes, Alexander Haro-Sarango, Carlota Delgado-Vera y Johnny Triviño-Sánchez.

## Cómo citar

Si utilizas este código, cita el artículo:

```bibtex
@article{CoronelReyes2026Rice,
  author  = {Coronel-Reyes, Julián and Haro-Sarango, Alexander and Delgado-Vera, Carlota and Triviño-Sánchez, Johnny},
  title   = {Comparative Evaluation of Machine Learning Algorithms for the Identification and Morphological Classification of Rice Grains},
  journal = {AgriEngineering},
  year    = {2026},
  volume  = {8},
  number  = {3},
  pages   = {100},
  doi     = {10.3390/agriengineering8030100}
}
```

Los metadatos de cita también están en [`CITATION.cff`](CITATION.cff).
