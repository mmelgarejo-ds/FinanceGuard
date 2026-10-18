# FinanceGuard — Predicción de Churn en Banca Digital

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-FF6600?style=flat&logo=xgboost&logoColor=white)

Proyecto de Machine Learning para predecir abandono de clientes en un banco digital ficticio.
Módulo 4 — Soy Henry Data Science AI.

---

## Problema de negocio

Un banco digital con 10.000 clientes y una tasa de churn del 20% necesita identificar
qué clientes van a abandonar el servicio antes de que ocurra, para tomar acciones de
retención a tiempo.

---

## Dataset

- 10.000 registros · 11 features tras limpieza
- Variable objetivo: `Exited` (1 = abandonó, 0 = se quedó)
- Fuente: Churn_Modelling.csv

---

## Notebooks

| # | Notebook | Contenido |
|---|---|---|
| 1 | EDA + Regresión Logística | Análisis exploratorio, baseline AUC 0.775 |
| 2 | Gradient Boosting y Optimización | Random Forest, XGBoost, LightGBM, CatBoost, Optuna |
| 3 | Aprendizaje No Supervisado | K-Means, DBSCAN, PCA, t-SNE |
| 4 | Optimización de Threshold | Threshold 0.309, Recall 0.666 |

---

## Resultados

| Métrica | Baseline (Regresión Logística) | Modelo final (CatBoost) | Mejora |
|---|---|---|---|
| AUC | 0.775 | **0.868** | +0.093 |
| Recall | 0.19 | **0.666** | +0.476 |
| Precision | — | 0.80 | — |

El baseline detectaba menos de 1 de cada 5 clientes que efectivamente abandonaban (recall 0,19). El modelo final detecta 2 de cada 3 (recall 0,666) — la mejora central del proyecto no está en el AUC, sino en esa capacidad de detección real.

**Por qué se priorizó recall sobre precision:** en un problema de retención, el costo de no detectar a un cliente que se va (falso negativo) es perder ese cliente; el costo de contactar a alguien que en realidad no se iba (falso positivo) es, como máximo, una acción de retención de más. Esa asimetría justifica optimizar el threshold para maximizar recall en vez de dejarlo en el valor por defecto — con threshold optimizado (0,309) se detectan **72 clientes en riesgo adicionales** frente a la configuración default (0,5).

**Hallazgos clave:**
- Clientes en Alemania tienen 2.27x más probabilidad de churn
- Clientes inactivos tienen 0.36x probabilidad (factor protector invertido)
- Segmento de mayor riesgo: balance alto + inactivo → churn hasta 78% (DBSCAN)

**Prevención de fuga de datos:** se eliminaron `RowNumber`, `CustomerId` y `Surname` antes de entrenar — son identificadores sin poder predictivo real que podrían filtrar información indirecta (ej. orden de carga de los datos) sin aportar señal genuina de negocio.

---

## Stack

Python · Pandas · scikit-learn · XGBoost · LightGBM · CatBoost · Optuna · Matplotlib · Seaborn

---

## Autor

Mauricio Melgarejo · [LinkedIn](https://www.linkedin.com/in/mauricio-daniel-melgarejo-amaro-482596105/) · [GitHub](https://github.com/mmelgarejo-ds)
