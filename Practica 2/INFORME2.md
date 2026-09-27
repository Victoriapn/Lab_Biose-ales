1. Exploración y descripción de la base de datos

La base de datos utilizada está compuesta por registros electrocardiográficos (ECG) y un archivo de diagnóstico asociado. En total, se encontraron 10646 registros, correspondientes a archivos individuales de ECG. El archivo Diagnostics.xlsx presenta una dimensión de 10646 filas y 16 variables, entre las que se encuentran el tipo de ritmo, características del paciente y diferentes parámetros electrocardiográficos.

Cada registro de ECG contiene 12 canales, correspondientes a las derivaciones estándar: I, II, III, aVR, aVL, aVF, V1, V2, V3, V4, V5 y V6. La frecuencia de muestreo utilizada es de 500 Hz, con aproximadamente 4999 muestras por registro, lo que corresponde a una duración aproximada de 9,998 segundos.

La variable Rhythm permitió identificar los diferentes tipos de ritmo presentes en la base de datos y establecer la distribución de los registros entre las diferentes clases. Esta distribución se presentó mediante una gráfica de barras, con el propósito de visualizar la cantidad de registros pertenecientes a cada tipo de ritmo. De estas clases, se destacan para el análisis posterior: AFIB (Fibrilación auricular): 1780 registros, y ST (Taquicardia sinusal): 1568 registros

El resto de clases presentes (visibles en la Tabla 1 y el gráfico de barras generados en el notebook) muestran que la base de datos está desbalanceada, es decir, no todas las arritmias tienen un número similar de registros, lo cual debe tenerse en cuenta al interpretar comparaciones estadísticas entre grupos y al considerar un eventual uso de estos datos para clasificación automática.

                            | Ritmo	   |  Numero_de_registros |	Porcentaje (%) |
                            |----------|----------------------|----------------|
                    |0	    |SB	       | 3889	              |    36.53|
                    |1	    |SR	       | 1826	              |    17.15|
                    |2	    |AFIB	   | 1780	              |    16.72|
                    |3   	|ST	       | 1568	              |    14.73|
                    |4	    |SVT	   | 587	              |    5.51|
                    |5	    |AF	       | 445	              |    4.18|
                    |6	    |SA	       | 399	              |    3.75|
                    |7	    |AT	       | 121	              |    1.14|
                    |8	    |AVNRT	   |  16	              |    0.15|
                    |9	    |AVRT	   |   8	              |    0.08|
                    |10	    |SAAWR	   |   7	              |    0.07|

![alt text](image.png)
