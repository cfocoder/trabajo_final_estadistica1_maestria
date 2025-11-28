# Análisis Estadístico de Retrasos en Vuelos ✈️

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## 📋 Descripción

Análisis estadístico de ~6 millones de vuelos comerciales de EE.UU. (2015) usando el dataset del US Department of Transportation. Proyecto final de Métodos Estadísticos Básicos que aplica técnicas descriptivas, inferenciales y predictivas para identificar patrones de retrasos.

**Autor:** Héctor Gabriel Sánchez Pérez  
**Dataset:** [Airline Flight Delays 2015](https://huggingface.co/datasets/hsanchezp/us-dot-flight-delays-2015) (Maven Analytics)

## 🎯 Hallazgos Clave

- **37.08%** de vuelos tienen retraso de salida (media: 9.37 min)
- **Correlación salida-llegada:** r=0.9447 → un retraso de salida casi siempre resulta en retraso de llegada
- **Mejor aerolínea:** Southwest (10.58 min) vs **Peor:** Spirit (15.94 min) - diferencia significativa (p<0.001)
- **Peor día:** Viernes (39.74% con retraso) vs **Mejor:** Martes (35.40%)
- **Aeropuerto con más retrasos:** ATL-Atlanta (61,703 vuelos)
- **Principal causa de cancelación:** Clima (54.35%)

## 🛠️ Stack Tecnológico

- **Procesamiento:** Ibis Framework (big data), Pandas, NumPy
- **Estadística:** SciPy (t-test, ANOVA, Chi²), Statsmodels (regresión)
- **ML:** Scikit-learn
- **Visualización:** Matplotlib, Seaborn

## 📦 Instalación

```bash
# Clonar repositorio
git clone https://github.com/cfocoder/trabajo_final_estadistica1_maestria.git
cd trabajo_final_estadistica1_maestria

# Instalar dependencias
poetry install && poetry shell
# O con pip: python -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt

# Descargar dataset (HuggingFace)
wget https://huggingface.co/datasets/hsanchezp/us-dot-flight-delays-2015/resolve/main/flights.parquet
wget https://huggingface.co/datasets/hsanchezp/us-dot-flight-delays-2015/resolve/main/airlines.parquet
wget https://huggingface.co/datasets/hsanchezp/us-dot-flight-delays-2015/resolve/main/airports.parquet
wget https://huggingface.co/datasets/hsanchezp/us-dot-flight-delays-2015/resolve/main/cancellation_codes.parquet

# Ejecutar notebook
jupyter notebook trabajo_final_estadistica.ipynb
```

## 📊 Métodos Estadísticos

**Descriptivos:** Media, mediana, varianza, desviación estándar, asimetría, curtosis, outliers, tablas de contingencia, correlación

**Probabilidad:** Probabilidades condicionales, Teorema de Bayes, valor esperado

**Distribuciones:** Normal (Shapiro-Wilk, Q-Q plots), Binomial, Poisson

**Inferencia:** Intervalos de confianza (95%), T-test, ANOVA, Chi-cuadrada

**Regresión:** Lineal simple (OLS), Logística (clasificación binaria)

## 🎓 Contexto

Proyecto final de **Métodos Estadísticos Básicos** - Maestría en Ciencia de Datos (CUCEA) - Universidad de Guadalajara.

## 👤 Autor

**Héctor Gabriel Sánchez Pérez**  
GitHub: [@cfocoder](https://github.com/cfocoder)

---

⭐ Si te resultó útil, dale una estrella en GitHub!
