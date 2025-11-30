# 🏎️ F1 Sustainable Logistics: Optimización de Calendario con Algoritmo Genetico

**Autor:** Jaime Arias
**Rol:** Supply Chain Analyst & Python Developer
**Tecnologías:** Python, Pandas, Folium, Plotly, Genetic Algorithms.

---

## 1. Definición del Problema (Business Case)

### El Reto
La Fórmula 1 es un "circo logístico" global que mueve miles de toneladas de equipamiento y personal a través de 24 sedes en 5 continentes en solo 9 meses. El problema central es la ineficiencia de las rutas heredadas, que a menudo implican saltos transatlánticos redundantes ("rutas espagueti"), aumentando drásticamente los costos operativos y la huella de carbono.

### El Objetivo
Desarrollar un modelo matemático capaz de proponer un calendario alternativo que:
* **Minimice la distancia total** de viaje (ahorro de combustible y costos).
* **Respete restricciones climáticas** estrictas (evitar monzones en Asia o nieve en Canadá).
* **Cumpla reglas comerciales** innegociables (Inicio en Australia, Fin en Abu Dhabi).

Este no es un simple problema de "Viajante de Comercio" (TSP), es un **TSP con Ventanas de Tiempo (TSPTW) y Restricciones de Anclaje**, lo que eleva exponencialmente su complejidad ($22!$ combinaciones).

---

## 2. El Marco Operacional: Restricciones Duras y Suaves

Para simular la realidad de una planificación logística, el modelo obedece reglas de negocio complejas clasificadas en un **Modelo de Semáforo de Riesgo**:

### 🟢 Zona Verde (Ideal)
* **Condición:** Desviación de fecha $\le 7$ días.
* **Penalización:** $0.
* **Significado:** Operación estándar en ventana climática óptima.

### 🟡 Zona Amarilla (Gestión de Riesgo)
* **Condición:** Desviación entre 8 y 45 días.
* **Penalización:** **$2.500.000 USD** (Costo de Mitigación).
* **Significado:** La IA tiene "permiso" para negociar. Si mover una carrera ahorra $5M en aviones pero cae en una fecha de mucho calor, el modelo paga la multa de $2.5M (aire acondicionado extra, logística nocturna) y aprueba la ruta porque el ahorro neto es positivo.

### 🔴 Zona Roja (Nuclear)
* **Condición:** Desviación $> 45$ días.
* **Penalización:** **$100.000.000 USD**.
* **Significado:** Restricción dura (Nieve/Huracanes). El costo se vuelve infinito para forzar el descarte de la ruta.

---

## 3. Resultados: Impacto Financiero y Sostenible

El algoritmo se sometió a un **Análisis de Robustez (5 iteraciones)** para garantizar estabilidad. La solución seleccionada logró eliminar los cruces oceánicos redundantes.

| KPI Logístico | Calendario Oficial | Propuesta IA | Ahorro / Mejora |
| :--- | :--- | :--- | :--- |
| **Distancia** | 114,521 km | **99,534 km** | 📉 **13.1%** |
| **Costo Operativo** | $29.8M USD | **$25.9M USD** | 💰 **$3.9M USD** |
| **Huella CO2** | 81,908 t | **66,739 t** | 🌿 **15,169 Tons** |
| **Lead Time** | 128 Días | **117 Días** | ⏱️ **11 Días Libres** |

> *Nota: El Costo Operativo incluye estimación de Jet Fuel y Overhead logístico ($250/km).*

---

## 4. Anatomía del Código (Arquitectura)

El proyecto utiliza una arquitectura modular Orientada a Objetos (OOP) para escalabilidad:

1.  **Gestión de Datos (`class F1LogisticsData`):** Carga dinámica de CSVs y anclas geográficas.
2.  **Motor de Optimización (`class SustainableOptimizer`):** Implementa el Algoritmo Genético con *Early Stopping* (Paciencia=150) para eficiencia computacional.
3.  **Visualización (`class LogisticsVisualizer`):** Genera dashboards interactivos con **Plotly** y mapas geoespaciales con **Folium**.

### Entregables Generados
El script produce automáticamente en la carpeta `outputs/`:
* 📊 `dashboard_ejecutivo.html`: Reporte interactivo para stakeholders.
* 🗺️ `mapa_comparativo_dual.html`: Visualización del "Antes vs. Después".

---

## 5. Aplicación Industrial

Este modelo es agnóstico y transferible a otras industrias:
* **Giras de Eventos:** Optimización de estadios mundiales.
* **Logística Naviera:** Rutas de buques con ventanas de entrega.
* **Retail Global:** Distribución de cadena de suministro.

---
*Desarrollado como caso de estudio de Investigación de Operaciones aplicada a Negocios.*