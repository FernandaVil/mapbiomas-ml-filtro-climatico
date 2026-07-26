# Prototipo de Filtro Temporal de Nueva Generación para MapBiomas Argentina 🇦🇷

**Corrección de ruido óptico por estrés hídrico mediante Machine Learning y datos climáticos ERA5.**

Este repositorio contiene el código fuente y el flujo de trabajo analítico presentado para el **Premio MapBiomas Argentina 2026**. El proyecto propone una evolución a los filtros temporales de post-procesamiento actuales, integrando inteligencia artificial y reanálisis climático para corregir transiciones espurias provocadas por anomalías climáticas extremas (como la sequía de 2020 en el Gran Chaco).

## 🗂️ Estructura del Proyecto

El flujo de trabajo está dividido en 4 cuadernos de Jupyter (*Notebooks*) secuenciales para garantizar su total reproducibilidad:

1. **`01_extraccion_datos_gee.ipynb`**: Conexión a la API de Google Earth Engine (GEE). Extracción de coberturas de MapBiomas (Colección 2) y datos climáticos de temperatura y precipitación (ERA5-Land) para el Gran Chaco durante la sequía histórica de 2020.
2. **`02_preprocesamiento_etiquetado.ipynb`**: Aplicación de la lógica de ventana móvil (2019-2020-2021) en la nube. Ejecución de un muestreo estratificado in situ para extraer una muestra perfectamente balanceada de píxeles estables y espurios, optimizando los costos computacionales.
3. **`03_entrenamiento_modelo_ml.ipynb`**: Entrenamiento de un modelo `RandomForestClassifier` (scikit-learn). Evaluación de métricas de precisión (F1-Score: 0.79) y análisis de importancia de variables climáticas en la detección del ruido óptico.
4. **`04_visualizacion_resultados.ipynb`**: Traducción del modelo algorítmico a la nube usando `geemap`. Despliegue interactivo del filtro espacial y visualización del "antes y después" de la cobertura del suelo a escala regional y local.

## Instalación y reproducibilidad

El proyecto fue diseñado para ejecutarse íntegramente en la nube apoyándose en el catálogo de Google Earth Engine, eliminando la necesidad de descargar rasteres pesados localmente.

### Prerrequisitos
- Python 3.8 o superior.
- Una cuenta activa en [Google Earth Engine](https://earthengine.google.com/).

### Pasos para ejecutar localmente

1. Clona este repositorio:
   ```bash
   git clone [https://github.com/FernandaVil/mapbiomas-ml-filtro-climatico.git](https://github.com/FernandaVil/mapbiomas-ml-filtro-climatico.git)
   cd mapbiomas-ml-filtro-climatico
   ```
2. Instala las dependencias necesarias:
    ```bash
    pip install -r requirements.txt
    ```
3. Autenticación en Earth Engine:
    Al ejecutar el primer cuaderno, el entorno solicitará autenticación en los servidores de Google. Sigue el enlace generado por `ee.Authenticate()` para habilitar el acceso a los catálogos públicos.

### Resultados Destacados
El modelo logró identificar espacialmente la huella de la sequía de 2020 sobre las coberturas agropastoriles y humedales del Gran Chaco. Al aplicar el filtro inteligente, se corrigió el 17.53% del área de estudio, lo que representa una recuperación cartográfica de 579.616 hectáreas que habían sido afectadas por ruido óptico derivado del estrés fisiológico de la vegetación.
