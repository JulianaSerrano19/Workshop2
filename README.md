# Workshop 2: Automatización de un Pipeline ETL 
**Estudiante:** Juliana Toro Serrano 
**Curso:** ETL (Ingeniería de Datos e Inteligencia Artificial) 
**Institución:** Universidad Autónoma de Occidente


## Descripción General del Proyecto
El objetivo de este taller es diseñar e implementar un pipeline ETL (Extracción, Transformación y Carga) automatizado que integra dos fuentes de datos diferentes: un archivo CSV con información de **Spotify** y una base de datos relacional con los premios **Grammy**. El proyecto incluye validaciones de calidad de datos, normalización de campos, uniones (*merge*), almacenamiento local y la generación de un reporte estático analítico consultado estrictamente desde la base de datos.


## Flujo del Pipeline y Orquestación (Apache Airflow)
El flujo de trabajo se estructura mediante un grafo acíclico dirigido (DAG) con dos ramas de extracción paralelas que convergen en un procesamiento central:

1. **`read_csv` y `transform_csv`:** Extracción del dataset de Spotify y aplicación de un esquema de validación de calidad de datos utilizando `pandera` (verificando tipos de datos, rangos de popularidad y manejo de nulos).
2. **`read_db` y `transform_db`:** Extracción y carga inicial del dataset de los Premios Grammy en una base de datos relacional SQLite (`workshop.db`).
3. **`merge`:** Cruce de ambas fuentes utilizando una llave común normalizada (`artist_clean`), consolidando un total de 23,944 registros cruzados.
4. **`load`:** Almacenamiento del dataset combinado final de vuelta en la base de datos relacional (`final_merged_data`).
5. **`store`:** Exportación del dataset transformado como un archivo CSV local (`transformed_dataset.csv`)[cite: 8, 13, 15].


## Reporte Estático
Como parte final del taller, se diseñó un reporte gráfico (Top 10 de artistas con mayor cantidad de registros combinados) que se alimenta **exclusivamente de la base de datos relacional** (`final_merged_data`) y no del archivo CSV plano, cumpliendo con los requerimientos de la práctica.


## Tecnologías y Librerías Utilizadas
* **Python**
* **Google Colab / Jupyter Notebook**
* **Pandas & Pandera** (Manipulación y validación estricta de calidad de datos)
* **SQLite & SQLAlchemy** (Gestión de base de datos relacional)
* **Apache Airflow** (Diseño conceptual y orquestación del DAG)
* **Matplotlib** 


## Estructura del Repositorio
* `Workshop_2.ipynb`: Cuaderno principal con la implementación completa del código, validaciones, consultas SQL y DAG de referencia.
* `transformed_dataset.csv`: Archivo CSV final resultante del proceso ETL.
* `static_report.png`: Imagen del reporte estático generado en alta resolución.
* `workshop.db`: Base de datos SQLite local con las tablas intermedias y finales.
