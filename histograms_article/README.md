# Histogramas: Decodificando Datos

En la era de la información, donde grandes volúmenes de datos son la norma, la habilidad para visualizar y analizar estos datos se convierte en una habilidad indispensable. Los histogramas emergen como una herramienta estadística crucial, no sólo para la visualización efectiva de datos, sino también para la interpretación y el análisis de sus distribuciones. Este artículo examina cómo la estructuración de datos en bins dentro de un histograma puede superar el reto de visualizar puntos de datos superpuestos, proporcionando así una ventana clara hacia patrones y tendencias ocultas.

## Datos Superpuestos

Los histogramas son herramientas estadísticas fundamentales para la visualización y el análisis de distribuciones de datos. A menudo, en el estudio de una variable, se mide un gran número de individuos, resultando en una cantidad de datos donde algunos valores pueden solaparse o incluso quedar ocultos.

La superposición de datos en la visualización es un fenómeno que se produce cuando múltiples puntos de datos se representan en un mismo espacio visual, resultando en que unos puntos se monten sobre otros. Este efecto puede ser particularmente problemático en conjuntos de datos grandes, donde la frecuencia de valores similares es alta.

La superposición puede distorsionar la interpretación de la información al ocultar la verdadera cantidad de observaciones en un área específica del gráfico. En la práctica, esto significa que, aunque visualmente puede parecer que hay una baja cantidad de datos en ciertos rangos de valor, en realidad puede haber una concentración significativa de observaciones que no se perciben a simple vista. Para resolver este problema, se utiliza el histograma.


```python
import pandas as pd
import numpy as np

np.random.seed(0)

n = 100
id = range(1, n + 1)
# https://www.eltiempo.com/archivo/documento/CMS-13128617
height = np.random.normal(172, 8, n)
# Body mass index (BMI)
# https://en.wikipedia.org/wiki/Body_mass_index
# weight = BMI * height^2
bmi = 26 + np.random.normal(0, 2.5, n)
weight = bmi * ((height/100) ** 2)
commute_time = np.random.uniform(15, 60, n)

data = pd.DataFrame({'ID': id, 'Height': height, 'Weight': weight, 'BMI': bmi})
data.sort_values(by=['Height'],inplace=True,ignore_index=True)
```


```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 2))
sns.scatterplot(x=data['Weight'], y=np.zeros(n), s=100, color="green", alpha=0.5, marker='o', legend=False)
plt.yticks([])
plt.xlabel("Weight")
plt.title("Overlapping Data")
plt.ylim(-1, 5)
plt.gca().axes.get_yaxis().set_visible(False)
plt.show()
```


    
![Alt text](README_files/README_2_0.png 'La imagen muestra un gráfico de dispersión titulado "Overlapping Data", enfocado en el eje x etiquetado como "Weight", que varía aproximadamente entre 50 y 100. Representa datos que se solapan, evidenciado por los puntos translúcidos en verde. La gráfica es ancha y baja, sin marcas visibles en el eje y, que ha sido ocultado para resaltar la distribución de los pesos. Los puntos, de tamaño considerable, parecen más concentrados alrededor de ciertos valores de peso, sugiriendo una variación en la densidad de los datos.')
    


## Agrupando Datos

Un histograma se crea dividiendo el rango de valores posibles en intervalos, conocidos como 'bins', y contabilizando cuántas mediciones caen en cada uno de ellos. La altura de cada pila dentro de un bin refleja el número de mediciones que corresponden a ese intervalo. Esta representación facilita la identificación de la frecuencia con la que ocurren ciertos rangos de valores en el conjunto de datos.

Al dividir el rango de valores posibles en segmentos discretos, y apilar las mediciones correspondientes, los histogramas revelan patrones que son fundamentales para el análisis estadístico. Estos patrones pueden indicar tendencias, picos, y anomalías en los datos. Por ejemplo, un pico en un intervalo puede señalar un rango de peso común en una población.

Además, la altura de las pilas en cada bin no solo muestra cuántas mediciones caen dentro de un rango específico, sino que también puede indicar la centralización o dispersión de los datos. Un histograma con pilas de altura similar sugiere una distribución uniforme, mientras que las pilas de diferentes alturas indican variabilidad.


