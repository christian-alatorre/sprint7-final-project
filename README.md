### sprint7-final-project

# **Análisis de la empresa de telecomunicaciones ConnectaTel**

En el presente documento se describe lo siguiente:
Objetivo del proyecto
Datasets utilizados
Etapas realizadas en el análisis
Cómo ejecutar el notebook
Guía de reproducción

## Objetivo del proyecto

Analizar el comportamiento de los usuarios de ConnectaTel para responder cuatro preguntas de negocio:

¿Qué patrones de uso (llamadas y mensajes) existen entre los clientes?
¿Hay usuarios con consumo atípico (outliers)?
¿Cómo varía el uso según la edad y el plan?
¿Qué ideas pueden mejorar la oferta actual de planes o dar lugar a nuevos planes?

## Datasets utilizados

plans.csv   ⟶ 	Información de los planes que ofrece la empresa.
users_latam.csv   ⟶ 	4,000 registros de usuarios: edad, ciudad, fecha de registro, plan y fecha de baja (churn date).
usage.csv   ⟶ 	40,000 registros de actividad: llamadas y mensajes, con fecha y duración.

## Etapas realizadas en el análisis

1. Carga y exploración: lectura y revisión de estructura de los tres datasets utilizados.

2. Identificación de problemas de calidad de datos: valores nulos, sentinels ("-999", "?") y fechas fuera de rango ("2026").

3. Limpieza básica de datos: reemplazo de edades inválidas por la mediana, manejo de ciudades y fechas inválidas, y análisis de nulos estructurales en usage.

4. Sumarización de estadísticas descriptivas: agregación de actividad por usuario (mensajes, llamadas y minutos) y creación del perfil de usuario (user_profile).

5. Visualización y outliers: Análisis por medio de histogramas, boxplots y detección de outliers con el método IQR; Se tomó la decisión de mantenerlos.

6. Visualización de segmentación de clientes: grupos por nivel de uso (bajo uso, uso medio, alto uso) y por edad (joven, adulto, adulto Mayor), con sus respectivas visualizaciones.

7. Insight ejecutivo: conclusiones y recomendaciones para los stakeholders.


## Cómo ejecutar el notebook

1. Asegúrate de tener instaladas las siguientes librerías de Python:
* Pandas: para cargar, limpiar y analizar los datos.
* Seaborn y matplotlib: para crear los gráficos.
* Jupyter Notebook: para abrir y ejecutar el notebook.

2. Coloca los tres archivos CSV en la carpeta "datasets" (el notebook los lee desde /datasets/plans.csv, /datasets/users_latam.csv y /datasets/usage.csv). Si trabajas fuera de la plataforma del curso, ajusta esas rutas).

3. Abre el notebook con jupyter notebook.

4. Ejecuta todas las celdas en orden con Kernel > Restart Kernel and Run All Cells.

## Guía de reproducción

Para obtener los mismos resultados que aparecen en el documento cargado, sigue este orden:

1. Carga: importa pandas, seaborn y matplotlib.pyplot, y explora los tres datasets.

2. Limpieza: reemplaza "-999" en age por la mediana, convierte "?" en city a nulo, convierte las fechas con pd.to_datetime(errors='coerce') y marca como NaT las fechas de registro posteriores a 2024.

3. Agregación: cuenta mensajes y llamadas y suma los minutos por usuario, después únelos a users con un merge(how='left') para crear la columna user_profile.

4. Outliers: calcula el límite superior con el método IQR (Q3 + 1.5 * IQR) para las columnas cant_mensajes, cant_llamadas y cant_minutos_llamada.

5. Segmentación: crea categorías "grupo_uso" (bajo uso, uso medio, alto uso) y "grupo_edad" (joven, adulto, adulto mayor) con comparaciones lógicas.
