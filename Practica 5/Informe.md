En esta práctica se realizó el análisis frecuencial de señales para observar su comportamiento en el dominio de la frecuencia y aplicar estos conceptos en registros biomédicos. Inicialmente, se creó una señal compuesta por la suma de tres ondas sinusoidales de 40, 80 y 160 Hz, definiendo una frecuencia de muestreo de 1000 Hz para cumplir con el criterio de Nyquist y representar la señal adecuadamente. A partir de 10 periodos de esta señal, se calculó la transformada de Fourier para graficar su espectro e identificar las tres frecuencias originales, comprobando además su reconstrucción en el tiempo mediante la transformada inversa y el aislamiento individual de cada componente aplicando un filtrado de coeficientes.

En la segunda parte, se analizó una señal de electrocardiograma (ECG) muestreada a 250 Hz utilizando el periodograma de Welch con una ventana Hanning, justificando tanto el ancho de la ventana como su solapamiento. Este análisis permitió identificar el ruido presente en el registro, el cual fue eliminado mediante un filtro en frecuencia para luego recuperar la señal limpia con la transformada inversa y verificar los resultados en un nuevo periodograma. Finalmente, se aplicó este mismo método de Welch para analizar y comparar la densidad espectral de potencia entre el registro de ECG de un paciente sano y el de un sujeto con arritmia, evaluando las diferencias frecuenciales entre ambas condiciones.

<img width="999" height="468" alt="image" src="https://github.com/user-attachments/assets/5fb489c4-40ed-483e-9785-be3afcc4c770" />

Para el punto 4.1, de acuerdo con el teorema de muestreo de Nyquist, para evitar el solapamiento espectral o aliasing y representar correctamente la información, la frecuencia de muestreo debe ser como mínimo el doble de la componente de frecuencia más alta. Dado que la frecuencia máxima de la señal es de 160 Hz, la frecuencia mínima teórica requerida es de 320 Hz. Sin embargo, en la práctica se recomienda muestrear a una velocidad varias veces superior a la frecuencia máxima de interés para visualizar adecuadamente la forma de onda en el dominio del tiempo [1]. Por esta razón, se eligió una frecuencia de muestreo de 1000 Hz, la cual permite obtener un intervalo de 0,001 segundos. Finalmente, al graficar la señal resultante durante 10 periodos de la frecuencia fundamental de 40 Hz (0,25 segundos), se observa una onda periódica compleja producto de la superposición constructiva y destructiva de las tres frecuencias originales.

<img width="1014" height="468" alt="image" src="https://github.com/user-attachments/assets/9df424df-6983-4876-85b9-be39d990a77b" />

Para el punto 4.2, al aplicar la transformada de Fourier a los 10 periodos de la señal, se obtuvo su espectro de frecuencia. Como la señal es puramente real, el espectro presenta simetría, por lo que basta con analizar la mitad positiva hasta la frecuencia de Nyquist. En la gráfica resultante se identifican con claridad tres picos sobresalientes ubicados exactamente en 40, 80 y 160 Hz, comprobando así las componentes originales de la onda. Además, tras escalar los coeficientes por el número de muestras y duplicar las frecuencias positivas, se verifica que cada pico alcanza una amplitud de 1, coincidiendo con los valores iniciales definidos.

<img width="999" height="469" alt="image" src="https://github.com/user-attachments/assets/5b9d8959-0d6d-4c49-9d35-3cd94ca3537c" />

4.3 Para reconstruir la señal en el dominio del tiempo, se aplicó la transformada inversa de Fourier (np.fft.ifft) sobre los coeficientes obtenidos anteriormente. Al tomar la parte real del resultado y graficarla junto con la señal original, se demostró que ambas ondas se superponen de forma exacta, sin pérdidas de amplitud ni desfases. Esto confirma que la transformación al dominio de la frecuencia conserva toda la información y permite recuperar la señal tal como era al principio.

4.4 ¿Podría decir que las siguientes líneas aplican un filtro? ¿Por qué?

Sí, las líneas de código presentadas aplican un filtro sobre la señal porque seleccionan únicamente una banda específica de frecuencias y eliminan las demás [2]. Al calcular la transformada de Fourier de la señal (Fl = np.fft.fft(x)), los datos pasan al dominio de la frecuencia y quedan ordenados en distintos índices. Después, al crear un arreglo de ceros (F2 = np.zeros((len(Fl)))) y conservar solo los valores ubicados entre los índices 9 y 12 (F2[9:13] = Fl[9:13]), se mantienen las componentes que interesan y se anula por completo el resto del espectro [2].   

En el procesamiento de señales, este procedimiento funciona como un filtro ideal en frecuencia, ya que deja pasar sin cambios el rango escogido y corta de raíz las frecuencias no deseadas [2]. Por último, al aplicar la transformada inversa (np.fft.ifft(F2)), se recupera la señal en el tiempo conteniendo solo la oscilación de esa banda filtrada. Al repetir este mismo proceso en los índices correspondientes a 40, 80 y 160 Hz, se logra separar y reconstruir cada una de las tres ondas sinusoidales que formaban la señal original. 

<img width="1013" height="468" alt="image" src="https://github.com/user-attachments/assets/92a209df-c27c-47df-b381-daedcbba51bb" />
Fig 1. Señal ECG original

<img width="1012" height="468" alt="image" src="https://github.com/user-attachments/assets/454fe567-69f6-4472-bbab-1bfa08679a10" />
Fig 2. Periodograma de Welch - ECG original

<img width="1189" height="690" alt="image" src="https://github.com/user-attachments/assets/5ea08ca1-53e7-4f42-9ee4-98899a897fef" />
Fig 3. ECG original / ECG filtrado - Sin interferencia de 60 Hz

