# Plan: Proyecto Final - Análisis Estadístico de Retrasos en Vuelos

Este proyecto utiliza el dataset "Airline Flight Delays" de Maven Analytics (~6 millones de registros) para demostrar de manera integral los métodos estadísticos aprendidos durante el primer semestre. El análisis se desarrollará en un notebook Jupyter usando Ibis Framework para manipular eficientemente el dataset completo, con visualizaciones claras y explicaciones didácticas dirigidas a una audiencia no experta.

## Pasos

### 1. Preparación y Exploración de Datos
Cargar las tablas parquet (`flights`, `airlines`, `airports`, `cancellation_codes`), unirlas en una tabla consolidada, realizar limpieza inicial y análisis exploratorio básico con estadísticas descriptivas.

**Archivos:** [flights.parquet](flights.parquet), [airlines.parquet](airlines.parquet), [airports.parquet](airports.parquet), [cancellation_codes.parquet](cancellation_codes.parquet)

**Temas del currículo:** Introducción al análisis de datos, manejo de datos agrupados

### 2. Estadística Descriptiva Completa
Calcular medidas de tendencia central (media, mediana, moda), dispersión (varianza, desviación estándar, coeficiente de variación), cuartiles, percentiles, valores atípicos (método IQR), asimetría y curtosis para variables clave de retrasos. Crear tablas de contingencia entre aerolíneas y categorías de retraso. Visualizar distribuciones con histogramas y box plots por aerolínea.

**Temas del currículo:** Medidas de tendencia central, medidas de dispersión, datos agrupados, rangos, frecuencias, cuartiles y percentiles, rango intercuartil, valores atípicos, teorema de Chebyshev, asimetría, curtosis, tablas de contingencia

### 3. Análisis de Probabilidad
Calcular probabilidades básicas (P(retraso), P(cancelación)), probabilidades condicionales (P(retraso llegada | retraso salida), P(cancelación | aerolínea)), aplicar reglas de adición y multiplicación. Calcular valores esperados de retraso por aerolínea y error estándar.

**Temas del currículo:** Teoría de probabilidad, probabilidad condicional, dependencia e independencia de eventos, reglas de adición y multiplicación, valor esperado, error estándar

### 4. Distribuciones de Probabilidad
Ajustar distribuciones a los datos de retrasos (normal, Poisson para llegadas/hora). Realizar pruebas de normalidad (Q-Q plots, Shapiro-Wilk). Aplicar distribución binomial para modelar probabilidad de k retrasos en n vuelos. Calcular valores z y aplicar regla empírica (68-95-99.7).

**Temas del currículo:** Variables aleatorias, distribución binomial, distribución de Poisson, distribución normal, valores z, regla empírica, aproximación normal de binomial

### 5. Inferencia Estadística Core
Construir intervalos de confianza (95%) para retraso promedio y proporción de vuelos puntuales. Realizar pruebas de hipótesis: t-tests para comparar retrasos entre aerolíneas, prueba Z para media poblacional, ANOVA para comparar múltiples aerolíneas con post-hoc tests (Tukey HSD).

**Temas del currículo:** Distribución muestral de la media, teorema del límite central, estimación de intervalo, prueba de hipótesis, errores tipo I y II, distribución T Student, ANOVA

### 6. Pruebas Chi-Cuadrada
Aplicar prueba de bondad de ajuste para verificar si los retrasos siguen distribución esperada. Realizar prueba de independencia con tabla de contingencia (día de la semana × categoría de retraso). Interpretar estadístico χ², grados de libertad y p-valores.

**Temas del currículo:** Prueba de chi cuadrada para ajuste de bondad, prueba de chi cuadrada para independencia, tablas de contingencia

### 7. Análisis de Regresión
Desarrollar regresión lineal simple (retraso llegada ~ retraso salida) y múltiple (retraso ~ distancia + hora + aerolínea). Realizar regresión logística para predecir probabilidad de retraso >15min. Analizar residuales, R², coeficientes y significancia estadística.

**Temas del currículo:** Regresión lineal simple y múltiple, regresión logística, coeficiente de correlación, covarianza, multicolinealidad

### 8. Métodos Avanzados y Machine Learning
Implementar Random Forest para clasificación de retrasos con análisis de importancia de variables. Aplicar validación cruzada y calcular métricas (accuracy, precisión, recall, AUC-ROC). Comparar con regresión logística y discutir trade-offs.

**Temas del currículo:** Métodos básicos de Machine Learning, validación de modelos

### 9. Integración y Conclusiones
Sintetizar hallazgos principales respondiendo preguntas de investigación planteadas (diferencias entre aerolíneas, patrones temporales, factores predictivos). Resumir insights estadísticos con implicaciones prácticas. Reflexionar sobre limitaciones del análisis y posibles extensiones.

**Temas del currículo:** Síntesis de análisis estadístico integral

## Consideraciones Adicionales

