# Telecom X — Análisis de Evasión de Clientes (Churn)

Proyecto del Challenge ONE (Alura Latam / Oracle Next Education) enfocado en aplicar un flujo ETL (Extract, Transform, Load) y realizar un Análisis Exploratorio de Datos (EDA) sobre una base de clientes de una empresa de telecomunicaciones, con el objetivo de comprender patrones asociados a la evasión (Churn) y dejar los datos listos para el equipo de Data Science.

Este proyecto extrae los datos desde una API en formato JSON, los normaliza para convertirlos a un DataFrame, realiza limpieza y tratamiento de inconsistencias (tipos de datos, valores vacíos y conversiones numéricas), y finalmente genera métricas descriptivas, visualizaciones e insights que ayudan a interpretar el fenómeno de churn.

Datos: los registros se consumen desde un JSON público (raw GitHub) y se transforman a un DataFrame con pandas.json_normalize(). El tamaño inicial es cercano a 7267 filas y 21 columnas; para el análisis final se removieron registros con churn vacío, quedando 7043 filas.

Tecnologías: Python 3, Pandas, NumPy, Matplotlib y Requests.

ETL y tratamiento (resumen): (1) Extract: consumo del JSON con requests.get() y validación de respuesta; normalización con pd.json_normalize(). (2) Transform: inspección de estructura con df.info(), df.dtypes, df.isna().sum() y valores únicos; estandarización de nombres de columnas; detección y corrección de valores vacíos en Churn ('' → NaN) y eliminación de registros sin churn para mantener consistencia del objetivo; conversión de account_Charges_Total a numérico con pd.to_numeric(errors='coerce') y tratamiento de NaN; verificación de duplicados; creación de variable opcional Cuentas_Diarias = account_Charges_Monthly / 30 para análisis a nivel diario. (3) Load & Analysis: estadísticas descriptivas con describe(), análisis de distribución de churn y comparaciones por variables numéricas/categóricas.

Principales resultados e insights: la distribución de churn observada es aproximadamente No = 73.46% y Yes = 26.54%. En variables numéricas, se observa una concentración de churn en clientes con menor antigüedad (tenure), es decir, evasión temprana. En el extra de correlación (con Churn_bin), la variable con mayor correlación absoluta fue customer_tenure (~0.35), seguida por variables monetarias como account_Charges_Total y account_Charges_Monthly/Cuentas_Diarias con correlaciones moderadas, lo cual sugiere que el tiempo de permanencia es un factor clave para explicar la evasión.

Visualizaciones incluidas en el notebook: gráfico de barras para la distribución de churn (Yes/No), histogramas comparativos de tenure según churn y un ranking de correlaciones con churn binario (extra), además de otras visualizaciones exploratorias según el análisis.

Estructura del repositorio: contiene el notebook principal (.ipynb) con todo el flujo (extracción, transformación, análisis y el informe final) y este README.md.

Cómo ejecutar: abrir el notebook en Google Colab o Jupyter y ejecutar las celdas en orden (Extract → Transform → Load/EDA → Informe final). Si se ejecuta localmente: pip install pandas numpy matplotlib requests.

Conclusión: el análisis muestra que la evasión ocurre principalmente al inicio de la relación con el cliente (tenure bajo). Esto permite orientar estrategias de retención temprana (onboarding, acompañamiento inicial, ofertas/beneficios en los primeros meses) y entrega un dataset tratado listo para modelado predictivo.

