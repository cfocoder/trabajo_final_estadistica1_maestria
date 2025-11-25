---
theme: penguin
layout: intro
title: Análisis Estadístico de Retrasos en Vuelos
subtitle: De la Estadística Descriptiva al Modelado Predictivo
author: Héctor Gabriel Sánchez Pérez
date: 2025-11-25
---

# Análisis Estadístico de Retrasos en Vuelos

## Proyecto Final - Métodos Estadísticos Básicos

<div class="absolute bottom-10 left-10 opacity-80">
  <span class="font-bold">Dataset:</span> Airline Flight Delays (~6M registros)
</div>

---
layout: text-image
media: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&auto=format&fit=crop&w=1353&q=80
caption: "¿Por qué se retrasan los vuelos?"
---

# Introducción y Problema

Los retrasos aéreos generan pérdidas millonarias y frustración.

### Objetivos
1.  **Identificar** qué aerolíneas y días son más propensos a retrasos.
2.  **Analizar** si los retrasos siguen una distribución normal.
3.  **Predecir** retrasos de llegada basados en datos de salida.

### Tecnología: Ibis Framework
Para manejar **5.7 millones de registros** eficientemente, utilizamos **Ibis** con **DuckDB**, permitiendo evaluación perezosa (Lazy Evaluation) y gestión de memoria "out-of-core".

---
layout: default
---

# Descripción de los Datos

El dataset "Airline Flight Delays" de Maven Analytics contiene información detallada de vuelos en EE.UU.

<div class="grid grid-cols-2 gap-4 mt-10">

<div class="border-l-4 border-blue-500 pl-4">
  <h3 class="text-xl font-bold mb-2">Volumen</h3>
  <p class="text-4xl font-mono text-blue-600">5,732,926</p>
  <p class="text-gray-500">Vuelos Totales</p>
</div>

<div class="border-l-4 border-green-500 pl-4">
  <h3 class="text-xl font-bold mb-2">Variables Clave</h3>
  <ul class="list-disc pl-5 space-y-1">
    <li><strong>Numéricas:</strong> Retrasos (Salida/Llegada), Distancia.</li>
    <li><strong>Categóricas:</strong> Aerolínea, Aeropuerto, Día, Motivo Cancelación.</li>
  </ul>
</div>

</div>

<!-- Mermaid Diagram for Data Flow -->
<div class="mt-10 flex justify-center">
```mermaid
graph LR
    A[Parquet Files] --> B[Ibis Connection]
    B --> C[DuckDB Engine]
    C --> D[Análisis Estadístico]
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style C fill:#bbf,stroke:#333,stroke-width:2px
```
</div>

---
layout: default
---

# Estadística Descriptiva: ¿Es Normal?

Analizamos la forma de la distribución de los retrasos de salida.

<div class="grid grid-cols-2 gap-4">
  <div>
    <img src="/images/distribucion_retrasos.png" class="rounded shadow-lg h-80 object-contain" />
  </div>
  <div class="flex flex-col justify-center">
    <ul class="space-y-4">
      <li>
        <strong>Tendencia Central:</strong>
        <br/>Media: 9.37 min | Mediana: -2.0 min
        <br/><span class="text-sm text-gray-500">La mayoría sale a tiempo, pero el promedio es alto.</span>
      </li>
      <li>
        <strong>Forma (No Normal):</strong>
        <br/>Asimetría: 7.59 (Cola derecha larga)
        <br/>Curtosis: 123.0 (Colas pesadas)
      </li>
      <li>
        <strong>Outliers:</strong>
        <br/>12.8% de los vuelos son valores atípicos extremos.
      </li>
    </ul>
  </div>
</div>

---
layout: default
---

# Probabilidad y Dependencia

Calculamos probabilidades básicas y condicionales.

<div class="grid grid-cols-3 gap-4 mt-8 text-center">
  <div class="bg-gray-100 p-4 rounded">
    <h3 class="font-bold text-lg">P(Retraso)</h3>
    <p class="text-3xl text-red-500">37.1%</p>
    <p class="text-xs">Probabilidad de salir tarde</p>
  </div>
  <div class="bg-gray-100 p-4 rounded">
    <h3 class="font-bold text-lg">P(A Tiempo)</h3>
    <p class="text-3xl text-green-500">62.9%</p>
    <p class="text-xs">Probabilidad de salir puntual</p>
  </div>
  <div class="bg-gray-100 p-4 rounded">
    <h3 class="font-bold text-lg">Condicional</h3>
    <p class="text-3xl text-blue-500">71.3%</p>
    <p class="text-xs">P(Llegada Tarde | Salida Tarde)</p>
  </div>
</div>

<div class="mt-8 border-t pt-4">
  <h3 class="text-xl font-bold mb-2">Teorema de Bayes & Independencia</h3>
  <p>La prueba de independencia muestra que los retrasos de salida y llegada son <strong>altamente dependientes</strong>.</p>
  <p class="italic text-gray-600 mt-2">"Si sales tarde, es muy probable que llegues tarde. Recuperar tiempo en el aire es un mito."</p>
