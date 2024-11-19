# Técnicas "difusas" de agregación de variables ambientales

> + **_Tipo de material_**: <span style="display: inline-block; font-size: 12px; color: white; background-color: #029BF9; border-radius: 5px; padding: 5px; font-weight: bold;"> Teoría</span> <span style="display: inline-block; font-size: 12px; color: white; background-color: #4caf50; border-radius: 5px; padding: 5px; font-weight: bold;">Prácticas</span> 
> + **_Versión_**: 2024-2025
> + **_Asignatura_** : Ecoinformática (Grado en biología). 
> + **_Autor_**: Cristina Crespo Bastias (crbasc@gmail.com), Curro Bonet-García (fjbonet@uco.es)
> + **_Duración_**: 50 minutos.



## Objetivos

Esta actividad tiene los siguientes objetivos de aprendizaje:

+ Entender que hay otras técnicas diferentes a la estadística correlacional para entender (y modelar) la naturaleza. 
+ Aprender que estas otras técnicas (evaluación multicriterio, integración booleana de variables, etc.) tienen, como todo, ventajas e inconvenientes.
+ Aprender técnicas de integración de datos relacionados con la asistencia a la toma de decisiones. 
+ Poner en práctica (al menos parcialmente) alguna de estas técnicas.



## Introducción

Partimos de la pregunta planteada en la sesión anterior:

> ¿Qué variables podemos utilizar para declarar una zona como espacio protegido?

Responder a esta pregunta desde la lógica correlacional a la que estamos acostumbrados (variable dependiente y variables dependientes que se relacionan) es imposible por varios motivos:

+ Hay demasiadas variables en la susceptiblidad de un territorio para ser útil desde el punto de vista de la protección de la naturaleza. No podemos contemplarlas todas.
+ Aunque consiguiéramos fijar algunas variables, no disponemos de la capacidad experimental necesaria para establecer relaciones entre las variables. Tendríamos que plantear un experimento en el que las distintas variables potencialmente explicativas (diversidad, distancia a núcleos urbanos, etc.) se manifestaran de manera similar en dos territorios: uno protegido y otro sin proteger. Esto es imposible.

Así que para decidir qué lugares son más adecuados para albergar un espacio protegido debemos de buscar otros métodos de generar conocimiento. Estas aproximaciones, más difusas y flexibles que las que conocemos, nos permiten abordar problemas como el que nos ocupa. Podemos englobar estas técnicas bajo la denominación de "álgebra de mapas". Estos métodos consisten en "unir" las distintas variables implicadas en un proceso o problema concreto usando justificaciones o razonamientos relacionados con el conocimiento experto. Se trata, por tanto, de "proyectar" en un procedimiento matemático el conocimiento que una o varias personas tienen sobre un problema o proceso concreto. Estas técnicas son muy fáciles de implementar, ya que implican operaciones matemáticas sencillas. Su principal desventaja es que son muy dependientes del conocimiento experto. De modo que si este está sesgado o es incorrecto, también lo serán los resultados obtenidos. Para reducir esta fuente de error se suelen aplicar usando colectivos de personas con distintas "versiones" del conocimiento experto. 

En la sesión anterior se identificaron una serie de variables potencialmente útiles para responder a la pregunta que nos ocupa. Estas variables se identificaron basándose en el criterio experto de los estudiantes y de la profesora Cristina:

