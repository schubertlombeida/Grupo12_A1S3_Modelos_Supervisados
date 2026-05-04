# Grupo 12 - A1.S3 - Modelos supervisados aplicados al dataset de salarios Cervecería

## Información general

**Materia:** Aprendizaje Automático  
**Docente:** Gladys María Villegas Rugel  
**Grupo:** 12  
**Actividad:** A1.S3 - Modelos supervisados  
**Dataset validado:** `Salarios_Cerveceria.csv`

## Integrantes

- Schubert Stalin Lombeida Manjarrez
- José Luis Peñafiel Fernández
- Juan Carlos Bajaña Gutiérrez
- Niko Dimitri Jiménez Bruno

## Resumen del problema

Este repositorio documenta el desarrollo de modelos supervisados de clasificación y regresión aplicados al dataset de salarios de Cervecería. El caso se enfoca en analítica laboral y salarial, con el objetivo de identificar patrones relacionados con horas extra y estimar el salario total de los empleados a partir de variables laborales, salariales y contextuales.

El trabajo incluye análisis exploratorio de datos, preprocesamiento, entrenamiento de modelos, evaluación experimental, visualización de resultados y conclusiones técnicas.

## Dataset

El archivo principal se encuentra en:

```text
data/Salarios_Cerveceria.csv
```

Características generales del dataset:

- Registros: **40.544**
- Variables originales: **14**
- Período: **2021-2025**
- Departamentos: **8**
- Cargos: **14**
- Oficinas: **5**

Variables principales:

- `SalarioBase`
- `HorasExtra`
- `OtrosPagos`
- `Beneficios`
- `SalarioTotal`
- `SalarioTotalConBeneficios`
- `Departamento`
- `Cargo`
- `Oficina`
- `Año`
- `TipoContrato`

## Variables objetivo

### Clasificación

La variable objetivo de clasificación es:

```text
TieneOvertime
```

Esta variable fue construida a partir de `HorasExtra`:

- `0`: empleado sin horas extra.
- `1`: empleado con horas extra.

### Regresión

La variable objetivo de regresión es:

```text
SalarioTotal
```

El objetivo es estimar el salario total percibido por el empleado a partir de variables laborales y salariales.

## Metodología

El flujo metodológico aplicado fue el siguiente:

1. Carga y validación del dataset.
2. Análisis exploratorio de datos (EDA).
3. Conversión de variables numéricas.
4. Tratamiento de valores nulos mediante imputación por mediana.
5. Winsorización mediante rango intercuartílico (IQR) para reducir el impacto de valores extremos.
6. Creación de variables derivadas: `BeneficiosRatio`, `OvertimeRatio`, `LogSalarioTotal` y `TieneOvertime`.
7. Codificación de variables categóricas mediante `LabelEncoder`.
8. Escalado de variables con `StandardScaler`.
9. División del dataset en entrenamiento y prueba bajo proporción 80/20.
10. Entrenamiento y comparación de modelos supervisados.

## Modelos implementados

### Modelos de clasificación

- Logistic Regression
- Decision Tree Classifier con profundidad controlada (`max_depth=6`)
- Random Forest Classifier
- Support Vector Machine (SVM) con kernel RBF

### Modelos de regresión

- Regresión Lineal
- Ridge Regression
- Decision Tree Regressor
- Random Forest Regressor

## Resultados principales

### Clasificación

| Modelo | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.9805 | 0.9817 | 0.9987 | 0.9902 | 0.9451 |
| Decision Tree (d=6) | 0.9809 | 0.9809 | 1.0000 | 0.9904 | 0.7952 |
| Random Forest | 0.9809 | 0.9809 | 1.0000 | 0.9904 | 0.9629 |
| SVM (RBF, 20%) | 0.9809 | 0.9809 | 1.0000 | 0.9904 | 0.9924 |

**Resultado destacado:** SVM con kernel RBF obtuvo el mayor AUC-ROC, mientras que Decision Tree, Random Forest y SVM alcanzaron el mayor F1-Score.