### 1. Enfoque Didáctico y Estructura del Notebook
Cada celda de código debe ir precedida de markdown breve explicando el objetivo, y seguida de markdown interpretando resultados en lenguaje claro. Evitar código verboso y exceso de prints; priorizar visualizaciones limpias. Minimizar uso de emojis. Crear secciones claras correspondientes a cada unidad del plan de estudios.

### 2. Preguntas de Investigación Sugeridas
- **(a)** ¿Existen diferencias significativas en retrasos entre aerolíneas principales? (ANOVA, t-tests)
- **(b)** ¿Los retrasos muestran patrones temporales? (Chi-cuadrada, regresión)
- **(c)** ¿Podemos predecir probabilidad de retraso? (regresión logística, ML)
- **(d)** ¿La distancia influye en retrasos? (correlación, regresión lineal)
- **(e)** ¿Qué factores asociados a cancelaciones? (tablas de contingencia, Chi-cuadrada independencia)

### 3. Optimización con Ibis Framework
Usar Ibis con backend DuckDB para operaciones eficientes sobre 6M filas. Realizar agregaciones, joins y filtros en Ibis antes de convertir a pandas para visualización. Aprovechar evaluación lazy para minimizar carga en memoria. 

Ejemplo de unión de tablas:
```python
flights.join(airlines, 'airline_code').join(airports.alias('origin'), flights.origin_airport == origin.airport_code)
```

### 4. Selección y Priorización de Temas
Dado el alcance, priorizar 2-3 preguntas de investigación que colectivamente cubran máximo número de temas del currículo. Asegurar cobertura de:
- Estadística descriptiva completa
- Al menos 2 pruebas de hipótesis diferentes
- Una regresión (lineal o logística)
- Una prueba Chi-cuadrada
- Un método ML básico

Balancear profundidad con amplitud.

## Cobertura del Currículo

### Unidad 1: Estadística Descriptiva ✓
- Medidas de tendencia central (media, mediana, moda)
- Medidas de dispersión (varianza, desviación estándar, rango, coeficiente de variación)
- Datos agrupados y no agrupados
- Cuartiles y percentiles
- Rango intercuartil
- Valores atípicos
- Teorema de Chebyshev
- Medidas de asimetría
- Medidas de curtosis
- Coeficiente de correlación y covarianza
- Tablas de contingencia
- Regresión lineal simple y múltiple

### Unidad 2: Probabilidad ✓
- Teoría de probabilidad
- Operaciones con conjuntos
- Reglas de adición y multiplicación
- Dependencia e independencia de eventos
- Probabilidad condicional
- Valor esperado
- Error estándar

### Unidad 3: Distribuciones de Probabilidad ✓
- Variables aleatorias
- Distribución binomial
- Distribución de Poisson
- Distribución normal
- Valores z
- Regla empírica
- Aproximación normal de una distribución binomial

### Unidad 4: Estadística Inferencial ✓
- Distribución muestral de la media
- Teorema del límite central
- Estimación de intervalo
- Prueba de hipótesis
- Errores tipo I y II
- Distribución T Student
- Prueba de chi cuadrada (bondad de ajuste e independencia)
- Análisis de varianza (ANOVA)
- Regresión lineal y logística
- Métodos básicos de Machine Learning

## Estructura del Dataset

### Tablas Principales

**flights.parquet** (~6 millones de registros)
- Dataset principal con detalles de vuelos
- Columnas esperadas: fecha, código aerolínea, número de vuelo, aeropuertos origen/destino, tiempos salida/llegada, retrasos (salida/llegada), estado cancelación, distancia

**airlines.parquet**
- Tabla de referencia de aerolíneas
- Columnas: código aerolínea, nombre aerolínea

**airports.parquet**
- Tabla de referencia de aeropuertos
- Columnas: código aeropuerto, nombre, ciudad, estado, latitud, longitud, altitud

**cancellation_codes.parquet**
- Códigos de razón de cancelación
- Columnas: código cancelación, descripción
- Categorías típicas: clima, aerolínea, NAS, seguridad

### Relaciones entre Tablas
```
flights.parquet
├── airline_code → airlines.parquet (airline_code)
├── origin_airport → airports.parquet (airport_code)
├── dest_airport → airports.parquet (airport_code)
└── cancellation_code → cancellation_codes.parquet (code)
```

## Stack Técnico

**Procesamiento de Datos:**
- Ibis Framework (backend DuckDB) para operaciones sobre 6M filas
- Pandas/Polars para análisis final y visualización

**Análisis Estadístico:**
- statsmodels: regresión, ANOVA, pruebas de hipótesis
- scipy.stats: distribuciones de probabilidad, pruebas estadísticas
- sklearn: machine learning, clasificación, validación cruzada

**Visualización:**
- matplotlib: gráficas fundamentales
- seaborn: visualizaciones estadísticas
- plotly (opcional): dashboards interactivos

**Entorno:**
- Python 3.13
- Jupyter Notebook para análisis narrativo
- Dependencias ya configuradas en pyproject.toml