+ Diversidad. La diversidad biológica es importante para considerar una zona como potencialmente protegible. Se supone que es esa diversidad la que queremos proteger. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/shannon.tif) puedes descargar el mapa de diversidad de Andalucía. Y [aquí](https://raw.githack.com/aprendiendo-cosas/P_shannon_ecologia_ccaa/main/guion_practica_mapa_biodiversidad.html) puedes ver cómo se obtuvo. 
+ Distancia a zonas urbanas. La distancia entre la zona protegida y los núcleos urbanos también es importante porque esto puede condicionar los posibles impactos al espacio protegido o el uso que se hace de este. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/dist_zona_urbana.tif) puedes descargar el mapa de distancias de cada punto de Andalucía a la zona urbana más cercana. 
+ Distancia a vías de comunicación. Igualmente, lo bien o mal comunicado que esté un espacio protegido condiciona tanto los impactos potenciales de la actividad humana como su posible uso por parte de la sociedad. [Aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/dist_red_viaria.tif) puedes descargar el mapa de distancias de cada punto de Andalucía a la carretera más cercana. 
+ Efecto del cambio climático. Sabemos que el clima está cambiando. Quizás es importante tener en cuenta esta variable para diseñar nuestra red de espacios protegidos. Usaremos una capa que muestra la estimación de la desviación de temperatura media anual (en décimas de grado) para la década de 2090 a 2100. Esta capa se ha obtenido a partir de la [REDIAM](https://www.juntadeandalucia.es/medioambiente/portal/acceso-rediam) y puedes descargla [aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/temp_futuro.tif). 

Esta fase de enumeración de las variables es clave porque en ella realizamos un proceso de abstracción o de modelización de la realidad: es necesario entender bien el problema de gestión o científico que queremos resolver para identificar adecuadamente las variables involucradas en el mismo. 

También es la fase más sencilla y más intuitiva. A partir de aquí, la cosa se complica (solo un poco). 

Una vez que hemos identificado las variables importantes, es fundamental saber si disponemos de datos para calcularlas. Si no tenemos datos para describir cómo cambia la diversidad en nuestra zona de estudio, por ejemplo, no podemos usar esa variable. En estos casos se suele recurrir a variables "subrogadas" (o proxy). Se trata de variables que, si bien no corresponden con la original que consideramos importante, están relacionados con ella. Por ejemplo, si estamos trabajando en una zona montañosa y necesitamos un mapa de precipitación del que no disponemos, podemos usar la altitud como subrogado de la precipitación. 

El siguiente esquema muestra de manera resumida las distintas fases que hemos de cumplir para aplicar estas técnicas difusas propias de la álgebra de mapas. 



![esquema](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/refs/heads/main/imagenes/esquema_metodo.png)



En las siguientes secciones se describen con más detalle los siguientes pasos de la metodología propuesta.




## Transformación de variable a criterio

En la sesión anterior hemos trabajado en la identificación de variables que son importantes para el ejemplo que nos ocupa: identificación de lugares adecuados para la creación de espacios protegidos. Estas variables se representan en este ejemplo como mapas que describen la distribución en el territorio de la variable en cuestión. Además se pueden usar para multitud de situaciones diferentes. Es decir, un mapa de diversidad, por ejemplo, se puede usar para nuestro caso de estudio y para cualquier otro en el que el suelo sea relevante.

Pero cuando aplicamos a la variable un cierto criterio decisional debemos de transformar el mapa que representa la distribución espacial de dicha variable. Es decir, si queremos tener un mapa que muestre la distribución espacial de un criterio concreto, es necesario transformar la variable de la que partimos. Por ejemplo, imaginemos que queremos ubicar en el territorio un área recreativa. Y resulta que la densidad del bosque es determinante para esto: las zonas más densas no son adecuadas porque en ellas no caben las mesas del área recreativa. Así, en este caso, **al aumentar la densidad del bosque, se reduce la idoneidad para albergar áreas recreativas**. En el proceso de transformación de la *variable* a *criterio*, aplicamos una función de transformación. Esta función cumple dos objetivos:

+ Estandariza los valores de todos los mapas para usar un rango de 0 a 1 (o a veces de 0 a 255)
+ Transforma los valores de la variable (producción primaria, profundidad del suelo, diversidad, etc.) a valores de idoneidad cualitativos.

La función de transformación puede tener formas diferentes (ver siguiente figura).



![esquema](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/refs/heads/main/imagenes/estandarizacion.jpg)

En nuestro caso asumiremos que la relación entre cada variable y su criterio es lineal. Así que tendremos dos situaciones representadas por los dos dibujos que hay a continuación: Función de preferencia directa e inversa. 



![lineal](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/refs/heads/main/imagenes/funcion_pertenencia_lineal.png)



En los dibujos anteriores también puedes ver cómo calcular los parámetros de las funciones. Dado que una recta está definida por dos puntos, es fácil despejar los parámetros de la ecuación de la recta (pendiente y ordenada en el origen) a partir de los valores extremos (que toman valores 0 y 1 en el mapa de idoneidad).

Para aplicar estas funciones de transformación a las variables con las que trabajamos tendremos que parametrizar las ecuaciones lineales anteriores. Lo haremos de la siguiente forma en QGIS.

### Mapa de diversidad -> Aptitud con relación a la biodiversidad.
Asumiremos una relación directa entre variable y aptitud. Es decir, a más diversidad mejor para nuestros objetivos (identificar sitios potencialmente protegibles). Sabemos que los valores máximos y mínimos del mapa de diversidad son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0.008539155125618
+ Máximo: 6.4734792709351
+ Por tanto, la ecuación sería así:

```python  
  (1/(6.4734792709351-0.072917148470879))*"shannon@1" - (0.072917148470879/(6.4734792709351-0.072917148470879))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_shannon.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/apt_shannon.tif) puedes descargarlo. 

### Distancia a zonas urbanas -> Aptitud con relación a la distancia a zonas urbanas.
Asumiremos una relación directa entre variable y aptitud. Es decir, a más distancia mejor para nuestros objetivos (identificar sitios potencialmente protegibles). Justificamos esta afirmación diciendo que las zonas urbanas generan impactos importantes en los espacios protegidos y por tanto es mejor que estén lejos de ellas. Sabemos que los valores máximos y mínimos del mapa de distancias a zonas urbanas son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0
+ Máximo: 22983.689453125
+ Por tanto, la ecuación sería así:

```python  
  (1/(22983.689453125-0))*"dist_zona_urbana@1" - (0/(22983.689453125-0))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_dist_zona_urbana.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/apt_dist_zona_urbana.tif) puedes descargarlo. 

