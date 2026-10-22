# Clasificación de variedades de arroz INIAP con aprendizaje automático

Proyecto inicial de clasificación multiclase de granos de arroz de tres variedades certificadas del INIAP (Ecuador) a partir de descriptores morfométricos. Compara modelos clásicos de aprendizaje automático y una red neuronal multicapa.

> Este es un proyecto exploratorio temprano. El trabajo posterior y más riguroso sobre morfometría de granos, con validación anidada y análisis de suficiencia de la representación, está en [geometric-invariance-bean-rice](https://github.com/Julians30/geometric-invariance-bean-rice).

## Datos

`Granos de Arroz.xlsx` contiene 500 granos con 7 descriptores morfométricos y la variedad como etiqueta.

| Variedad | Granos |
|---|---:|
| INIAP-12 | 172 |
| INIAP-11 | 171 |
| INIAP-20 | 157 |

Descriptores: `AREA`, `PERIMETER`, `MAJOR_AXIS`, `MINOR_AXIS`, `ECCENTRICITY`, `CONVEX_AREA`, `EXTENT`.

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

## Autor

Julián Coronel Reyes
