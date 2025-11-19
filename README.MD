🚕 NYC Taxi – Procesamiento de Viajes (CPrueba Tecnica Simon Movilidad)

Este repositorio contiene un script en Python que procesa un archivo de viajes en formato Parquet (similar al dataset de NYC Taxi) y genera dos reportes solicitados:

ultima_ubicacion.csv → Última ubicación conocida por vehículo.

viajes_por_hora.csv → Total de viajes iniciados por hora del día (0–23).

El objetivo es demostrar un pipeline simple, claro y reproducible, transformando un dataset crudo en salidas analíticas útiles.

1. Herramientas utilizadas

Python 3.x

pandas (procesamiento tabular)

numpy (generación determinística de coordenadas)

pyarrow (lectura de archivos Parquet)

Nota: En un entorno real, la latitud/longitud debería venir del origen o un shape oficial.
Para este challenge, se generan coordenadas reproducibles basadas en el PULocationID.

2. Requisitos previos

Python 3.x instalado

pip configurado

Archivo .parquet con los viajes

3. Instalación

   3.1 Clonar el repositorio

git clone <https://github.com/dabbi20/SIMON-MOVILIDAD.git>.git


3.2 (Opcional) Crear entorno virtual

Linux/Mac:
python -m venv venv
source venv/bin/activate

Windows:
python -m venv venv
venv\Scripts\activate

3.3 Instalar dependencias

pip install -r requirements.txt

Contenido del requirements.txt:
pandas
numpy
pyarrow

4. Estructura del repositorio

.
├── process_data.py

├── README.md

├── requirements.txt

├── outputs/

│ ├── ultima_ubicacion.csv

│ └── viajes_por_hora.csv
└── docs/

└── presentacion.pdf

5. Cómo ejecutar el script

python process_data.py ruta/al/archivo.parquet

Ejemplo:

python process_data.py data/trips.parquet

Esto generará automáticamente:

outputs/ultima_ubicacion.csv

outputs/viajes_por_hora.csv

6. Explicación del procesamiento
   6.1 Lectura del archivo Parquet

Se lee el archivo con pandas y se visualiza un printSchema.

6.2 Generación de latitud/longitud sintética

Como el dataset no contiene coordenadas, se generan basadas en el PULocationID usando rangos aproximados de NYC:

Latitud entre 40.55 y 40.95
Longitud entre -74.15 y -73.70

Estas columnas agregadas son:

pickup_latitude

pickup_longitude

6.3 Salida 1: Última Ubicación Conocida

vehicle_id = PULocationID
Se ordena el dataset por tpep_pickup_datetime descendente.
Se toma el último registro correspondiente a cada vehículo.
Columnas finales:

vehicle_id

ultimo_timestamp

ultima_latitud

ultima_longitud

6.4 Salida 2: Viajes por Hora

Se extrae la hora del tpep_pickup_datetime.
Se agrupa por hora del día.
Se genera un total de viajes para cada hora entre 0 y 23.

Columnas:

hora_del_dia

total_viajes

7. Archivos de salida incluidos

En la carpeta outputs/ ya se incluyen ejemplos generados:

ultima_ubicacion.csv

viajes_por_hora.csv

8. Presentación en 5 diapositivas

En docs/presentacion.pdf se incluye una presentación explicando:

El problema

Herramientas

Proceso

Outputs

Mejoras futuras

9. Resumen rápido

git clone <repo>
cd <repo>
pip install -r requirements.txt
python process_data.py archivo.parquet

Esto genera:

ultima_ubicacion.csv

viajes_por_hora.csv

