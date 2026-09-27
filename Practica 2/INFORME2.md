En esta segunda parte de la práctica, trabajamos con una amplia base de datos de señales de electrocardiograma (ECG). El primer paso consistió en realizar una exploración general de los archivos para comprender la estructura de la información suministrada. Para ello, identificamos el número total de registros, los tipos de arritmias disponibles y la cantidad de sujetos por grupo, así como las derivaciones (canales), la frecuencia de muestreo y la duración temporal de los registros.

Posteriormente, seleccionamos dos tipos específicos de arritmias para graficarlas y analizar su comportamiento, observando aspectos como la morfología de la señal, la amplitud y la regularidad de los latidos. A partir de estas señales, realizamos un análisis descriptivo extrayendo variables estadísticas clave para cada paciente: calculamos la media, la desviación estándar, los valores máximos y mínimos, la frecuencia cardíaca (FC) y el valor RMS.

Finalmente, el objetivo principal era realizar un análisis estadístico comparativo riguroso entre ambos grupos de arritmias. Para lograrlo, formulamos una hipótesis nula y una alternativa. Antes de comparar los grupos directamente, debíamos comprobar los supuestos estadísticos para decidir qué prueba aplicar: verificamos la normalidad de las variables (usando la prueba de Shapiro-Wilk) y la homocedasticidad o igualdad de varianzas (mediante la prueba de Levene). La instrucción de la guía era clara: si los datos cumplían con los supuestos, utilizaríamos una prueba paramétrica como la t de Student para muestras independientes; si no los cumplían, debíamos recurrir a un análisis no paramétrico aplicando la prueba U de Mann-Whitney.





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