### Distancia a la red viaria -> Aptitud con relación a la distancia a la red viaria.
Asumiremos una relación inversa entre variable y aptitud. Es decir, a más distancia peor para nuestros objetivos (identificar sitios potencialmente protegibles). Justificamos esta afirmación diciendo que los espacios protegidos necesitan gestión y que para ello es importante que estén cerca de carreteras y caminos. Esto es muy cuestionable en realidad, pero lo hacemos así por fines docentes. Sabemos que los valores máximos y mínimos del mapa de distancias a carreteras son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 0
+ Máximo: 17755.28125
+ Por tanto, la ecuación sería así:

```python  
 (1/(0-17755.28125))*"dist_red_viaria@1" - (17755.28125/(0-17755.28125))
```
Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_dist_red_viaria.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/apt_dist_red_viaria.tif) puedes descargarlo. 



### Aumento previsto de temperatura -> Aptitud con relación al impacto del cambio climático

Asumiremos una relación inversa entre variable y aptitud. Es decir, a más aumento de temperatura respecto a la media de la serie histórica, menos aptitud para nuestro objetivo. Justificamos esta decisión porque nos interesa que los espacios protegidos estén en lugares poco afectados por el cambio climático.  Sabemos que los valores máximos y mínimos del mapa de distancias a carreteras son (podemos verlos fácilmente en las propiedades de la capa, en QGIS)

+ Mínimo: 1.6337893009186
+ Máximo: 17755.28125
+ Por tanto, la ecuación sería así:

```python  
 (1/(1.7122367620468-4.7942304611206))*"temp_futuro@1" - (4.7942304611206/(1.7122367620468-4.7942304611206))
```

Para aplicar esta función lineal basta con poner el código anterior en la calculadora raster de QGIS. El resultado debe de llamarse *apt_temp_futuro.tif*. Si no consigues hacerlo, [aquí](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/apt_temp_futuro.tif) puedes descargarlo. 

Una vez que tenemos todos los criterios espacializados, podemos aplicar dos métodos para integrar las variables: evaluación multicriterio y operadores booleanos. Se describen en los siguientes apartados.



## Evaluación multicriterio

El análisis multicriterio es una técnica muy sencilla que permite combinar en un mismo mapa criterios diferentes. Es una forma de espacializar criterios decisionales basados en conocimiento experto. Es decir, gracias a esta técnica podemos obtener mapas que recojan los criterios de un centro decisor concreto con relación a un aspecto determinado.  En nuestro ejemplo tenemos varios criterios y se trata de unificarlos en un único mapa que asigne un valor de aptitud global a cada punto afectado por el incendio. 

Para agregar los criterios empezaremos asignando un peso a cada uno de ellos. La suma de los pesos ha de ser 1. El criterio que tenga más peso contribuirá en mayor medida al mapa final. La siguiente figura muestra cómo se haría este proceso. 