<img width="1012" height="469" alt="image" src="https://github.com/user-attachments/assets/5fe0d092-ee44-4124-9fc2-7e0e54d89e45" />
Fig 4. Comparación de periodogramas de Welch

4.5 Al visualizar la señal original de ECG, se observa que sobre el trazo cardíaco existe una oscilación rápida de alta frecuencia que ensucia la morfología de las ondas. Para analizar este comportamiento en frecuencia, se calculó el periodograma de Welch usando una ventana Hanning con un ancho de 500 muestras (equivalente a 2 segundos) y un solapamiento de 250 muestras (50 %). Se eligió este ancho de ventana porque ofrece una resolución espectral de 0,5 Hz ($F_s / N = 250 / 500$), suficiente para separar con precisión componentes cercanas sin perder estabilidad, mientras que el solapamiento del 50 % compensa la atenuación de los bordes generada por la ventana Hanning y reduce la varianza de la estimación [3]

En la gráfica del periodograma original se observa que la potencia fisiológica del corazón se concentra por debajo de los 40 Hz, pero aparece un pico muy pronunciado exactamente en 60 Hz (con una densidad espectral superior a $10^{-2}$), lo que confirma una fuerte interferencia de la red eléctrica. Debido a esto, se aplicó un filtro en el dominio de la frecuencia anulando los coeficientes ubicados en la banda de $60 \pm 0,5\text{ Hz}$. Al calcular la transformada inversa y comparar ambos trazos en el tiempo, se evidencia que la señal filtrada elimina por completo el ruido superpuesto y permite distinguir con claridad cada onda P, el complejo QRS y la onda T. Finalmente, al superponer ambos periodogramas de Welch, se comprueba que el pico de 60 Hz desaparece por completo en la señal filtrada (cayendo por debajo de $10^{-7}$), mientras que el resto del espectro cardíaco se mantiene intacto.

<img width="1189" height="690" alt="image" src="https://github.com/user-attachments/assets/6bbc5dc3-3cfc-4f83-ba79-98e68ff00674" />
Fig 5. ECG con ritmo sinusal (SR) - Derivación II / ECG con fibrilación auricular (AFIB) - Derivación II

<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/3be85207-99fa-4bc0-ab0b-1ae54e8a6cac" />
Fig 6. Comparación espectral de ECG mediante Welc

Al contrastar la derivación II de ambos registros (de 10 segundos y muestreados a 500 Hz), se nota a simple vista una diferencia clara en la regularidad del ritmo cardíaco. En el paciente con ritmo sinusal (SR) los complejos QRS aparecen de forma constante y equidistante, acompañados de ondas P y T bien definidas; en cambio, el sujeto con fibrilación auricular (AFIB) presenta intervalos R-R completamente desordenados, ausencia de ondas P claras y pequeñas vibraciones irregulares sobre la línea base.   Estas variaciones se trasladan directamente al periodograma de Welch, el cual se calculó empleando una ventana Hanning de 1000 muestras (2 segundos) con 500 muestras de solapamiento (50 %). Dicho ancho de ventana permite alcanzar una resolución de 0,5 Hz ($F_s / N = 500 / 1000$) para distinguir con exactitud los picos de baja frecuencia, mientras que el solapamiento del 50 % suaviza la estimación al reducir la varianza y evitar que se pierda información en los extremos de cada segmento [3]. Como resultado, la gráfica espectral muestra que la potencia máxima del paciente sano se ubica en 1,00 Hz (equivalente a unos 60 latidos por minuto), mientras que en la fibrilación auricular el pico dominante se desplaza a 4,00 Hz y la energía se dispersa mucho más entre los 15 y 35 Hz debido a la actividad auricular desorganizada. 

Conclusiones 

1. El uso de la Transformada Rápida de Fourier (FFT) y su inversa demostró que pasar una señal al dominio de la frecuencia permite identificar con exactitud sus componentes fundamentales y manipularlas sin perder información, siempre que se respete el criterio de muestreo de Nyquist para evitar el aliasing.
2. El filtrado espectral resulta una herramienta directa y efectiva para eliminar interferencias específicas en registros fisiológicos, como el ruido de 60 Hz de la red eléctrica en el electrocardiograma, logrando recuperar la morfología limpia de las ondas P, QRS y T en el dominio del tiempo.
3. El periodograma de Welch con ventana Hanning y solapamiento del 50 % permite diferenciar claramente un ritmo cardíaco sano de una arritmia, evidenciando cómo la fibrilación auricular desplaza el pico de máxima potencia hacia frecuencias más altas (4 Hz frente a 1 Hz) y dispersa la energía espectral debido a la actividad eléctrica desorganizada del corazón




Referencias 
[1] National Instruments, "Ancho de banda, teorema de muestreo de Nyquist y aliasing," NI, 2026. [En línea]. Disponible en: https://www.ni.com/es/shop/data-acquisition/measurement-fundamentals/analog-fundamentals/acquiring-an-analog-signal--bandwidth--nyquist-sampling-theorem-.html

[2] S. W. Smith, The Scientist and Engineer's Guide to Digital Signal Processing, California Technical Publishing, 1997. [En línea]. Disponible en: https://www.dspguide.com/ch17/1.htm

[3] P. D. Welch, "The use of fast Fourier transform for the estimation of power spectra: A method based on time averaging over short, modified periodograms," IEEE Transactions on Audio and Electroacoustics, vol. 15, no. 2, pp. 70–73, Jun. 1967. [En línea]. Disponible en: https://ieeexplore.ieee.org/document/1161901
