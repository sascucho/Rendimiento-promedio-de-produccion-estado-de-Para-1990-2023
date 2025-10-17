# 📈 Análisis de Series Temporales: Rendimiento Medio y Volatilidad de Cultivos

## 📌 Introducción

Este proyecto de Ciencia de Datos se enfoca en el análisis de una serie temporal de datos agrícolas para evaluar el **Rendimiento Medio** histórico y la **Volatilidad (Variabilidad)** de diferentes cultivos.

El principal desafío fue la **ingesta y limpieza de un archivo Excel** con un formato de reporte no estructurado (datos no tabulares, múltiples encabezados y caracteres especiales) para transformarlo en un *dataset* numérico apto para el análisis estadístico y la visualización interactiva.

---

## 🛠️ Metodología y Herramientas

### 1. Herramientas y Librerías

| Componente | Uso Principal |
| :--- | :--- |
| **Entorno** | Google Colab |
| **Lenguaje** | Python |
| **Pandas** | Ingesta, Limpieza, Transformación, y Análisis Estadístico. |
| **openpyxl** | Manejo de archivos Excel para escritura en múltiples hojas. |
| **Altair** | Creación de visualizaciones interactivas y dinámicas. |

### 2. Diagrama de Flujo del Proceso

El siguiente diagrama ilustra el flujo de trabajo integral desde la ingesta de los datos crudos hasta la generación de los informes finales y las visualizaciones interactivas.

<img width="1280" height="3304" alt="Untitled diagram-2025-10-17-023308" src="https://github.com/user-attachments/assets/010145a7-c5c0-4f83-b1c8-6dc6b42e1808" />

---

## ⚙️ Flujo de Trabajo del Algoritmo (Detalle)

El script se estructura en cuatro fases principales que garantizan la calidad del dato y la extracción de valor analítico:

### 1. Ingesta y Limpieza de Datos Crudos

La fase inicial maneja la complejidad del archivo Excel, cargando solo el rango relevante de la tabla y aislando los metadatos:

* **Carga Específica:** Se utiliza `pd.read_excel` con `skiprows` y `usecols` para cargar la tabla de datos obviando encabezados y metadatos irrelevantes.
* **Aislamiento de Metadatos:** La primera columna se establece como el **índice (`Año`)**, y la primera fila se extrae para ser el **encabezado** de los cultivos en el DataFrame final.
* **Normalización de Nulos:** Los caracteres de reporte no numéricos (`...`, `..`, `-`) son reemplazados explícitamente por **'0'** para su posterior conversión.

### 2. Transformación y Sanidad Numérica

Esta es la fase crítica donde el *dataset* se convierte completamente a valores numéricos:

* **Coerción de Tipos:** Se aplica `pd.to_numeric(errors='coerce')`. Esta función convierte el texto a números y transforma cualquier valor que no pudo convertirse (incluyendo texto residual) a **`NaN`** (Not a Number).
* **Filtrado de Columna:** Se eliminan las columnas donde **todos los valores son `NaN`** (columnas que originalmente no contenían datos numéricos).
* **Imputación Final:** Cualquier `NaN` restante se rellena con **`0`** (`fillna(0)`), asumiendo un valor nulo de rendimiento.
* **Descarte por Cero:** Se eliminan las columnas donde la suma total de valores es **cero**, eliminando cultivos sin registro histórico de rendimiento.

### 3. Análisis Estadístico y Generación de Reportes

Se extraen dos métricas clave de la serie histórica y se guardan en un archivo Excel con múltiples hojas:

* **Clasificación por Rendimiento (Último Año):** Se calcula y ordena el rendimiento para el **último año disponible** para identificar los cultivos de mayor rendimiento reciente.
* **Variabilidad Histórica:** Se calcula la **Desviación Estándar (`std()`)** por cultivo. Esta métrica es crucial para identificar los cultivos más inestables o volátiles a lo largo del periodo, un riesgo clave para la planificación agrícola.
* **Almacenamiento:** Ambos reportes se guardan en el archivo `Clasificación_cultivos_último_año.xlsx` en hojas separadas usando `pd.ExcelWriter(mode='a')`.

### 4. Visualización Interactiva (Altair)

Se generan gráficos dinámicos para facilitar la exploración y la toma de decisiones:

* **Evolución Temporal:** Un gráfico de líneas interactivo permite al usuario seleccionar un cultivo mediante un menú desplegable (`alt.binding_select`) para visualizar su serie temporal de rendimiento medio de forma aislada.
* **Top 10 Rendimiento:** Un gráfico de barras apiladas que muestra la contribución anual de los 10 cultivos con el mayor rendimiento histórico promedio.

***

## 👨‍💻 Autor

| Detalle | Información |
| :--- | :--- |
| **Integrantes** | Laura Alvis
Juan Bohorquez
Andres Niño
Michell Sanchez|
| **Materia** | Ciencia de Datos |
| **Profesor** | [Oscar Vargas] |
| **Institución** | [Universidad Santo Tomas] |
| **Año** | 2025 |
---

## 💾 Resultados y Acceso

El código fuente, los resultados estadísticos y la metodología detallada se encuentran en:

* [**`Análisis_Pará.ipynb`**](Análisis_Pará.ipynb)