![multicriterio](https://raw.githubusercontent.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/refs/heads/main/imagenes/pesos_ponderados.png)

El proceso de integración se hace fácilmente con la calculadora de mapas de QGIS u operando con las capas raster en el caso de que trabajemos con R o con Python. El resultado final es la suma del producto de cada criterio (capa _apt_) por su peso. El valor relativo de cada peso nos da una idea del escenario decisional en el que nos encontramos. Por ejemplo, la siguiente combinación de pesos da mucha importancia a la diversidad y al escenario de cambio climático. Llamaremos al resultado de esta operación [*escenario_1.tif*](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/escenario_1.tif)

```python  
("apt_shannon@1" * 0.4)+("apt_temp_futuro@1"*0.4)+ ( "apt_dist_red_viaria@1"*0.1)+("apt_dist_zona_urbana@1"*0.1)
 
```
También podemos crear otro escenario quitando importancia al efecto del cambio climático. Llamaremos [*escenario_2.tif*](https://github.com/aprendiendo-cosas/TP_integracion_capas_ecoinf_bio/raw/refs/heads/main/geoinfo/escenario_2.tif) a este resultado:

```python  
("apt_shannon@1" * 0.5)+("apt_temp_futuro@1"*0.1)+ ( "apt_dist_red_viaria@1"*0.2)+("apt_dist_zona_urbana@1"*0.2)
 
```

Uno de los problemas del análisis multicriterio es que ocurre una compensación de criterios. Si una variable tiene un valor muy alto en un lugar determinado, puede que el resultado final en ese punto sea alto aunque el valor de un criterio importante en ese punto sea bajo. Esto puede hacer que lugares no adecuados sean etiquetados como sí adecuados. Un ejemplo que ilustra esta situación: imaginemos que queremos montar un equipo de baloncesto. Un buen jugador de baloncesto ha de tener las siguientes características:
+ Altura.
+ Fortaleza en los brazos.
+ Tobillos resistentes.

Si le damos distintos pesos a esas variables y con eso "puntuamos" la idoneidad de una lista de personas para entrar en nuestro equipo, puede darse la situación de que una persona tenga alta puntuación final aún teniendo los tobillos débiles. Eso implica tomar una decisión equivocada puesto que estaríamos incluyendo en el equipo a una persona que no rendiría bien. Esta situación denota que hay criterios que no solo tienen más peso que otros, sino que además deben satisfacerse **necesariamente** para tomar una decisión acertada. Y esto nos lleva a la segunda técnica de análisis de la decisión:



## Operadores lógicos

En esta segunda técnica no se asignan pesos a los criterios que combinamos sino que se establecen condiciones que deben cumplir los lugares de nuestra zona de estudio para ser idoneos según el objetivo del proceso decisiona en cuestión. Volviendo al ejemplo del jugador de baloncesto ideal, diríamos algo así: debe de tener los tobillos fuertes **y** **o bien** ser fuerte **o bien** ser alto. De alguna forma estamos diciendo que hay una condición **necesaria** para ser buen jugador, pero no suficiente. Necesita tener los tobillos resistentes y luego una de las otras dos condiciones. Esta forma de combinar criterios decisionales recibe el nombre de integración mediante operadores booleanos porque implican el uso de las conjunciones **o** e **y**. 

En el ejemplo que nos ocupa, usaremos operadores lógicos para integrar las cuatro capas. Consideraremos que un lugar es adecuado para satisfaer nuestros objetivos si cumple un criterio específico y una combinación de los otros dos. Es decir, pondremos como criterio fundamental que los lugares adecuados tengan una **alta diversidad** o que sean **poco vulnerables al cambio climático**. Además, un lugar será adecuado para nuestros objetivos si también cumple el criterio de o bien **estar cerca de una carretera** o bien **estar lejos de un núcleo urbano**. Es decir, en conjunto aplicaremos los siguientes criterios concatenados: Un lugar es considerado como adecuado si:

+ Tiene alta diversidad **o** baja vulnerabilidad al cambio climático.
+ **Y**
+ Está cerca de una carretera **o** lejos de un núcleo urbano.

Para implementar esta operación en un SIG, usamos dos operadores matemáticos muy sencillos:

+ Valor **máximo** entre dos capas: es el equivalente al operador **O**. Si en un píxel hay valores altos de aptitud en una capa y bajos en otra, el resultado será alto, puesto que estamos eligiendo el máximo de ambos. Si la aptitud es alta en los dos casos, también seleccionaremos un valor alto. Es decir, se trata de un operador poco restrictivo.
+ Valor **mínimo** entre dos capas: es el equivalente al operador **Y**. Si en un píxel hay valores altos de aptitud en una capa y bajos en otra, el resultado será bajo, puesto que estamos eligiendo el mínimo de ambos. Solo si la aptitud es alta en los dos casos, seleccionaremos un valor alto. Es decir, se trata de un operador poco restrictivo.

La siguiente figura muestra el funcionamiento de estos operadores:

<img src="https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/imagenes/operadores_booleanos.png" alt="imagen" style="zoom:40%;" />

Para aplicar estos operadores a nuestras capas, usamos la calculadora de mapas de QGIS en tres pasos anidados:

Primero combinamos con el operador **o** la aptitud con relación a la diversidad y la vulnerabilidad al cambio climático:

```py
MAX ( "apt_shannon@1","apt_temp_futuro@1")
```

Al resultado le llamamos *apt_shannon_o_apt_temp_futuro.tif*

  MIN (MAX ( "apt_shannon@1","apt_temp_futuro@1"),  MAX ("apt_dist_red_viaria@1","apt_dist_zona_urbana@1")

Los operadores anteriores son un poco "rígidos" dado que solo seleccionan los valores extremos (mínimo o máximo). Para suavizar el resultado se pueden usar otros operadores como los mostrados en la siguiente figura:

<img src="https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/imagenes/operadores_difusos.png" alt="imagen" style="zoom:40%;" />



## Reclasificación de los resultados obtenidos

Tras aplicar cualquiera de las técnicas anteriores obtendremos un mapa con valores de aptitud que van de 0 a 1. Este mapa puede ser muy útil para comprender mejor el proceso socioecológico en el que estamos trabajando. Pero normalmente cuando se toman decisiones es necesario seleccionar una serie de zonas concretas en las que se va a realizar una actuación determinada. Por eso es útil simplificar el mapa resultante para elegir solo los lugares (=píxeles) que resulten más idoneos para nuestro objetivo. El resto los descartaremos porque no reunen los requisitos que hemos impuesto. Para hacer esta selección aplicaremos una operación muy común en análisis raster: [reclasificación](https://docs.qgis.org/3.4/en/docs/user_manual/processing_algs/qgis/rasteranalysis.html#qgisreclassifybytable). Consiste en reducir la diversidad de valores de un raster asigando nuevos en función de un rango. Por ejemplo, asignaremos el valor de 1 a todos los píxeles que tengan una aptitud igual o mayor de 0.8. Para hacer esto, construimos una tabla de reclasificación.

Para reclasificar una capa rastser en QGIS, buscamos el algoritmo "reclassify by table" en el buscador de procesos de QGIS. Añadimos los siguientes parámetros:
- _raster layer_: _apt\_final.tif_
- _reclassification table_: Abrimos la tabla y añadimos las siguientes filas:


| Desde (Mínimo) | hasta (Máximo)| Valor nuevo|
|----------------:|------------:|---------:|
|0|0.9| 0|
| 0.9 | 1|1|
 - _reclassified raster_ (capa de salida): _apt\_final\_re.tif_





## Lecturas complementarias

Además de lo visto anteriormente, os paso la siguiente información que puede resultar de utilidad:

+ [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/modelos_ecologicos.pdf) que describe distintos tipos de modelos ecológicos. Incide en alguno de los conceptos descritos en la sesión final de nuestra asignatura. 
+ [Resumen](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/herramientas_apoyo_decisiones.pdf) de mi tesis (año 2003, no os riais de los esquemas, por favor. En esa época no existía R). En el texto se describen los conceptos generales sobre integración de información ambiental usando técnicas de operadores booleanos. He recortado solo la parte interesante. Eso hace que el texto no sea muy fluido porque faltan secciones.
+ Varios textos sobre análisis multicriterio:
  + [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/multicriterio_seleccion_zonas_plantas_electricas.pdf) sobre el uso del análisis multicriterio para localizar plantas de producción fotovoltaica. 
  + [Interesante](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/MCE_review.pdf) revisión del uso de las técnicas multicriterio en cuestiones de conservación de la naturaleza. Muy recomendable este trabajo.
  + [Artículo](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/ecological_corridors_multicriteria.pdf) que describe cómo la conectividad ecológica del paisaje usando evaluación multicriterio.
  + [Informe](https://github.com/aprendiendo-cosas/TP_integracion_final_SIG_II_geoforest/raw/2023_2024/biblio/memoria_apicola_2004.pdf) de la REDIAM que describe cómo se hizo el mapa de aprovechamientos apícolas de Andalucía usando la técnica de la evaluación multicriterio. 
+ [Manual](https://geodacenter.github.io/workbook/9a_spatial1/lab9a.html) interesante sobre el uso de la clasificación espacialmente explícita.






# Vídeo de la sesión

Este vídeo muestra los contenidos comentados durante la sesión del día 24 de noviembre. 


<iframe width="560" height="515" src="https://www.youtube.com/embed/teqT3d6G8E4?si=WYVQ-H-rQ0_8VYfs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>