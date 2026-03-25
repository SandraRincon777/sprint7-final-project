# sprint7-final-project
el objetivo del proyecto: El objetivo es evaluar el comportamiento de los clientes de Connecta Tel, una empresa de telecomunicaciones en Latinoamerica, utilizando datos registrados hasta el ano 2024

los datasets utilizados: 
-Plans.CSV (plan_name	messages_included	gb_per_month	minutes_included	usd_monthly_pay	usd_per_gb	usd_per_message	usd_per_minute) 2 filas 
-Users_latam.csv (user_id	first_name	last_name	age	city	reg_date	plan	churn_date	) 4000 filas 
-Usage.csv (id	user_id	type	date	duration	length	) 40000 filas 

las etapas del análisis realizadas,
Paso 1 — Carga y Exploración Inicial
•	Importación de librerías: pandas, matplotlib, seaborn.
•	Carga de los tres datasets desde /datasets/ con pd.read_csv().
•	Revisión de primeras filas (.head()), dimensiones (.shape) y estructura (.info()).
Paso 2 — Identificación de Problemas de Calidad
•	Valores nulos: conteo y proporción por columna (.isna().sum() y .isna().mean()).
•	Valores inválidos (sentinels): detección de -999 en age y '?' en city.
•	Revisión de fechas: conversión a datetime y verificación de años fuera de rango.
Paso 3 — Limpieza de Datos
•	Reemplazo de sentinel -999 en age por la mediana del campo.
•	Reemplazo de '?' en city por pd.NA.
•	Marcado de fechas futuras (año > 2024) en reg_date como NaT.
•	Verificación de nulos MAR (Missing At Random) en duration y length de usage.
Paso 4 — Métricas de Uso por Usuario
•	Creación de columnas auxiliares: is_text, is_call.
•	Agrupación por user_id: cant_mensajes, cant_llamadas, cant_minutos_llamadas.
•	Merge del dataset agregado con users para crear user_profile.
•	Resumen estadístico y distribución porcentual por plan.
Paso 5 — Visualización y Detección de Outliers
•	Histogramas de age, cant_mensajes, cant_llamadas, cant_minutos_llamadas con hue=plan.
•	Boxplots para visualización de outliers en las mismas variables.
•	Cálculo de límites mediante método IQR para cuantificar valores extremos.
•	Decisión de mantener outliers identificados como comportamiento real (heavy users).
Paso 6 — Segmentación de Clientes
•	grupo_uso: clasificación en Bajo uso, Uso medio, Alto uso según llamadas y mensajes.
•	grupo_edad: clasificación en Joven (<30), Adulto (30–59), Adulto Mayor (60+).
•	Visualización de ambas segmentaciones con gráficos de conteo (countplot).
Paso 7 — Insight Ejecutivo
•	Diagnóstico de problemas de datos con porcentajes de afectación.
•	Análisis de segmentos por comportamiento y valor para el negocio.
•	Identificación de patrones extremos y sus implicaciones comerciales.
•	Recomendaciones accionables para mejora de planes y retención de clientes.

cómo ejecutar el notebook :
 Google Colab (Recomendado)
1.	Abre Google Colab: https://colab.research.google.com
2.	Ve a File → Upload notebook y selecciona el archivo .ipynb.
3.	Sube los archivos CSV: en el panel izquierdo, carpeta Files, arrastra plans.csv, users_latam.csv y usage.csv a la carpeta /datasets/.
4.	Ejecuta todas las celdas: Runtime → Run all.

una breve guía de reproducción.
•	Los archivos CSV deben estar exactamente en /datasets/ relativo al notebook.
•	El notebook debe ejecutarse en orden secuencial — cada paso depende del anterior.
•	En Google Colab, los archivos cargados se pierden al cerrar la sesión; vuelve a subirlos si es necesario.
•	Si ejecutas localmente, asegúrate de que el kernel de Jupyter apunte a tu entorno con las dependencias instaladas.