```python
bin_count = 10
counts, bin_edges = np.histogram(data['Weight'], bins=bin_count)
hist_data = pd.DataFrame()

for i in range(bin_count):
    bin_center = (bin_edges[i] + bin_edges[i + 1]) / 2
    bin_data = pd.DataFrame({'x': [bin_center] * counts[i], 'y': range(counts[i])})
    hist_data = pd.concat([hist_data, bin_data], ignore_index=True)

plt.figure(figsize=(10, 4))
sns.scatterplot(x=hist_data['x'], y=hist_data['y'], s=100, color="green", marker='o', legend=False)

plt.xlabel("Weight")
plt.title("Grouping Data")
plt.xticks(ticks=bin_edges, labels=np.round(bin_edges, 1))
plt.gca().axes.get_yaxis().set_visible(False)
plt.show()
```


    
![Alt text](README_files/README_4_0.png '
La imagen presenta un gráfico titulado "Grouping Data" que muestra puntos verdes distribuidos verticalmente en líneas que representan diferentes pesos. Las líneas verticales de puntos están alineadas con marcas específicas en el eje x, que varía de aproximadamente 52 a 107, agrupadas en intervalos regulares, lo que indica agrupamientos de datos en categorías de peso. El eje y no es visible, enfocando la atención en la distribución horizontal de los puntos.')
    


El análisis detallado de las visualizaciones nos muestra cómo un gráfico de puntos agrupados, donde cada punto representa una medición individual, puede transformarse en un histograma de barras para una interpretación más eficiente. En el histograma de barras, los 'bins' representan rangos de valores, y las alturas de las barras reflejan la cantidad de mediciones en esos rangos. Esta transición de puntos individuales a barras agrupadas simplifica la visualización y mejora la interpretación de la frecuencia y la distribución de los datos, permitiendo a los analistas capturar rápidamente la esencia de la información contenida en el conjunto de datos.


```python
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=bin_count, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight")
plt.show()
```


    
![Alt text](README_files/README_6_0.png 'La imagen muestra un histograma de color verde con el título "Histogram of Weight". El eje X, etiquetado como "Weight", va de 50 a más de 100, y el eje Y, etiquetado como "Count", muestra la frecuencia, contando en incrementos de 2 hasta un valor máximo que parece ser 18. Las barras representan la frecuencia de pesos, con alturas variables, indicando una distribución de los datos de peso recopilados.')
    


## Distribuciones y Predicciones

Los histogramas ofrecen más que una simple instantánea de datos pasados; son predictores potenciales de eventos futuros. Al observar la altura de las barras, los analistas pueden cuantificar la probabilidad de ocurrencia de un evento dentro de un rango de valores. Un rango con una barra alta significa una mayor probabilidad de que los eventos futuros caigan en ese rango, lo que puede ser crucial para la toma de decisiones en campos como la calidad del control de procesos o la gestión de riesgos.


```python
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=bin_count, color="green", kde=True)
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Distribution")
plt.show()
```


    
![Alt text](README_files/README_8_0.png "La imagen muestra un histograma titulado `Histogram of Weight with Distribution`, con barras verdes que representan el conteo de observaciones de peso agrupadas por rango. Las barras varían en altura, indicando la frecuencia de los pesos; las más altas sugieren que esos rangos de peso son más comunes. Una línea curva atraviesa la parte superior de las barras, representando la estimación de la distribución de los datos. Los valores en el eje X varían de 50 a más de 100, y el eje Y está etiquetado de 0 en incrementos de 2, mostrando el conteo de observaciones por rango de peso.")
    


La forma del histograma brinda pistas sobre la distribución estadística subyacente. Un perfil en forma de campana simétrica sugiere que los datos pueden seguir una distribución normal, que es común en fenómenos naturales y sociales. Por otro lado, una forma sesgada hacia un extremo podría implicar una distribución exponencial, que a menudo se encuentra en procesos que involucran decaimiento o crecimiento, como la desintegración radiactiva o la adopción de nuevas tecnologías.


```python
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Height'], bins=bin_count, color="blue", kde=True)
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Height")
plt.ylabel("Count")
plt.title("Histogram of Height with Distribution")
plt.show()
```


    
![Alt text](README_files/README_10_0.png "La imagen presenta un histograma titulado `Histogram of Height with Distribution`, con barras azules que ilustran la frecuencia de distintas alturas. Las barras forman una curva similar a una campana, con la mayor concentración de datos alrededor del centro, indicando una distribución normal. La distribución de los datos está superpuesta con una línea de curva suave, que sugiere la tendencia general y la probabilidad de los datos dentro de esos rangos de altura. El eje X, que representa la altura, varía de 150 a 190, y el eje Y, que muestra el conteo, está marcado en incrementos de 2, mostrando la cantidad de datos en cada rango de altura.")
    


La predicción de probabilidades a partir de histogramas no es infalible; se basa en la suposición de que las condiciones existentes persistirán en el futuro. Sin embargo, esta herramienta estadística proporciona una base sólida para inferir tendencias y patrones que son esenciales para comprender tanto la actualidad como el potencial futuro de los datos observados.

## Calibrando Bins en Histogramas

La selección del ancho de los 'bins' en un histograma es una parte integral del proceso de visualización de datos que tiene un impacto significativo en la interpretación de los resultados estadísticos. Un 'bin' demasiado estrecho puede resultar en un gráfico sobre-fragmentado que hace difícil discernir cualquier patrón significativo, similar a mirar cada punto de dato de manera aislada.


```python
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=100, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Thin Bins")
plt.show()
```


    
![Alt text](README_files/README_12_0.png "")
    


Por otro lado, 'bins' excesivamente anchos pueden amalgamar datos críticos, borrando diferencias sutiles y posiblemente relevantes entre las mediciones.


```python
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=2, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 5))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Thick Bins")
plt.show()
```


    
![ALT text](README_files/README_14_0.png "La imagen muestra un histograma titulado `Histogram of Weight with Thick Bins`, donde se visualizan dos barras verticales de color verde que representan conteos de datos de peso dentro de intervalos anchos o `thick bins`. El eje X, que muestra el peso, abarca de 50 a más de 100, mientras que el eje Y, representando el conteo, está marcado en incrementos de 5 hasta un máximo que supera los 50. Esta presentación indica la frecuencia de datos en amplios rangos de peso, ofreciendo una visión generalizada de la distribución de los datos.")
    


Este acto de equilibrio entre demasiado detalle y una excesiva generalización requiere una cuidadosa consideración del contexto de los datos y del propósito del análisis. Los estadísticos a menudo prueban diferentes anchos de 'bins' y comparan visualmente los histogramas resultantes para evaluar cuál presenta la mejor interpretación de la distribución de datos.

## Cálculo Cuantitativo de Bins

En algunos casos, se pueden aplicar métodos cuantitativos para determinar el ancho óptimo de 'bins', basados en medidas como la amplitud de los datos y el tamaño de la muestra.

Se pueden aplicar métodos cuantitativos como la regla de Sturges, que sugiere que el número óptimo de 'bins' puede calcularse como:

$$ k = 1 + \log_{2}(n) $$

donde $ n $ es el tamaño de la muestra.


```python
bin_count_sturges = int((1 + np.log2(n)).round())
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=bin_count_sturges, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Sturges' formula")
plt.show()
```


    
![png](README_files/README_16_0.png "La imagen muestra un histograma verde titulado `Histogram of Weight with Sturges' formula`. Las barras del histograma representan el conteo de frecuencias de peso dentro de rangos específicos en el eje X, que va desde 50 hasta poco más de 100. El eje Y, etiquetado como `Count`, muestra la frecuencia de las observaciones, y tiene valores que van de 0 a más de 20 en incrementos de 2. La barra más alta se encuentra en el rango de 60 a 70, indicando que la mayor frecuencia de pesos cae dentro de este intervalo.")
    


La regla de la raíz cuadrada propone un número de 'bins' equivalente a la raíz cuadrada del tamaño de la muestra, simplificando el cálculo a:

$$ k = \sqrt{n} $$


```python
bin_count_sturges = int((np.sqrt(n)).round())
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], bins=bin_count_sturges, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Square-root Choice")
plt.show()
```


    
![ALT text](README_files/README_18_0.png "La imagen muestra un histograma titulado `Histogram of Weight with Square-root Choice`, con barras verticales de color verde que representan la distribución de la frecuencia de los pesos. Las barras están agrupadas en rangos de peso que van desde 50 hasta más de 100, cada una representando la cuenta de observaciones en esos rangos específicos. La altura de las barras varía, indicando diferentes conteos, y el eje Y, etiquetado como `Count`, tiene marcas desde 0 hasta más de 18, incrementando de 2 en 2. Este histograma utiliza una regla de raíz cuadrada para determinar el ancho de los 'bins'.")

La regla de Freedman-Diaconis utiliza el rango intercuartílico $IQR$ para determinar el ancho del 'bin' $ h $ de una manera que minimiza la diferencia en la distribución de la muestra y la representación del histograma:

$$ h = 2 \times \frac{\text{IQR}}{n^{1/3}} $$


```python
Q1 = np.percentile(data['Weight'], 25, method= 'midpoint')
Q3 = np.percentile(data['Weight'], 75, method= 'midpoint')
IQR = Q3 - Q1
h_reedman_diaconis = 2 * IQR /(n ** (1/3))
print(h_reedman_diaconis)
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], binwidth=h_reedman_diaconis, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Freedman–Diaconis' Choice")
plt.show()
```

    7.862429209262235



    
![ALT text](README_files/README_20_1.png "La imagen muestra un histograma titulado `Histogram of Weight with Freedman-Diaconis' Choice`. Presenta barras verticales de color verde que representan la frecuencia de diferentes rangos de peso, que varían de 50 a más de 100. La altura de las barras indica el conteo de observaciones dentro de cada rango de peso, con el eje Y marcado de 0 a más de 24 en incrementos de 2. Este histograma aplica la regla de Freedman-Diaconis para determinar el ancho de las barras (`bins`), basado en el rango intercuartílico de los datos, buscando una representación precisa de la distribución de la muestra.")
    


Por último, la regla de Scott ajusta el ancho del 'bin' para minimizar la distorsión en la representación de la distribución normal y se calcula como:

$$ h = 3.49 \times \sigma \times n^{-1/3} $$

donde $ \sigma $ es la desviación estándar de los datos.


```python
h_scott = 3.49 * data['Weight'].std() /(n ** (1/3))
plt.figure(figsize=(10, 4))
histplot = sns.histplot(data['Weight'], binwidth=h_scott, color="green")
max_count = int(max(histplot.patches, key=lambda p: p.get_height()).get_height())
plt.yticks(ticks=range(0, max_count+1, 2))

plt.xlabel("Weight")
plt.ylabel("Count")
plt.title("Histogram of Weight with Scott's Normal Reference Rule")
plt.show()
```


    
![ALT text](README_files/README_22_0.png "La imagen muestra un histograma verde titulado `Histogram of Weight with Scott's Normal Reference Rule`. Las barras representan el conteo de observaciones de peso distribuidas en rangos específicos. La altura de las barras refleja la frecuencia en esos rangos, comenzando en cero y alcanzando un máximo superior a 24. El eje Y está marcado en incrementos de 2, mientras que el eje X muestra los rangos de peso desde 50 hasta más de 100. Este histograma utiliza la regla de Scott, que determina el ancho de las barras basándose en la desviación estándar de los datos para ajustar la distribución normal.")
    


Estas fórmulas matemáticas proporcionan una base estructurada para definir el ancho de 'bins' y pueden ser particularmente útiles cuando se manejan grandes conjuntos de datos o cuando se requiere un análisis estadístico riguroso. Aplicar estos métodos ayuda a evitar la subjetividad y asegura que el histograma refleje las propiedades intrínsecas de los datos.

## Conclusión

Los histogramas, con su capacidad para transformar datos crudos en visualizaciones comprensibles, juegan un papel crucial en el análisis de datos moderno. Al agrupar eficientemente los datos y revelar sus distribuciones subyacentes, estos gráficos no solo mejoran la interpretación de los conjuntos de datos complejos, sino que también allanan el camino para modelos predictivos más precisos y decisiones informadas. Este análisis demuestra cómo una herramienta aparentemente simple puede tener un impacto profundo en el campo de la ciencia de datos y el aprendizaje automático.