### Regresión

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Regresión Lineal | 551.1487 | 723.7829 | 0.7028 |
| Ridge (alpha=10) | 551.2487 | 723.7526 | 0.7028 |
| Decision Tree Regressor (d=8) | 196.0456 | 306.0497 | 0.9469 |
| Random Forest Regressor | 31.5005 | 55.1137 | 0.9983 |

**Resultado destacado:** Random Forest Regressor obtuvo el mejor desempeño general en regresión, con el menor RMSE y el mayor R².

## Visualizaciones generadas

Las visualizaciones se encuentran en:

```text
results/figures/
```

Incluyen:

- Distribución de la variable objetivo.
- Matriz de correlación.
- Comparación de métricas de clasificación.
- Matriz de confusión del modelo seleccionado.
- Curvas ROC comparativas.
- Importancia de variables.
- Visualización del árbol de decisión.
- Comparación de R² en regresión.

## Archivos de métricas

Las métricas exportadas se encuentran en:

```text
results/metrics/
```

Archivos incluidos:

- `metrics_classification.csv`
- `metrics_regression.csv`
- `metrics_cv.csv`

## Estructura del repositorio

```text
Grupo12_A1S3/
├── README.md
├── requirements.txt
├── data/
│   └── Salarios_Cerveceria.csv
├── notebooks/
│   └── Grupo12_A1_S3.ipynb
├── docs/
│   └── Informe_Tecnico_A1S3_Grupo12.docx
├── presentation/
│   └── Presentacion_Actividad1_S3_Grupo12.pptx
└── results/
    ├── figures/
    │   ├── arbol_decision.png
    │   ├── comparacion_metricas_clf.png
    │   ├── comparacion_r2_reg.png
    │   ├── curvas_roc.png
    │   ├── distribucion_objetivo.png
    │   ├── importancia_variables.png
    │   ├── matriz_confusion_dt.png
    │   ├── matriz_correlacion.png
    │   ├── pipeline.png
    │   └── salario_por_overtime.png
    └── metrics/
        ├── metrics_classification.csv
        ├── metrics_cv.csv
        └── metrics_regression.csv
```

## Cómo ejecutar el notebook

1. Clonar o descargar el repositorio.
2. Instalar las librerías necesarias:

```bash
pip install -r requirements.txt
```

3. Abrir el notebook:

```text
notebooks/Grupo12_A1_S3.ipynb
```

4. Ajustar la ruta de carga del dataset si se ejecuta fuera de Google Colab:

```python
df = pd.read_csv('data/Salarios_Cerveceria.csv', low_memory=False, encoding='latin1')
```

5. Ejecutar las celdas en orden.

## Limitaciones técnicas

- La variable `TieneOvertime` presenta desbalance de clases: 39.767 registros con overtime y 777 sin overtime.
- El F1-Score alto debe interpretarse con cuidado porque se calcula principalmente sobre la clase positiva, que es mayoritaria.
- Algunas variables salariales pueden actuar como variables proxy de la variable objetivo.
- En futuras iteraciones se recomienda evaluar `class_weight='balanced'`, macro-F1, balanced accuracy y validación cruzada más amplia.

## Conclusiones

Los modelos supervisados permitieron analizar patrones relevantes en el dataset salarial. En clasificación, SVM con kernel RBF presentó la mayor capacidad discriminativa según AUC-ROC, mientras que Decision Tree, Random Forest y SVM alcanzaron el mejor F1-Score. En regresión, Random Forest Regressor obtuvo el mejor desempeño general, mostrando alta capacidad para capturar relaciones no lineales en los datos salariales.

El proyecto cumple con los componentes solicitados: EDA, preprocesamiento, implementación de SVM y Árbol de Decisión, comparación de modelos, visualización de métricas, documentación técnica y reflexión final.

## Referencias de apoyo

- scikit-learn developers. (s. f.). *scikit-learn: Machine Learning in Python*. https://scikit-learn.org/stable/
- Pandas development team. (s. f.). *pandas documentation*. https://pandas.pydata.org/docs/
- Matplotlib development team. (s. f.). *Matplotlib documentation*. https://matplotlib.org/stable/
- GitHub Docs. (s. f.). *Get started with GitHub*. https://docs.github.com/
