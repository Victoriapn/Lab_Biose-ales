En esta practica se utilizando las librerías NumPy y SciPy, con el objetivo de generar, analizar y reconstruir señales periódicas. Para llevar a cabo este procedimiento, inicialmente se abordó la generación de señales mediante la construcción de dos ondas periódicas de prueba: una cuadrada y una triangular. Ambas fueron definidas con los mismos parámetros base para permitir su comparación, estableciendo una amplitud de 5.0, una frecuencia fundamental de 0.5 Hz y una frecuencia de muestreo de 100 Hz. Además, se utilizó un total de 600 muestras con el fin de visualizar correctamente tres periodos completos de cada onda.

Posteriormente, se procedió con el análisis espectral, para lo cual se desarrolló una función que calcula los coeficientes de la serie de Fourier en su forma exponencial para ambas señales discretas, empleando el algoritmo de la Transformada Rápida de Fourier (FFT). A partir de este cálculo, se extrajeron y graficaron los espectros de magnitud y fase. Finalmente, en la etapa de reconstrucción, se elaboró una función matemática que, partiendo de los coeficientes obtenidos, permitió reconstruir las señales en el dominio del tiempo mediante la suma progresiva de los armónicos individuales. Esta reconstrucción fue evaluada sistemáticamente utilizando conjuntos de N = 1, 3, 5, 20 y 50 armónicos.

g. esprectros de magnitud y fase 
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/12bd2657-31f0-43c0-94ba-fca0b0243414" />

En la gráfica del espectro de magnitud se observa una simetría par respecto al origen, lo que concuerda con lo esperado para una señal de valores reales en el tiempo, [1]. En la frecuencia de $0\text{ Hz}$ el valor es cero, lo que demuestra que la señal no tiene un nivel de voltaje continuo (DC) y que oscila de forma balanceada alrededor del eje horizontal. El pico principal aparece en la frecuencia fundamental de $\pm 0.5\text{ Hz}$ con un valor aproximado de $3.18$, el cual corresponde con la amplitud teórica calculada como $\frac{2A}{\pi}$ para una onda cuadrada de amplitud $5$. Además, se nota que los armónicos caen de forma lenta, a razón de $1/k$, debido a los saltos bruscos que tiene la señal en los cambios de ciclo, [1].  

En el espectro de fase se presenta una simetría impar entre las frecuencias positivas y negativas, [1]. Para el lado positivo, los armónicos tienen un desfase constante cercano a $-\pi/2$ radianes ($-1.57\text{ rad}$), mientras que en el lado negativo el valor es de $+\pi/2$ radianes ($+1.57\text{ rad}$). Este desfase fijo refleja el comportamiento senoidal de la onda generada [1]. En los puntos donde la magnitud de los armónicos llega a ser muy baja, la fase se mantiene en cero debido al filtro numérico del código.

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/d6092254-36a2-4fe8-8c83-b185068de96e" />

Para la señal triangular, el espectro de magnitud también muestra simetría par y un valor medio nulo en 0 Hz, ya que tampoco tiene nivel de DC [1]. Sin embargo, la diferencia con la cuadrada está en la rapidez con la que decaen los armónicos. En esta señal la caída es mucho más pronunciada, proporcional a 1/k^2, debido a que la onda en el tiempo es continua y no tiene saltos instantáneos [1]. El armónico fundamental en ±0.5 Hz concentra casi toda la energía con un valor cercano a 2.0, y a partir de 5 Hz la amplitud de los armónicos restantes es prácticamente despreciable.

En la gráfica de fase se mantiene la simetría impar requerida para señales reales [1]. Los valores se alternan entre 0 y ±pi radianes (±3.14 rad), lo que significa que los coeficientes de Fourier de la señal triangular son reales pero van alternando de signo entre positivo y negativo [1]. Al igual que en la señal anterior, en las frecuencias donde no hay contenido de energía la fase se grafica en cero para evitar ruido de cálculo. 

i) Reconstruya la señal cuadrada y la señal triangular utilizando N = 1, 3, 5, 20 y 50 armónicos, y
grafique cada reconstrucción junto con la señal original.

<img width="1003" height="1189" alt="image" src="https://github.com/user-attachments/assets/4519137d-4413-4079-94e5-85b86c835ed2" />

En las gráficas de la señal cuadrada, se observó que en los saltos de -5 a 5 la señal no se reconstruye perfectamente. Al usar N=3 y N=5, la onda se ve con muchas oscilaciones en toda su longitud. Al subir a N=50, la parte plana de la onda se estabiliza casi por completo, pero en las esquinas del salto siempre queda un pico visible. Aunque se sumen más armónicos, ese pico se hace más angosto, pero no disminuye su altura.

Consultando la bibliografía, esto se conoce como el fenómeno de Gibbs. Esto ocurre porque se están usando ondas continuas (senos y cosenos) para tratar de dibujar un salto que es completamente recto y vertical. Como en la práctica no es posible sumar armónicos hasta el infinito, siempre va a faltar información, lo que produce esa oscilación en la esquina. No es un error del código en Python, sino una característica matemática de la serie de Fourier. Según la teoría, ese pico extra nunca desaparece, sino que se mantiene siempre cerca del 9% del tamaño total del salto, sin importar cuántos armónicos se agreguen al código [2].


Bibliografia
[1] A. V. Oppenheim, A. S. Willsky y S. H. Nawab, Señales y sistemas, 2.ª ed. México: Prentice Hall, 1998, pp. 186-211.