</div>

---
layout: default
---

# Comparación de Aerolíneas (Inferencia)

¿Existen diferencias significativas entre aerolíneas?

<div class="grid grid-cols-2 gap-4">
  <div class="flex flex-col justify-center">
    <h3 class="font-bold text-xl mb-4">Pruebas de Hipótesis</h3>
    <ul class="space-y-4">
      <li>
        <strong>T-Test (Spirit vs United):</strong>
        <br/>$p \approx 0$. Diferencia significativa.
        <br/>Spirit (15.9 min) > United (14.4 min).
      </li>
      <li>
        <strong>ANOVA (Top 5):</strong>
        <br/>$F \approx 1441, p \approx 0$.
        <br/>Existen diferencias significativas entre todas las grandes aerolíneas.
      </li>
    </ul>
  </div>
  <div>
    <img src="/images/retraso_aerolineas.png" class="rounded shadow-lg h-80 object-contain" />
  </div>
</div>

---
layout: default
---

# Independencia de Categorías

¿La severidad del retraso depende de la aerolínea?

<div class="flex justify-center mb-4">
  <img src="/images/heatmap_categorias.png" class="rounded shadow-lg h-80 object-contain" />
</div>

*   **Prueba Chi-Cuadrada:** $\chi^2 \approx 24,913, p \approx 0$.
*   **Conclusión:** Las categorías de retraso **NO** son independientes de la aerolínea.
*   **Insight:** United tiene más retrasos leves, mientras Spirit tiene más retrasos severos.

---
layout: default
---

# Patrones Temporales

¿Qué día es peor para volar?

<div class="grid grid-cols-2 gap-4">
  <div>
    <img src="/images/retraso_dias_semana.png" class="rounded shadow-lg h-80 object-contain" />
  </div>
  <div class="flex flex-col justify-center">
    <div class="bg-red-50 p-4 rounded mb-4 border-l-4 border-red-500">
      <h3 class="font-bold text-red-700">Peor Día: Viernes</h3>
      <p>Mayor probabilidad de retraso y mayor retraso promedio.</p>
    </div>
    <div class="bg-green-50 p-4 rounded border-l-4 border-green-500">
      <h3 class="font-bold text-green-700">Mejor Día: Martes</h3>
      <p>Menor probabilidad de incidencias.</p>
    </div>
  </div>
</div>

---
layout: default
---

# Modelado Predictivo: Regresión Lineal

Prediciendo el retraso de llegada ($Y$) basado en la salida ($X$).

<div class="grid grid-cols-2 gap-4">
  <div class="flex flex-col justify-center">
    <div class="text-2xl font-mono bg-gray-800 text-white p-4 rounded mb-4">
      Y = -4.94 + 1.006X
    </div>
    <ul class="space-y-2">
      <li><strong>$R^2$:</strong> 0.892 (Muy alto)</li>
      <li><strong>Interpretación:</strong> Relación casi 1 a 1.</li>
      <li><strong>Intercepto (-4.94):</strong> Pequeña recuperación de tiempo en vuelo promedio.</li>
    </ul>
  </div>
  <div>
    <img src="/images/scatter_correlacion.png" class="rounded shadow-lg h-80 object-contain" />
  </div>
</div>

---
layout: default
---

# Regresión Logística: Un Experimento Fallido

Intentamos predecir "Retraso Significativo (>15min)" usando solo la **Distancia**.

<div class="grid grid-cols-2 gap-8 mt-10">
  <div class="text-center">
    <h3 class="text-xl font-bold text-red-600">Resultado</h3>
    <p class="text-6xl font-bold mt-4">Recall = 0%</p>
    <p class="text-gray-500 mt-2">Para la clase "Con Retraso"</p>
  </div>
  <div>
    <h3 class="font-bold mb-2">¿Por qué falló?</h3>
    <ul class="list-disc pl-5 space-y-2">
      <li>El modelo predijo "Sin Retraso" para <strong>todos</strong> los vuelos.</li>
      <li>La <strong>Distancia</strong> por sí sola no causa retrasos.</li>
      <li><strong>Lección:</strong> La "Accuracy" (82%) es engañosa en clases desbalanceadas. Se necesitan más variables (Clima, Tráfico).</li>
    </ul>
  </div>
</div>

---
layout: center
class: text-center
---

# Conclusiones

1.  **Distribución:** Los retrasos no son normales; son eventos extremos en una operación mayormente puntual.
2.  **Elección:** La aerolínea y el día de la semana (Martes vs Viernes) afectan significativamente tu probabilidad de retraso.
3.  **Predicción:** Si sales tarde, llegarás tarde. No cuentes con recuperar tiempo en el aire.

<div class="mt-10 text-gray-500">
  Gracias por su atención
</div>
